---
title: 'PowerShell 7 - choose Neovim "stable" or "test" config'
date: 2025-08-19T15:48:10+02:00
draft: false
categories:
- Utility
tags:
- Windows
toc: true
---

***

## 1. PowerShell 7 \$profile

In PowerShell 7, the `$PROFILE` variable represents the path to your profile script—a script that runs every time you start PowerShell (unless using `-NoProfile`).[^1][^2][^5]

**Typical locations for PowerShell 7 profile scripts:**

- **Current User, Current Host:**
`$HOME\Documents\PowerShell\Microsoft.PowerShell_profile.ps1`
- **Current User, All Hosts:**
`$HOME\Documents\PowerShell\profile.ps1`
- **All Users, Current Host:**
`$PSHOME\Microsoft.PowerShell_profile.ps1` (`$PSHOME` is usually `C:\Program Files\PowerShell\7\`)
- **All Users, All Hosts:**
`$PSHOME\profile.ps1`

To see all profile file locations in your session, use:

```powershell
$PROFILE | Select-Object *
```

To edit your main profile file for the current user and host:

```powershell
notepad $PROFILE
```

If the file doesn't exist, PowerShell will prompt you to create it.[^2][^5]

The profile script can be used to define functions, aliases, variables, or import modules, making them available in every new PowerShell session.

**My profile**: [Microsoft.PowerShell_profile.ps1.txt](/posts/2025/2025_08m_19-Microsoft.PowerShell_profile.ps1.txt)
`/ C:\Users\<you>\Documents\PowerShell\Microsoft.PowerShell_profile.ps1 /`


***

## 2. pwsh 7 script - choose on screen between nvims and nvimt

In my PowerShell profile, I created two functions, to launch Neovim with different configurations by setting the environment variable `NVIM_APPNAME`:

```powershell
# Neovim STABLE config
function nvims {
    $env:NVIM_APPNAME = "nvim"
    nvim nazivi_2025_temp.txt
}

# Neovim TEST config
function nvimt {
    $env:NVIM_APPNAME = "nvimt"
    nvim
}
```

Explanation:

- The function `nvims` sets `NVIM_APPNAME` to `"nvim"` and opens the file `nazivi_2025_temp.txt` in Neovim.
- The function `nvimt` sets `NVIM_APPNAME` to `"nvimt"` and launches Neovim without specifying a file.

You can call the above functions with "nvims" or "nvimt" in the PowerShell prompt.

**pwsh 7 script**: This script shows both options, takes user input, and outputs the selection.\
If the user enters "1" or "nvims", it selects **nvims**; "2" or "nvimt" selects **nvimt**; any other input results in "Invalid Selection."


```powershell
# Neovim STABLE config
function nvims {
    $env:NVIM_APPNAME = "nvim"
    nvim nazivi_2025_temp.txt
}

# Neovim TEST config
function nvimt {
    $env:NVIM_APPNAME = "nvimt"
    nvim
}

$nvimOptions = @("nvims", "nvimt")
Write-Host "Choose Neovim config:"

# Show the list with numbers
# for ($i = 0; $i -lt $nvimOptions.Count; $i++) {
for ($i = 0; $i -lt $nvimOptions.length; $i++) {
    Write-Host "$($i + 1). $($nvimOptions[$i])"
}
$choice = Read-Host "Write number or text value"

switch ($choice.ToLower()) {
    "1" { $selected = $nvimOptions[0] }
    "2" { $selected = $nvimOptions[1] }
    "nvims" { $selected = $nvimOptions[0] }
    "nvimt" { $selected = $nvimOptions[1] }
    default { $selected = "Invalid Selection" }
}
Write-Output "You chose: $selected"

if ($selected -eq "nvims") {
    nvims
} elseif ($selected -eq "nvimt") {
    nvimt
} else {
    Write-Output "No applicable function for selection: $selected"
}
```

- If the user chooses "nvims" or "1", the `nvims` function runs.
- If "nvimt" or "2" is chosen, the `nvimt` function runs.
- If another valid option is chosen, no function is called, and a message informs the user.

<span style="display:none">[^3][^4][^6][^7]</span>

<div style="text-align: center">⁂</div>

[^1]: https://learn.microsoft.com/en-us/powershell/scripting/whats-new/migrating-from-windows-powershell-51-to-powershell-7?view=powershell-7.5

[^2]: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-7.5

[^3]: https://www.reddit.com/r/PowerShell/comments/hc4seg/powershell_7_profile_load_help/

[^4]: https://stackoverflow.com/questions/75540911/how-do-i-create-a-profile-in-powershell-7-3-2

[^5]: https://www.techtarget.com/searchwindowsserver/tutorial/How-to-find-and-customize-your-PowerShell-profile

[^6]: https://subscription.packtpub.com/book/cloud-and-networking/9781804614235/1/ch01lvl1sec06/building-powershell-7-profile-files

[^7]: https://www.youtube.com/watch?v=VeEdGTmCW5g






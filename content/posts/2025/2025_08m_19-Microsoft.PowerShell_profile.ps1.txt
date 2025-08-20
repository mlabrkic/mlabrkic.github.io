# https://learn.microsoft.com/en-us/windows/terminal/tutorials/new-tab-same-directory

# https://learn.microsoft.com/en-us/windows/terminal/tutorials/new-tab-same-directory#powershell-powershellexe-or-pwshexe

function prompt {
    $loc = $executionContext.SessionState.Path.CurrentLocation;

      $out = "PS $loc$('>' * ($nestedPromptLevel + 1)) ";
        if ($loc.Provider.Name -eq "FileSystem") {
              $out += "$([char]27)]9;9;`"$($loc.ProviderPath)`"$([char]27)\"
                }
                  return $out
}

Invoke-Expression (& { (zoxide init powershell | Out-String) })

# ------------------------------
# Neovim:

# $env:PATH += ";C:\UTILS\Neovim\bin"
$env:TERM = "xterm-256color"

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

# ------------------------------

---
title: 'Windows Terminal - choose Neovim "stable" or "test" config'
date: 2025-08-13T14:37:11+02:00
draft: false
categories:
- Utility
tags:
- Windows
- Windows Terminal
toc: true
---

## Neovim Windows Terminal profile with \$env:NVIM_APPNAME

To create a dedicated **Neovim profile in Windows Terminal** that automatically sets the `$env:NVIM_APPNAME` environment variable, you should customize your Windows Terminal `settings.json` to add a specific profile for Neovim with the appropriate environment variable.

This allows you to launch Neovim with a separate config directory (profile) just by selecting the profile from the Windows Terminal dropdown—ideal for testing configs or keeping different setups isolated.

Neovim (Vim-based text editor): https://neovim.io/

Check in Neovim: `:h NVIM_APPNAME`, `:echo $NVIM_APPNAME` and `:echo stdpath("config")`

This needs to be done first:
1. Copy the Neovim test configuration to the "nvimt" folder: `C:\Users\<you>\AppData\Local\nvimt`
2. Then run the Neovim-TEST profile in the "Windows Terminal".

```
These are my folders (stable and test):

C:\Users\<you>\AppData\Local\
nvim
nvim-data

nvimt
nvimt-data
```


***

## Step-by-Step: Windows Terminal Neovim Profile with `$env:NVIM_APPNAME`

***

### 1. **Open Windows Terminal Settings**

- Press `Ctrl + ,` or use the dropdown menu (top bar) → **Settings**.
- Alternatively, open the `settings.json` file for advanced editing.


### 2. **Add a New Profile for Neovim**

Locate the `"profiles"` section and add a new object under `"list"`. Here is my profile for Neovim with `NVIM_APPNAME` set:

```json
        "list":
        [
            {
                "commandline": "\"C:\\UTILS\\Neovim\\bin\\nvim.exe\"",
                "environment":
                {
                    "NVIM_APPNAME": "nvim"
                },
                "font":
                {
                    "face": "SauceCodePro Nerd Font",
                    "size": 16,
                    "weight": "medium"
                },
                "guid": "{85d07d3a-2606-428a-9cf8-16ba4c45c770}",
                "hidden": false,
                "icon": "C:\\UTILS\\Neovim\\share\\nvim\\runtime\\neovim.ico",
                "name": "Neovim-STABLE",
                "startingDirectory": "%USERPROFILE%\\Documents"
            },
            {
                "commandline": "\"C:\\UTILS\\Neovim\\bin\\nvim.exe\"",
                "environment":
                {
                    "NVIM_APPNAME": "nvimt"
                },
                "font":
                {
                    "face": "SauceCodePro Nerd Font",
                    "size": 16,
                    "weight": "medium"
                },
                "guid": "{31d2b985-d9d6-4288-b31d-8fd24d6b9bf0}",
                "hidden": false,
                "icon": "C:\\UTILS\\Neovim\\share\\nvim\\runtime\\neovim.ico",
                "name": "Neovim-TEST",
                "startingDirectory": "%USERPROFILE%\\Documents",
                "tabColor": "#FFFFCC"
            },

          ...

        ]
```

- Change `"nvimt"` to whatever profile/directory name you want Neovim to use, e.g., `"astronvim"`, `"lazyvim"`, etc.
- Adjust `commandline`, `icon`, `colorScheme`, or `fontFace` as needed.
- `environment` is the critical key: it will set the environment variable **only for terminals started from this profile**.[^1][^2][^3]


### 3. **Save and Use Your Profile**

- Save the edited `settings.json` (the terminal reloads automatically).
- Use the **down-arrow** in Windows Terminal to select your new “Neovim (Custom Profile)” tab.
- Every new tab with this profile will run `nvim` with `NVIM_APPNAME` set, making Neovim use the config directory at `%LOCALAPPDATA%\<NVIM_APPNAME>` (e.g., for `"lvim"`, it uses `C:\Users\<you>\AppData\Local\lvim`).[^4][^5][^6]

***

## Key Points

- **Isolated configs:** Multiple `NVIM_APPNAME` profiles let you isolate configs/plugins/data per Neovim profile.
- **No scripting needed:** The `environment` option in profile config ensures the variable is set just for that profile—no need to edit `PROFILE` scripts or system-wide variables.
- **Custom launch:** You can have as many Neovim profiles (for different setups) in the Windows Terminal dropdown as you wish; just duplicate and adjust the `environment` variable for each.

***

### Reference Profile Block

```json
{
    "guid": "{unique-guid-here}",
    "name": "Neovim (Astronvim)",
    "commandline": "nvim",
    "environment": { "NVIM_APPNAME": "astronvim" }
}
```


***

With this **Windows Terminal profile setup**, simply open a dedicated Neovim tab to use your chosen config profile—fast and easily switchable without manual commandline `set` or `export` gymnastics.[^2][^5][^6][^3][^4][^1]

<div style="text-align: center">⁂</div>

[^1]: https://code.visualstudio.com/docs/terminal/profiles

[^2]: https://www.ninjaone.com/blog/add-or-remove-profiles-in-windows-terminal/

[^3]: https://github.com/microsoft/terminal/issues/6604

[^4]: https://michaeluloth.com/neovim-switch-configs/

[^5]: https://www.reddit.com/r/neovim/comments/12k2u6e/nvim_appname/

[^6]: http://neovim.io/doc/user/vim_diff.html

[^7]: https://github.com/neovim/neovim/issues/21691

[^8]: https://www.reddit.com/r/neovim/comments/1crdv93/neovim_on_windows_using_windows_terminal_and/

[^9]: https://neovim.io/doc/user/starting.html

[^10]: https://learn.microsoft.com/en-us/windows/terminal/customize-settings/profile-appearance

[^11]: https://www3.ntu.edu.sg/home/ehchua/programming/howto/Environment_Variables.html

[^12]: https://www.jasonross.dev/neovim-setup-on-windows-2022/

[^13]: https://stackoverflow.com/questions/62578458/vim-nvim-not-filling-windows-terminal

[^14]: https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/How-to-set-an-environment-variable.html

[^15]: https://blog.nikfp.com/how-to-install-and-set-up-neovim-on-windows

[^16]: https://www.youtube.com/watch?v=v34n_lgOe1c

[^17]: https://learn.microsoft.com/en-us/windows/terminal/customize-settings/profile-general

[^18]: https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/set_1

[^19]: https://stackoverflow.com/questions/66994307/how-to-set-environment-variables-in-windows-command-prompt-so-they-re-passed-in

[^20]: https://stackoverflow.com/questions/73941134/how-do-i-create-a-new-custom-profile-in-windows-terminal-from-a-powershell-scrip




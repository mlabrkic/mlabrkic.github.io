---
title: "Windows Terminal"
date: 2023-08-23T12:58:55+02:00
draft: false
categories:
- Utility
tags:
- Windows
- Windows Terminal
toc: true
---

---

"[Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/) is a modern host application for the command-line shells you already love, like Command Prompt, PowerShell, and bash (via Windows Subsystem for Linux (WSL))."

[These are my settings (Windows Terminal): "settings.json"](/posts/2023/2023-12M-03-settings.json)


## 01. How to use the command palette in Windows Terminal

You can invoke the [command palette](https://learn.microsoft.com/en-us/windows/terminal/command-palette) by typing `Ctrl+Shift+P`.


#### [Command line mode](https://learn.microsoft.com/en-us/windows/terminal/command-palette#command-line-mode)

If you'd like to enter a wt command into the command palette,
you can do so by deleting the > character in the text box.
This will run the wt command in the current window.

Open "Command Palette" (Ctrl+Shift+P), delete the > character in the text box.
Copy and paste some of this:

`split-pane`\
`split-pane cmd /k dir`\
`split-pane "wsl.exe"`


#### [Nested commands](https://learn.microsoft.com/en-us/windows/terminal/command-palette#nested-commands)

Windows Terminal "settings.json" ( `Ctrl+,` ):
```json
        {
            "name": "F- Change font size...",
            "commands": [
                { "command": { "action": "adjustFontSize", "delta": 1 } },
                { "command": { "action": "adjustFontSize", "delta": -1 } },
                { "command": "resetFontSize" },
            ]
        },
        {
            "name": "P- Pane ...",
            "commands": [
                { "command": { "action": "splitPane", "split": "vertical" }, "keys": "alt+shift+plus" },
                { "command": { "action": "splitPane", "split": "horizontal" }, "keys": "alt+shift+-" },
                { "command": { "action": "moveFocus", "direction": "right" }, "keys": "alt+right" },
                { "command": { "action": "moveFocus", "direction": "left" }, "keys": "alt+left" },
                { "command": { "action": "swapPane", "direction": "right" } },
                { "command": { "action": "swapPane", "direction": "left" } },
                { "command": "toggleSplitOrientation" },
                { "command": { "action": "resizePane", "direction": "left" }, "keys": "alt+shift+left" },
                { "command": { "action": "resizePane", "direction": "right" }, "keys": "alt+shift+right" },
                { "command": "closePane", "keys": "ctrl+shift+w" },
                { "command": "togglePaneZoom", "keys": "ctrl+f11" },
                { "command": { "action": "splitPane", "split": "auto", "splitMode": "duplicate" }, "keys": "alt+shift+d" },
            ]
        }
```

---

## 02. Windows Terminal panes

"[Panes](https://learn.microsoft.com/en-us/windows/terminal/panes) give you the ability to run multiple command-line applications next to each other within the same tab."


#### [Creating a new pane](https://learn.microsoft.com/en-us/windows/terminal/panes#creating-a-new-pane)

To create a new vertical pane of your default profile,
you can press the `Alt+Shift++` key combination.
(alt+shift+plus)

For a horizontal pane of your default profile, you can use `Alt+Shift+-`.

"settings.json" ( Ctrl+, ):
```json
        {
            { "command": { "action": "splitPane", "split": "vertical" }, "keys": "alt+shift+plus" },
            { "command": { "action": "splitPane", "split": "horizontal" }, "keys": "alt+shift+-" },
        }
```

or,\
Command Palette (Ctrl+Shift+P):\
spd(own)  &nbsp; ==> &nbsp; `splitPane, down`\
spr(ight) &nbsp; ==> &nbsp; `splitPane, right`


#### [Switching between panes](https://learn.microsoft.com/en-us/windows/terminal/panes#switching-between-panes)

If you hold the Alt key, you can use your arrow keys to move your focus between panes.

```json
        {
            { "command": { "action": "moveFocus", "direction": "down" }, "keys": "alt+down" },
            { "command": { "action": "moveFocus", "direction": "left" }, "keys": "alt+left" },
        }
```

`Alt+Right`\
`Alt+Left`\
...


#### [Swapping panes](https://learn.microsoft.com/en-us/windows/terminal/panes#swapping-panes)

```json
        {
            { "command": { "action": "swapPane", "direction": "down" } },
            { "command": { "action": "swapPane", "direction": "left" } },
        }
```

Command Palette (Ctrl+Shift+P):\
swl(eft) &nbsp; ==> &nbsp; `swapPane, left`\
swr(ight) &nbsp; ==> &nbsp; `swapPane, right`


#### [Moving panes](https://learn.microsoft.com/en-us/windows/terminal/panes#moving-panes)

Panes can also be moved between tabs,
creating a new tab if one with the target index does not exist.

Command Palette (Ctrl+Shift+P):\
mp1 &nbsp; ==> &nbsp; `movePane, tab index:1`


#### [Changing split orientation](https://learn.microsoft.com/en-us/windows/terminal/panes#changing-split-orientation)

```json
        {
            { "command": "toggleSplitOrientation" }
        }
```

Command Palette (Ctrl+Shift+P):\
togor &nbsp; ==> &nbsp; `toggleSplitOrientation`


#### [Resizing a pane](https://learn.microsoft.com/en-us/windows/terminal/panes#resizing-a-pane)

You can adjust the size of your panes by holding Alt+Shift and
using your arrow keys to resize the focused pane.

```json
        {
            { "command": { "action": "resizePane", "direction": "down" }, "keys": "alt+shift+down" },
            { "command": { "action": "resizePane", "direction": "left" }, "keys": "alt+shift+left" },
            { "command": { "action": "resizePane", "direction": "right" }, "keys": "alt+shift+right" },
            { "command": { "action": "resizePane", "direction": "up" }, "keys": "alt+shift+up" }
        }
```

`alt+shift+left`\
`alt+shift+right`


#### [Closing a pane](https://learn.microsoft.com/en-us/windows/terminal/panes#closing-a-pane)

```json
        {
            { "command": "closePane", "keys": "ctrl+shift+w" }
        }
```


#### [Zooming a pane](https://learn.microsoft.com/en-us/windows/terminal/panes#zooming-a-pane)

You can zoom the focused pane to fill the entire contents of the window.

```json
        {
            { "command": "togglePaneZoom", "keys": "ctrl+f11" },
        }
```
The togglePaneZoom action is not bound to any keys by default.

---

## 03. Customizing panes using key bindings

#### [Duplicating a pane](https://learn.microsoft.com/en-us/windows/terminal/panes#duplicating-a-pane)


```json
        {
            { "command": { "action": "splitPane", "split": "auto", "splitMode": "duplicate" }, "keys": "alt+shift+d" }
        }
```
Duplicate pane `alt+shift+d`\
( Duplicate tab `Ctrl+shift+d` )


#### [Color a tab](https://learn.microsoft.com/en-us/windows/terminal/tips-and-tricks#color-a-tab)

The tabColor can be set as part of a profile.

```json
        {
            {
                "font":
                {
                    "size": 14.0
                },
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "name": "PowerShell",
                "source": "Windows.Terminal.PowershellCore",
                "startingDirectory": "%USERPROFILE%\\Documents",
                "tabColor": "#012456",
            },

        }
```

---

## 04. Mouse interaction

There are several ways to interact with Windows Terminal [using a mouse](https://learn.microsoft.com/en-us/windows/terminal/tips-and-tricks#mouse-interaction).


#### [Drag and drop file/folder to open](https://learn.microsoft.com/en-us/windows/terminal/tips-and-tricks#drag-and-drop-filefolder-to-open)

You can hold Alt to open a new pane in your current tab or hold Shift to open a new window.


#### [Clear your screen](https://learn.microsoft.com/en-us/windows/terminal/tips-and-tricks#clear-your-screen)

Command Palette (Ctrl+Shift+P):\
cl &nbsp; ==> &nbsp; `clear`


---

## 05. Tips and tricks: Navigate to parent directory

[Navigating to the parent directory](https://learn.microsoft.com/en-us/windows/terminal/tips-and-tricks#navigate-to-parent-directory) with a key binding may also be helpful.

```json
        { "command": {"action": "sendInput", "input": "cd ..\r"}, "keys": "ctrl+up" }

```

Navigating to the "$HOME\Documents":
* PowerShell ... "ctrl+1"
* bash (via Windows Subsystem for Linux (WSL)) ... "ctrl+2"
* Command Prompt ... "ctrl+3"

```json
    {
        { "command": {"action": "sendInput", "input": "cd $HOME\\Documents\r"}, "keys": "ctrl+1" },
        { "command": {"action": "sendInput", "input": "cd /mnt/c/Users/$USER/My\\ Documents\r"}, "keys": "ctrl+2" },
        { "command": {"action": "sendInput", "input": "cd %USERPROFILE%\\Documents\r"}, "keys": "ctrl+3" },
    }
```
You can also use this functionality to run builds or test scripts.


---

## 06. Tutorial: Opening a tab or pane in the same directory in Windows Terminal

[Opening a tab or pane in the same directory in Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/tutorials/new-tab-same-directory)

Typically, the "new tab" and "split pane" actions will always open a new tab/pane in whatever the "startingDirectory" is for that profile. However, on other platforms, it's common for new tabs to automatically use the working directory of the current tab as the starting directory for a new tab. This allows the user to quickly multitask in a single directory.

"To tell the Terminal what the CWD is, you'll need to modify your shell to emit an escape sequence as you navigate the OS. Fortunately, most shells have a mechanism for configuring the "prompt", which is run after every command."


#### [Windows Command Prompt](https://learn.microsoft.com/en-us/windows/terminal/tutorials/new-tab-same-directory#command-prompt-cmdexe)

Windows Command Prompt:\
`set PROMPT=$e]9;9;$P$e\%PROMPT%`\
`setx PROMPT "%PROMPT%"`

Duplicate pane `alt+shift+d`\
( Duplicate tab `Ctrl+shift+d` )


#### [PowerShell](https://learn.microsoft.com/en-us/windows/terminal/tutorials/new-tab-same-directory#powershell-powershellexe-or-pwshexe)


For example, the $PROFILE variable has the following values in the Windows PowerShell console:

```ps1
Current User, Current Host - $PROFILE
Current User, Current Host - $PROFILE.CurrentUserCurrentHost
Current User, All Hosts - $PROFILE.CurrentUserAllHosts
All Users, Current Host - $PROFILE.AllUsersCurrentHost
All Users, All Hosts - $PROFILE.AllUsersAllHosts
```

To see the current values of the `$PROFILE` variable, type:
```ps1
$PROFILE | Select-Object *
```
==>

```ps1
AllUsersAllHosts       : C:\Program Files\PowerShell\7\profile.ps1
AllUsersCurrentHost    : C:\Program Files\PowerShell\7\Microsoft.PowerShell_profile.ps1
CurrentUserAllHosts    : $HOME\Documents\PowerShell\profile.ps1
CurrentUserCurrentHost : $HOME\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
```

The following command determines whether an "Current User, Current Host"
profile has been created on the local computer:
```ps1
Test-Path -Path $PROFILE
```

To create a profile for the current user in the current PowerShell host application, use the following command:

```ps1
if (!(Test-Path -Path $PROFILE)) {
  New-Item -ItemType File -Path $PROFILE -Force
}
```

==> $HOME\Documents\PowerShell\Microsoft.PowerShell_profile.ps1

`notepad $PROFILE`

Add the following to your PowerShell profile:
```ps1
function prompt {
  $loc = $executionContext.SessionState.Path.CurrentLocation;

  $out = "PS $loc$('>' * ($nestedPromptLevel + 1)) ";
  if ($loc.Provider.Name -eq "FileSystem") {
    $out += "$([char]27)]9;9;`"$($loc.ProviderPath)`"$([char]27)\"
  }
  return $out
}
```


#### [Open a new pane with splitPane](https://learn.microsoft.com/en-us/windows/terminal/tutorials/new-tab-same-directory#open-a-new-pane-with-splitpane)

```json
        {
            { "command": { "action": "splitPane", "split": "auto", "splitMode": "duplicate" }, "keys": "alt+shift+d" }
        }
```


---

## 07. COMMAND LINE ARGUMENT EXAMPLES

[EXAMPLES](https://learn.microsoft.com/en-us/windows/terminal/command-line-arguments?tabs=windows#command-line-argument-examples)

The wt command line accepts two types of values: options and commands.\
wt [options] [command ; ]


#### Windows Command Prompt:

Try it: Win-s(earch), cmd, Enter\
Paste one of the lines below (wt ...), Enter

echo %USERPROFILE%

```
wt new-tab PowerShell -c Start-Service ; new-tab cmd /k dir

wt -p "Command Prompt" ; split-pane -p "PowerShell"
wt -p "Command Prompt" -d %USERPROFILE%\Documents ; split-pane -p "PowerShell" -d %USERPROFILE%\Documents

wt ; new-tab cmd /k dir
wt -d %USERPROFILE%\Documents; new-tab -d %USERPROFILE%\Documents cmd /k dir
wt -d %USERPROFILE%\Documents; split-pane -d %USERPROFILE%\Documents cmd /k dir

NOTE:
wt -d %USERPROFILE%\Documents cmd /k dir ; split-pane -p "PowerShell" -d %USERPROFILE%\Documents
wt -d %USERPROFILE%\Documents ; split-pane -d %USERPROFILE%\Documents "wsl.exe"
```


#### PowerShell:

Try it: Win-s(earch), type "powershell" (==> PowerShell 7), Enter

echo $HOME

For example, to open Windows Terminal from PowerShell with three panes,
with the leftpane running a Command Prompt profile and the
right pane split between your PowerShell and
your default profile running WSL, enter:

```
wt -p "Command Prompt" `; split-pane -p "Windows PowerShell" `; split-pane -H wsl.exe

NOTE:
wt -p "Command Prompt" -d $HOME\Documents `; split-pane -p "PowerShell" -d $HOME\Documents
```

---

####  INFO

"[PowerShell](https://learn.microsoft.com/en-us/powershell)" 7.3 installs to a new directory and runs side-by-side with "Windows PowerShell" 5.1.


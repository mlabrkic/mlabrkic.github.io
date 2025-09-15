---
title: 'Multi Commander - choose Neovim "stable" or "test" config'
date: 2025-09-15T14:49:57+02:00
draft: false
categories:
- Utility
tags:
- Windows
- Multi Commander
toc: true
---

This is the *modern way* of selecting the Neovim config folder by setting the **NVIM_APPNAME** environment variable!

Check in Neovim: `:h NVIM_APPNAME`, `:echo $NVIM_APPNAME` and `:echo stdpath("config")`

Multi Commander: https://multicommander.com/

Multi Commander is a multi-tabbed file manager and is an alternative to the standard Windows Explorer. It uses the very popular and efficient dual-panel layout.

Info (Multi Commander: Run the Neovim GUI): https://forum.multicommander.com/forum/index.php/topic,4835.0.html

***

### 1. First of all, do this

1. Copy the Neovim "TEST" configuration to the "nvimt" folder: `C:\Users\<you>\AppData\Local\nvimt`
2. Then run the "Neovim-neovide-TEST" MultiScript (F11) in the "Multi Commander".

```
These are my folders (stable and test):

C:\Users\<you>\AppData\Local\
nvim
nvim-data

nvimt
nvimt-data
```


***

### 2. I am now using these Multi Commander scripts

```MultiScript
F10
Neovim-neovide-STABLE
Command type: Multi-Script

@var $selectedFile = GetSelectedPaths();
@var $fileDir = PathGetPathPart($selectedFile, 1);

// @var $app = "neovide --neovim-bin=C:\\UTILS\\Neovim\\bin\\nvim";
// I have Neovim folder in Windows path: C:\UTILS\Neovim\bin\
@var $app = "neovide";

MC.Run CMD={$app} ARG={$selectedFile} STARTIN={$fileDir}

------------------------------
F11
Neovim-neovide-TEST
Command type: Multi-Script

@var $selectedFile = GetSelectedPaths();
@var $fileDir = PathGetPathPart($selectedFile, 1);

// MC.Run CMD="cmd.exe" ARG="/k set NVIM_APPNAME=nvimt&neovide "{$selectedFile} STARTIN={$fileDir}
// MC.Run CMD="cmd.exe" ARG="/c set NVIM_APPNAME=nvimt&neovide "{$selectedFile} STARTIN={$fileDir}

// start cmd shell, start neovide from cmd, and immediately close the cmd window
MC.Run CMD="cmd.exe" ARG="/c set NVIM_APPNAME=nvimt&&start neovide "{$selectedFile} STARTIN={$fileDir}

------------------------------
F12

Neovim-neovide-STABLE-without-file
Command type: Multi-Script

// STABLE configuration without an initial file

@var $selectedFile = GetSelectedPaths();
@var $fileDir = PathGetPathPart($selectedFile, 1);

// @var $app = "neovide --neovim-bin=C:\\UTILS\\Neovim\\bin\\nvim";
// I have Neovim folder in Windows path: C:\UTILS\Neovim\bin\
@var $app = "neovide";

MC.Run CMD={$app} STARTIN={$fileDir}

```

***

1. Windows CMD Shell How-to guides and examples
https://ss64.com/nt/syntax.html

2. START
https://ss64.com/nt/start.html

Try this:
1. Run Command Shell: cmd.exe
2. START "Demo 1" nvim
3. START neovide



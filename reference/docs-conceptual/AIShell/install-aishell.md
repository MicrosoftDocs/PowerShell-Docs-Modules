---
title: Install AI Shell
description: Learn how to install AI Shell on your system.
ms.date: 10/29/2024
ms.topic: install-set-up-deploy
---
# Install AI Shell

AI Shell is an interactive shell that provides a chat interface with language models. There are two
packages you need to install to have a complete AI Shell experience.

- The command-line shell (`aish`) interface
- The AI Shell module for PowerShell

This article explains how to install these packages on your system.


## System requirements

AI Shell is supported on the following platforms:

<!-- markdownlint-disable MD023 MD024 MD051 -->
### [Windows](#tab/windows)

- Windows 10 or higher
- PowerShell 7.4.6 or higher
- Windows Terminal

### [macOS](#tab/macos)

- macOS v13 Ventura or higher
- PowerShell 7.4.6 or higher
- iTerm2 (limited support)

### [Linux](#tab/linux)

- Ubuntu 20.04 or higher
- PowerShell 7.4 or higher (recommended)
- Any terminal emulator supported by the OS

  > [!NOTE]
  > The AI Shell module isn't supported on Linux.

<!-- markdownlint-enable MD023 MD024 MD051 -->

---

## Install AI Shell

For convenience we have provided a simple command to download and install script and run it. This script will download the necessary packages and add them to your PATH.

On windows this script will
- Install aish.exe to `$env:LOCALAPPDATA\Programs\AIShell`
- Install the AI Shell module to your module path location

Due to some limitations on macOS, the script will only install the `aish` executable to
/usr/local/AIShell. The AI Shell module will not be installed.

>!NOTE This script will only work on Windows and Mac systems. Linux users will need to follow the manual installation steps below.

```powershell
Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShell/AIShell/tools/scipts/installaishell.ps1')) 
```
<!-- markdownlint-disable MD023 MD024 MD051 -->
### [Windows](#tab/windows)

1. Download the latest version from the
   [GitHub releases page][03].
1. Install the AI Shell module from the PowerShell Gallery.

   ```powershell
   Install-PSResource -Name AIShell
   ```

### [macOS](#tab/macos)

1. Download the latest version from the
   [GitHub releases page][03].
1. Install the AI Shell module from the PowerShell Gallery.

   ```powershell
   Install-PSResource -Name AIShell
   ```

### [Linux](#tab/linux)

1. Download the latest version from the
   [GitHub releases page][03].

<!-- markdownlint-enable MD023 MD024 MD051 -->

---

## Next steps

- [Get started with AI Shell][02]
- [Get started with AI Shell for PowerShell][01]

<!-- link references -->
[01]: get-started/aishell-powershell.md
[02]: get-started/aishell-standalone.md
[03]: https://github.com/PowerShell/ProjectMercury/releases/latest

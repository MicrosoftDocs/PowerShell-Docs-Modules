---
description: Overview of the Crescendo module
ms.date: 03/07/2022
title: Crescendo overview
---
# Microsoft.PowerShell.Crescendo overview

PowerShell, like other shells, is capable of invoking command-line tools. However, it
would improve the experience if the command-line tool could participate in the PowerShell pipeline
and take advantage of the parameter behaviors that are part of PowerShell.

Crescendo provides a framework to rapidly create PowerShell cmdlets that _amplify_ command-line
tools, regardless of platform. The goal of a Crescendo-based module is to create PowerShell cmdlets
that use a command-line tool and, unlike that tool, return PowerShell objects instead of plain text.

## How Crescendo works

The Crescendo framework has two main components:

- A JSON configuration file that describes the cmdlets you want
- Output handler functions that parse the output from the command-line tool and return objects

The Crescendo module provides cmdlets to help you create the JSON configurations and build a module
containing the the cmdlets you defined. You must write your own output handler functions that return
PowerShell objects.

### Crescendo-specific terminology

The documentation for Crescendo includes some new terminology.

- **command-line tool** - a native executable file installed on your system
  - For example: `ipconfig.exe`
- **command** - what you type on the command line to invoke the executable, which may include
  specific parameters
  - For example: `ipconfig.exe /all`
- **amplified command** - the cmdlet you created with Crescendo to wrap a command in a PowerShell
  function
  - For example: `Get-IpConfig -All`

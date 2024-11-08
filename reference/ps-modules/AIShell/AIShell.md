---
Module Name: AIShell
Module Guid: ecb8bee0-59b9-4dae-9d7b-a990b480279a
Download Help Link:
Help Version: 0.1.0
ms.date: 10/29/2024
Locale: en-US
title: AIShell Module
---

# AIShell Module

## Description

The AIShell module integrates PowerShell with AIShell. This integration enables the sharing queries,
errors, and results between PowerShell and AIShell.

## AIShell Cmdlets

### [Invoke-AIShell](Invoke-AIShell.md)

Sends a query to the connected AIShell window. Results are shown in the AIShell window.

### [Resolve-Error](Resolve-Error.md)

Sends the last error in the current session  for resolution in the connected AIShell window.

### [Start-AIShell](Start-AIShell.md)

Starts an AIShell session in a split pane window of Windows Terminal and iTerm2 and connects a
communication channel to the PowerShell session that started it.

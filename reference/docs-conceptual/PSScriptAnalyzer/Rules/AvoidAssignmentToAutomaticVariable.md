---
description: Changing automatic variables might have undesired side effects
ms.date: 05/28/2026
ms.topic: reference
title: AvoidAssignmentToAutomaticVariable
---
# AvoidAssignmentToAutomaticVariable

**Severity Level: Warning**

## Description

PowerShell automatic variables are built-in variables that store runtime and execution state.
Several automatic variables are read-only, and PowerShell throws an error if you try to assign a
value to them. Assign other automatic variables only in advanced, intentional scenarios.

This rule helps you avoid conflicts with automatic variable names, which reduces hard-to-diagnose
bugs and keeps function behavior predictable.

To learn more about automatic variables, see `Get-Help about_Automatic_Variables`.

## How

Use variable names in functions or their parameters that do not conflict with automatic variables.

## Example

### Noncompliant

The variable `$Error` is an automatic variable that exists in the global scope and should therefore
never be used as a variable or parameter name.

```powershell
function foo($Error){ }
```

```powershell
function Get-CustomErrorMessage($ErrorMessage){ $Error = "Error occurred: $ErrorMessage" }
```

### Preferred

```powershell
function Get-CustomErrorMessage($ErrorMessage){ $FinalErrorMessage = "Error occurred: $ErrorMessage" }
```

---
description: Changing automatic variables might have undesired side effects
ms.date: 05/28/2026
ms.topic: reference
title: AvoidAssignmentToAutomaticVariable
---
# AvoidAssignmentToAutomaticVariable

**Severity Level: Warning**

## Description

PowerShell defines a set of automatic variables that store state information for and are created and
maintained by PowerShell. Even though you _can_ override many automatic variables, doing so can have
unexpected effects for users. Assign automatic variables only in advanced, intentional scenarios.

This rule helps you avoid conflicts with automatic variable names, which reduces hard-to-diagnose
bugs and keeps function behavior predictable.

Use variable names in functions or their parameters that don't conflict with automatic variables.

To learn more about automatic variables, see [about_Automatic_Variables][01].

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

<!-- Link reference definitions -->

[01]: /powershell/module/microsoft.powershell.core/about/about_automatic_variables

---
description: No Global Variables
ms.date: 05/28/2026
ms.topic: reference
title: AvoidGlobalVars
---
# AvoidGlobalVars

**Severity Level: Warning**

## Description

A variable is a unit of memory in which values are stored. PowerShell controls access to variables,
functions, aliases, and drives through a mechanism known as scoping. Variables and functions that
are present when PowerShell starts have been created in the global scope.

Globally scoped variables include:

- Automatic variables
- Preference variables
- Variables, aliases, and functions that are in your PowerShell profiles

Use local or script scope for variables instead of the global scope. To learn more, see
[about_Scopes][01].

## Example

### Noncompliant

```powershell
$Global:var1 = $null
function Test-NotGlobal ($var)
{
    $a = $var + $var1
}
```

### Compliant

```powershell
$var1 = $null
function Test-NotGlobal ($var1, $var2)
{
    $a = $var1 + $var2
}
```

<!-- link references -->

[01]: /powershell/module/microsoft.powershell.core/about/about_scopes

---
description: Avoid Using Positional Parameters
ms.date: 06/01/2026
ms.topic: reference
title: AvoidUsingPositionalParameters
---
# AvoidUsingPositionalParameters

**Severity Level: Information**

## Description

Using positional parameters reduces code readability and can introduce errors. It's possible
that a future version of the cmdlet could change in a way that'll break existing scripts if they
rely on parameter position.

For simple cmdlets with only a few positional parameters, the risk is much smaller. To prevent this
rule from being too noisy, it's only triggered when there are 3 or more parameters supplied. A
simple example where the risk of using positional parameters is negligible, is `Test-Path $Path`.

Use full parameter names when calling commands.

## Configure rule

```powershell
Rules = @{
    PSAvoidUsingPositionalParameters = @{
        CommandAllowList = 'Join-Path', 'MyCmdletOrScript'
        Enable = $true
    }
}
```

## Example

### Noncompliant

```powershell
Get-Command ChildItem Microsoft.PowerShell.Management
```

### Compliant

```powershell
Get-Command -Noun ChildItem -Module Microsoft.PowerShell.Management
```

## Parameters

### CommandAllowList: string[] (Default value is @()')

Commands or scripts to be excluded from this rule as a string. Default value is `@()`.

### Enable

Enables (`$true`) the rule during ScriptAnalyzer invocation. Default value is `$true`.

### Disable

Disables (`$false`) the rule during ScriptAnalyzer invocation.

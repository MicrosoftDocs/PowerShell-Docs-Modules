---
description: Avoid semicolons as line terminators
ms.date: 06/01/2026
ms.topic: reference
title: AvoidSemicolonsAsLineTerminators
---
# AvoidSemicolonsAsLineTerminators

**Severity Level: Warning**

## Description

Avoid using semicolons at the end of lines. In PowerShell, line-ending semicolons are redundant and
detract from code readability. Although semicolons serve as statement separators on a single line,
using them as line terminators is discouraged. This rule promotes cleaner, more maintainable code by
removing unnecessary semicolons. This rule isn't enabled by default.

## Example

### Noncompliant

```powershell
Install-Module -Name PSScriptAnalyzer; $a = 1 + $b;
```

```powershell
Install-Module -Name PSScriptAnalyzer;
$a = 1 + $b
```

### Compliant

```powershell
Install-Module -Name PSScriptAnalyzer; $a = 1 + $b
```

```powershell
Install-Module -Name PSScriptAnalyzer
$a = 1 + $b
```

## Configuration

```powershell
Rules = @{
    PSAvoidSemicolonsAsLineTerminators = @{
        Enable = $true
    }
}
```

## Parameters

### Enable

Enables (`$true`) the rule during ScriptAnalyzer invocation.

### Disable

Disables (`$false`) the rule during ScriptAnalyzer invocation. Default value is `$false`.

---
description: Use compatible syntax
ms.date: 06/09/2026
ms.topic: reference
title: UseCompatibleSyntax
---
# UseCompatibleSyntax

**Severity Level: Warning**

## Description

This rule detects syntax elements that aren't compatible with your specified PowerShell target
versions. When you run this rule from PowerShell 3 or 4, it can't detect syntax that's incompatible
with those versions because those versions can't parse newer syntax constructs.

## Example

### Noncompliant

The following example uses PowerShell 7 syntax. If `TargetVersions` includes `5.1` or earlier, this
rule flags these statements.

```powershell
$message = $IsReady ? 'Ready' : 'Not ready'
$displayName = $name ?? 'Unknown'
```

### Compliant

```powershell
if ($IsReady) {
    $message = 'Ready'
}
else {
    $message = 'Not ready'
}

if ($name -ne $null) {
    $displayName = $name
}
else {
    $displayName = 'Unknown'
}
```

## Configure rule

```powershell
@{
    Rules = @{
        PSUseCompatibleSyntax = @{
            Enable = $true
            TargetVersions = @(
                '6.0',
                '5.1',
                '4.0'
            )
        }
    }
}
```

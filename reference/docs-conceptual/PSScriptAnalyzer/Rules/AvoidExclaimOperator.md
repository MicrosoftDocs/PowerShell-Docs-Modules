---
description: Avoid exclaim operator
ms.date: 05/28/2026
ms.topic: reference
title: AvoidExclaimOperator
---
# AvoidExclaimOperator

**Severity Level: Warning**

## Description

This rule detects the use of the negation operator (`!`) and recommends using the `-not`
operator instead for improved readability and consistency with PowerShell conventions.

The `-not` operator is more explicit and aligns with PowerShell's verbose style, making code
easier to understand at a glance.

This rule is **disabled** by default. Enable it explicitly during ScriptAnalyzer invocation if
desired.

## Example

### Noncompliant

```powershell
$MyVar = !$true
```

### Compliant

```powershell
$MyVar = -not $true
```

## Configure rule

To enable this rule, run the following command:

```powershell
Rules = @{
    PSAvoidExclaimOperator  = @{
        Enable = $true
    }
}
```

## Parameters

### Enable

Enables (`$true`) the rule during ScriptAnalyzer invocation.

### Disable

Disables (`$false`) the rule during ScriptAnalyzer invocation. Default value is `$false`.

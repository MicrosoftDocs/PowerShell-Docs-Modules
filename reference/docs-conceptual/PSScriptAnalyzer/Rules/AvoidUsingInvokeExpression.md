---
description: Avoid Using Invoke-Expression
ms.date: 06/01/2026
ms.topic: reference
title: AvoidUsingInvokeExpression
---
# AvoidUsingInvokeExpression

**Severity Level: Warning**

## Description

You must be careful when using the `Invoke-Expression` command. It executes the specified string and
returns the results. Don't use `Invoke-Expression`.

Code injection can occur in your application or script if the expression passed as a string includes
user-provided data.

## Example

### Noncompliant

```powershell
Invoke-Expression 'Get-Process'
```

### Compliant

```powershell
Get-Process
```

---
description: Avoid Using Empty Catch Block
ms.date: 06/01/2026
ms.topic: reference
title: AvoidUsingEmptyCatchBlock
---
# AvoidUsingEmptyCatchBlock

**Severity Level: Warning**

## Description

Empty catch blocks aren't a good design choice because they can't handle errors that occur in a
`try` block. Add `Write-Error` or `throw` statements within the catch block to properly handle
exceptions.

## Example

### Noncompliant

```powershell
try
{
    1/0
}
catch [DivideByZeroException]
{
}
```

### Compliant

```powershell
try
{
    1/0
}
catch [DivideByZeroException]
{
    Write-Error 'DivideByZeroException'
}

try
{
    1/0
}
catch [DivideByZeroException]
{
    throw 'DivideByZeroException'
}
```

---
description: Use Cmdlet Correctly
ms.custom: PSSA v1.21.0
ms.date: 10/18/2021
ms.topic: reference
title: UseCmdletCorrectly
---
# UseCmdletCorrectly

**Severity Level: Warning**

## Description

Whenever we call a command, care should be taken that it is invoked with the correct syntax and
parameters.

## How

Specify all mandatory parameters when calling commands.

## Example

### Wrong

```powershell
Function Set-TodaysDate ()
{
    Set-Date
    ...
}
```

### Correct

```powershell
Function Set-TodaysDate ()
{
    $date = Get-Date
    Set-Date -Date $date
    ...
}
```

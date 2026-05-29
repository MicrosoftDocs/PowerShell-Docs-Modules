---
description: Avoid Default Value For Mandatory Parameter
ms.date: 05/28/2026
ms.topic: reference
title: AvoidDefaultValueForMandatoryParameter
---
# AvoidDefaultValueForMandatoryParameter

**Severity Level: Warning**

## Description

Mandatory parameters shouldn't have default values because there isn't a scenario where the default
can be used. PowerShell prompts for a value if the parameter value isn't specified when calling the
function.

## Example

### Noncompliant

```powershell
function Test
{

    [CmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$true)]
        $Parameter1 = 'default Value'
    )
}
```

### Preferred

```powershell
function Test
{
    [CmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$true)]
        $Parameter1
    )
}
```

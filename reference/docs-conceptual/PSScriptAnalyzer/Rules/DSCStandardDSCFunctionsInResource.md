---
description: Use standard DSC Get, Set, and Test TargetResource functions in a resource
ms.date: 06/03/2026
ms.topic: reference
title: DSCStandardDSCFunctionsInResource
---
# StandardDSCFunctionsInResource

**Severity Level: Error**

## Description

All Desired State Configuration (DSC) resources must implement the correct functions. Add the
missing functions to the resource.

For non-class based resources:

- `Get-TargetResource`
- `Set-TargetResource`
- `Test-TargetResource`

For class based resources:

- `Get`
- `Set`
- `Test`

## Example

### Noncompliant

```powershell
function Get-TargetResource
{
    [OutputType([Hashtable])]
    param
    (
        [parameter(Mandatory = $true)]
        [String]
        $Name
    )
    ...
}

function Test-TargetResource
{
    [OutputType([System.Boolean])]
    param
    (
        [parameter(Mandatory = $true)]
        [String]
        $Name
    )
    ...
}
```

### Compliant

```powershell
function Get-TargetResource
{
    [OutputType([Hashtable])]
    param
    (
        [parameter(Mandatory = $true)]
        [String]
        $Name
    )
    ...
}

function Set-TargetResource
{
    param
    (
        [parameter(Mandatory = $true)]
        [String]
        $Name
    )
    ...
}

function Test-TargetResource
{
    [OutputType([System.Boolean])]
    param
    (
        [parameter(Mandatory = $true)]
        [String]
        $Name
    )
    ...
}
```

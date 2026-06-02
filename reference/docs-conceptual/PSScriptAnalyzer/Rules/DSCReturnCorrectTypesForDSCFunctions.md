---
description: Return correct types for DSC functions
ms.date: 06/03/2026
ms.topic: reference
title: DSCReturnCorrectTypesForDSCFunctions
---
# ReturnCorrectTypesForDSCFunctions

**Severity Level: Information**

## Description

Functions in Desired State Configuration (DSC) resources have specific return objects. You'll need
to ensure that each function returns the correct type.

For non-class based resources:

- `Get-TargetResource` must return a hash table.
- `Set-TargetResource` must not return any value.
- `Test-TargetResource` must return a boolean.

For class based resources:

- `Get` must return an instance of the DSC class.
- `Set` must not return any value.
- `Test` must return a boolean.

## Example

### Noncompliant

```powershell
function Get-TargetResource
{
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

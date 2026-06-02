---
description: Use identical parameters for DSC Test and Set functions
ms.date: 06/03/2026
ms.topic: reference
title: DSCUseIdenticalParametersForDSC
---
# UseIdenticalParametersForDSC

**Severity Level: Error**

## Description

The `Get-TargetResource`, `Test-TargetResource`, and `Set-TargetResource` functions in a Desired
State Configuration (DSC) resource must all have identical parameters. If they don't match, you'll
need to update the function parameters to be consistent across all three functions.

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
        $Name,

        [String]
        $TargetResource
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

### Compliant

```powershell
function Get-TargetResource
{
    [OutputType([Hashtable])]
    param
    (
        [parameter(Mandatory = $true)]
        [String]
        $Name,

        [String]
        $TargetResource
    )
    ...
}

function Set-TargetResource
{
    param
    (
        [parameter(Mandatory = $true)]
        [String]
        $Name,

        [String]
        $TargetResource
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
        $Name,

        [String]
        $TargetResource
    )
    ...
}
```

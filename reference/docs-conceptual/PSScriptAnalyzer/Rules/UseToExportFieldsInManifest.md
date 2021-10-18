---
description: Use the *ToExport module manifest fields.
ms.custom: PSSA v1.20.0
ms.date: 10/18/2021
ms.topic: reference
title: UseToExportFieldsInManifest
---
# UseToExportFieldsInManifest

**Severity Level: Warning**

## Description

To improve the performance of module auto-discovery, module manifests should not use wildcards
(`'*'`) or null (`$null`) in the following entries:

- `AliasesToExport`
- `CmdletsToExport`
- `FunctionsToExport`
- `VariablesToExport`

Using wildcards or null has causes PowerShell to perform expensive work to analyze a module during
module auto-discovery.

## How

Use an explicit list in the entries.

## Example 1

Suppose there are no functions in your module to export. Then,

### Wrong

```powershell
FunctionsToExport = $null
```

### Correct

```powershell
FunctionToExport = @()
```

## Example 2

Suppose there are only two functions in your module, `Get-Foo` and `Set-Foo` that you want to
export. Then,

### Wrong

```powershell
FunctionsToExport = '*'
```

### Correct

```powershell
FunctionToExport = @(Get-Foo, Set-Foo)
```

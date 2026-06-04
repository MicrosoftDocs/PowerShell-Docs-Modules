---
description: Module manifest fields
ms.date: 06/04/2026
ms.topic: reference
title: MissingModuleManifestField
---
# MissingModuleManifestField

**Severity Level: Warning**

## Description

This rule detects when a module manifest's missing required fields. A module manifest is a `.psd1`
file that contains a hash table. The keys and values in the hash table describe the contents and
attributes of the module, define the prerequisites, and determine how the components are processed.

Module manifests must contain the following keys (and a corresponding value) to be considered valid:

- `ModuleVersion`

All other keys are optional and the order you place them don't matter.

## Example

### Noncompliant

```powershell
@{
    Author              = 'PowerShell Author'
    NestedModules       = @('.\mymodule.psm1')
    FunctionsToExport   = '*'
    CmdletsToExport     = '*'
    VariablesToExport   = '*'
}
```

### Compliant

```powershell
@{
    ModuleVersion       = '1.0'
    Author              = 'PowerShell Author'
    NestedModules       = @('.\mymodule.psm1')
    FunctionsToExport   = '*'
    CmdletsToExport     = '*'
    VariablesToExport   = '*'
}
```

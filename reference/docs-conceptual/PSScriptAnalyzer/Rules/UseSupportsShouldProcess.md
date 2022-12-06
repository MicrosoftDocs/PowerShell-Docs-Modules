---
description: Use SupportsShouldProcess
ms.custom: PSSA v1.21.0
ms.date: 12/06/2022
ms.topic: reference
title: UseSupportsShouldProcess
---
# UseSupportsShouldProcess

**Severity Level: Warning**

## Description

This rule discourages manual declaration of `WhatIf` and `Confirm` parameters in a function/cmdlet.
These parameters are, however, provided automatically when a function declares a `CmdletBinding`
attribute with `SupportsShouldProcess` as its named argument. Using `SupportsShouldProcess` not only
provides these parameters but also some generic functionality that allows the function/cmdlet
authors to provide the desired interactive experience while using the cmdlet.

## Example

### Wrong:

```powershell
function foo {
    param(
        $param1,
        $Confirm,
        $WhatIf
    )
}
```

### Correct:

```powershell
function foo {
    [CmdletBinding(SupportsShouldProcess)]
    param(
        $param1
    )
}
```

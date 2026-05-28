---
description: Switch Parameters Should Not Default To True
ms.date: 05/28/2026
ms.topic: reference
title: AvoidDefaultValueSwitchParameter
---
# AvoidDefaultValueSwitchParameter

**Severity Level: Warning**

## Description

If your parameter takes only `true` and `false`, define the parameter as type `[Switch]`. PowerShell
treats a switch parameter as `true` when it's used with a command. If the parameter isn't included
with the command, PowerShell considers the parameter to be false. Don't define `[Boolean]`
parameters.

Don't define a switch parameter with a default value of `$true` because a switch parameter is
already `$false` when it isn't specified. Leave the switch parameter without a default value so it
behaves like an ordinary on/off flag.

## Example

### Noncompliant

```powershell
function Test-Script
{
    [CmdletBinding()]
    Param
    (
        [String]
        $Param1,

        [switch]
        $Switch=$True
    )
    ...
}
```

### Preferred

```powershell
function Test-Script
{
    [CmdletBinding()]
    Param
    (
        [String]
        $Param1,

        [switch]
        $Switch
    )
    ...
}
```

<!-- link references -->

[01]: /powershell/scripting/developer/cmdlet/strongly-encouraged-development-guidelines#parameters-that-take-true-and-false

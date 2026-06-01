---
description: Avoid Using ShouldContinue Without Boolean Force Parameter
ms.date: 06/01/2026
ms.topic: reference
title: AvoidShouldContinueWithoutForce
---
# AvoidShouldContinueWithoutForce

**Severity Level: Warning**

## Description

Functions that use `ShouldContinue` should have a boolean `Force` parameter to allow users to bypass
the confirmation prompt. When using `ShouldContinue` in advanced functions, call it after the
`ShouldProcess` method returns `$true`.

To learn more, see [about_Functions_CmdletBindingAttribute][01] and
[about_Functions_Advanced_Methods][02].

## Example

### Noncompliant

```powershell
Function Test-ShouldContinue
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    Param
    (
        $MyString = 'blah'
    )

    if ($PsCmdlet.ShouldContinue('ShouldContinue Query', 'ShouldContinue Caption'))
    {
        ...
    }
}
```

### Compliant

```powershell
Function Test-ShouldContinue
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    Param
    (
        $MyString = 'blah',
        [Switch]$Force
    )

    if ($Force -or $PsCmdlet.ShouldContinue('ShouldContinue Query', 'ShouldContinue Caption'))
    {
        ...
    }
}
```

<!-- link references -->

[01]: /powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute
[02]: /powershell/module/microsoft.powershell.core/about/about_functions_advanced_methods

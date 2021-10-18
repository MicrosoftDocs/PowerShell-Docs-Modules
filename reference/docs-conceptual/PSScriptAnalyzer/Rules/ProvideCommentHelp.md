---
description: Basic Comment Help
ms.custom: PSSA v1.20.0
ms.date: 10/18/2021
ms.topic: reference
title: ProvideCommentHelp
---
# ProvideCommentHelp

**Severity Level: Info**

## Description

Comment based help should be provided for all PowerShell commands. This test only checks for the
presence of comment based help and not on the validity or format.

For assistance on comment based help, use the command `Get-Help about_comment_based_help` or the
following articles:

- [Writing Comment-based Help](https://docs.microsoft.com/powershell/scripting/developer/help/writing-comment-based-help-topics)
- [Writing Help for PowerShell Cmdlets](https://docs.microsoft.com/powershell/scripting/developer/help/writing-help-for-windows-powershell-cmdlets)
- [Create XML-based help using PlatyPS](https://docs.microsoft.com/powershell/scripting/dev-cross-plat/create-help-using-platyps)

## Configuration

```powershell
Rules = @{
    PSProvideCommentHelp = @{
        Enable = $true
        ExportedOnly = $false
        BlockComment = $true
        VSCodeSnippetCorrection = $false
        Placement = "before"
    }
}
```

### Parameters

#### Enable: bool (Default valus is `$true`)

Enable or disable the rule during ScriptAnalyzer invocation.

#### ExportedOnly: bool (Default value is `$true`)

If enabled, throw violation only on functions/cmdlets that are exported using the
`Export-ModuleMember` cmdlet.

#### BlockComment: bool (Default value is `$true`)

If enabled, returns comment help in block comment style, i.e., `<#...#>`. Otherwise returns comment
help in line comment style, i.e., each comment line starts with `#`.

#### VSCodeSnippetCorrection: bool (Default value is `$false`)

If enabled, returns comment help in vscode snippet format.

#### Placement: string (Default value is `before`)

Represents the position of comment help with respect to the function definition.

Possible values are: `before`, `begin` and `end`. If any invalid value is given, the property
defaults to `before`.

`before` means the help is placed before the function definition. `begin` means the help is placed
at the beginning of the function definition body. `end` means the help is places the end of the
function definition body.

## Example

### Wrong

```powershell
function Get-File
{
    [CmdletBinding()]
    Param
    (
        ...
    )

}
```

### Correct

```powershell
<#
.Synopsis
    Short description
.DESCRIPTION
    Long description
.EXAMPLE
    Example of how to use this cmdlet
.EXAMPLE
    Another example of how to use this cmdlet
.INPUTS
    Inputs to this cmdlet (if any)
.OUTPUTS
    Output from this cmdlet (if any)
.NOTES
    General notes
.COMPONENT
    The component this cmdlet belongs to
.ROLE
    The role this cmdlet belongs to
.FUNCTIONALITY
    The functionality that best describes this cmdlet
#>

function Get-File
{
    [CmdletBinding()]
    Param
    (
        ...
    )

}
```

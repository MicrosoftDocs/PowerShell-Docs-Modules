---
description: This article provides a basic guide for creating your own customized rules.
ms.date: 06/28/2023
title: Creating custom rules
---
# Creating custom rules

PSScriptAnalyzer uses the [Managed Extensibility Framework (MEF)][01] to import all rules defined in
the assembly. It can also consume rules written in PowerShell scripts.

When calling `Invoke-ScriptAnalyzer`, users can specify custom rules using the
**CustomizedRulePath** parameter.

This article provides a basic guide for creating your own customized rules.

## Basic requirements

### Functions should have comment-based help

Include the `.DESCRIPTION` field. This becomes the description for the customized rule.

```powershell
<#
.SYNOPSIS
    Name of your rule.
.DESCRIPTION
    This would be the description of your rule. Please refer to Rule Documentation
    for consistent rule messages.
.EXAMPLE
.INPUTS
.OUTPUTS
.NOTES
#>
```

### Output type should be **DiagnosticRecord**

```powershell
[OutputType([Microsoft.Windows.PowerShell.ScriptAnalyzer.Generic.DiagnosticRecord[]])]
```

### Each function must have a Token array or an Ast parameter

The name of the **Ast** parameter name must end with **Ast**.

```powershell
Param
(
    [Parameter(Mandatory = $true)]
    [ValidateNotNullOrEmpty()]
    [System.Management.Automation.Language.ScriptBlockAst]
    $testAst
)
```

The name of the **Token** parameter name must end with **Token**.

```powershell
Param
(
    [Parameter(Mandatory = $true)]
    [ValidateNotNullOrEmpty()]
    [System.Management.Automation.Language.Token[]]
    $testToken
)
```

### DiagnosticRecord should have the required properties

The **DiagnosticRecord** should have at least four properties:

- **Message**
- **Extent**
- **RuleName**
- **Severity**

```powershell
$result = [Microsoft.Windows.PowerShell.ScriptAnalyzer.Generic.DiagnosticRecord[]]@{
    "Message"  = "This is a sample rule"
    "Extent"   = $ast.Extent
    "RuleName" = $PSCmdlet.MyInvocation.InvocationName
    "Severity" = "Warning"
}
```

Since version 1.17.0, you can include a **SuggestedCorrections** property of type
**IEnumerable\<CorrectionExtent\>**. Make sure to specify the correct type. For example:

```powershell
[int]$startLineNumber =  $ast.Extent.StartLineNumber
[int]$endLineNumber = $ast.Extent.EndLineNumber
[int]$startColumnNumber = $ast.Extent.StartColumnNumber
[int]$endColumnNumber = $ast.Extent.EndColumnNumber
[string]$correction = 'Correct text that replaces Extent text'
[string]$file = $MyInvocation.MyCommand.Definition
[string]$optionalDescription = 'Useful but optional description text'
$objParams = @{
  TypeName = 'Microsoft.Windows.PowerShell.ScriptAnalyzer.Generic.CorrectionExtent'
  ArgumentList = $startLineNumber, $endLineNumber, $startColumnNumber,
                 $endColumnNumber, $correction, $optionalDescription
}
$correctionExtent = New-Object @objParams
$suggestedCorrections = New-Object System.Collections.ObjectModel.Collection[$($objParams.TypeName)]
$suggestedCorrections.add($correctionExtent) | Out-Null

[Microsoft.Windows.Powershell.ScriptAnalyzer.Generic.DiagnosticRecord]@{
    "Message"              = "This is a rule with a suggested correction"
    "Extent"               = $ast.Extent
    "RuleName"             = $PSCmdlet.MyInvocation.InvocationName
    "Severity"             = "Warning"
    "Severity"             = "Warning"
    "RuleSuppressionID"    = "MyRuleSuppressionID"
    "SuggestedCorrections" = $suggestedCorrections
}
```

### Make sure you export the function(s)

```powershell
Export-ModuleMember -Function (FunctionName)
```

## Example rule function

```powershell
<#
    .SYNOPSIS
    Uses #Requires -RunAsAdministrator instead of your own methods.
    .DESCRIPTION
    The #Requires statement prevents a script from running unless the Windows PowerShell
    version, modules, snap-ins, and module and snap-in version prerequisites are met.
    From Windows PowerShell 4.0, the #Requires statement let script developers require that
    sessions be run with elevated user rights (run as Administrator). Script developers does
    not need to write their own methods any more. To fix a violation of this rule, please
    consider using #Requires -RunAsAdministrator instead of your own methods.
    .EXAMPLE
    Measure-RequiresRunAsAdministrator -ScriptBlockAst $ScriptBlockAst
    .INPUTS
    [System.Management.Automation.Language.ScriptBlockAst]
    .OUTPUTS
    [Microsoft.Windows.PowerShell.ScriptAnalyzer.Generic.DiagnosticRecord[]]
    .NOTES
    None
#>
function Measure-RequiresRunAsAdministrator
{
    [CmdletBinding()]
    [OutputType([Microsoft.Windows.PowerShell.ScriptAnalyzer.Generic.DiagnosticRecord[]])]
    Param
    (
        [Parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [System.Management.Automation.Language.ScriptBlockAst]
        $ScriptBlockAst
    )

    Process
    {
        $results = @()
        try
        {
            #region Define predicates to find ASTs.
            # Finds specific method, IsInRole.
            [ScriptBlock]$predicate1 = {
                param ([System.Management.Automation.Language.Ast]$Ast)
                [bool]$returnValue = $false
                if ($Ast -is [System.Management.Automation.Language.MemberExpressionAst])
                {
                    [System.Management.Automation.Language.MemberExpressionAst]$meAst = $Ast
                    if ($meAst.Member -is [System.Management.Automation.Language.StringConstantExpressionAst])
                    {
                        [System.Management.Automation.Language.StringConstantExpressionAst]$sceAst = $meAst.Member
                        if ($sceAst.Value -eq 'isinrole')
                        {
                            $returnValue = $true
                        }
                    }
                }
                return $returnValue
            }

            # Finds specific value, [system.security.principal.windowsbuiltinrole]::administrator.
            [ScriptBlock]$predicate2 = {
                param ([System.Management.Automation.Language.Ast]$Ast)
                [bool]$returnValue = $false
                if ($Ast -is [System.Management.Automation.Language.AssignmentStatementAst])
                {
                    [System.Management.Automation.Language.AssignmentStatementAst]$asAst = $Ast
                    if ($asAst.Right.ToString() -eq '[system.security.principal.windowsbuiltinrole]::administrator')
                    {
                        $returnValue = $true
                    }
                }
                return $returnValue
            }
            #endregion
            #region Finds ASTs that match the predicates.

            [System.Management.Automation.Language.Ast[]]$methodAst     = $ScriptBlockAst.FindAll($predicate1, $true)
            [System.Management.Automation.Language.Ast[]]$assignmentAst = $ScriptBlockAst.FindAll($predicate2, $true)
            if ($null -ne $ScriptBlockAst.ScriptRequirements)
            {
                if ((!$ScriptBlockAst.ScriptRequirements.IsElevationRequired) -and
                ($methodAst.Count -ne 0) -and ($assignmentAst.Count -ne 0))
                {
                    $result = [Microsoft.Windows.PowerShell.ScriptAnalyzer.Generic.DiagnosticRecord]@{
                        'Message' = $Messages.MeasureRequiresRunAsAdministrator
                        'Extent' = $assignmentAst.Extent
                        'RuleName' = $PSCmdlet.MyInvocation.InvocationName
                        'Severity' = 'Information'
                    }
                    $results += $result
                }
            }
            else
            {
                if (($methodAst.Count -ne 0) -and ($assignmentAst.Count -ne 0))
                {
                    $result = [Microsoft.Windows.PowerShell.ScriptAnalyzer.Generic.DiagnosticRecord]@{
                        'Message' = $Messages.MeasureRequiresRunAsAdministrator
                        'Extent' = $assignmentAst.Extent
                        'RuleName' = $PSCmdlet.MyInvocation.InvocationName
                        'Severity' = 'Information'
                    }
                    $results += $result
                }
            }
            return $results
            #endregion
        }
        catch
        {
            $PSCmdlet.ThrowTerminatingError($PSItem)
        }
    }
}
```

More examples can be found in the [CommunityAnalyzerRules][02] folder on GitHub.

<!-- link references -->
[01]: /dotnet/framework/mef/
[02]: https://github.com/PowerShell/PSScriptAnalyzer/tree/master/Tests/Engine/CommunityAnalyzerRules

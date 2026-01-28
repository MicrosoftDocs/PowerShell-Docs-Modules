---
description: This article lists best-practice recommendations and the rules associated with them.
ms.date: 01/28/2026
title: PSScriptAnalyzer rules and recommendations
---
# PSScriptAnalyzer rules and recommendations

The following guidelines come from a combined effort from both the PowerShell team and the
community. The guidelines are organized by type. Within each type, there's a list of rules. The
rules are grouped by the **Severity** defined in the implementation of the **PSScriptAnalyzer**
rule. The severity level labeled `TBD` means "To be determined." Items labeled as TBD are
recommendations that don't currently have rules defined.

## Cmdlet Design Rules

### Severity: Error

No rules defined.

### Severity: Warning

- Use only Approved Verbs [UseApprovedVerbs][33]
- Cmdlets names with unusable characters [AvoidReservedCharInCmdlet][30]
- Parameter names that can't be used [AvoidReservedParams][31]
- Support confirmation requests [UseShouldProcessForStateChangingFunctions][37] and
  [UseSupportsShouldProcess][39]
- Must call **ShouldProcess** when the **ShouldProcess** attribute is present and vice versa
  [UseShouldProcess][32]
- Nouns should be singular [UseSingularNouns][38]
- Missing module manifest fields [MissingModuleManifestField][28]
  - **Version**
  - **Author**
  - **Description**
  - **LicenseUri** (for PowerShell Gallery)
- Switch parameters shouldn't default to true [AvoidDefaultValueSwitchParameter][10]

### Severity: Information

No rules defined.

### Severity: TBD

- Support **Force** parameter for interactive sessions. If your cmdlet is used interactively, always
  provide a **Force** parameter to override the interactive actions, such as prompts or reading
  lines of input. The **Force** parameter is important because it allows your cmdlet to be used in
  non-interactive scripts and hosts.
- Document output objects
- Module must be loadable
- No syntax errors
- Unresolved dependencies are an error
- Derive from the Cmdlet or PSCmdlet Classes
- Specify the Cmdlet Attribute
- Override an Input Processing Method
- Specify the OutputType Attribute
- Write single records to the pipeline
- Make cmdlets case-insensitive and case-preserving

## Script Functions

### Severity: Error

No rules defined.

### Severity: Warning

- Avoid using aliases [AvoidUsingCmdletAliases][12]
- Avoid using deprecated WMI cmdlets [AvoidUsingWMICmdlet][20]
- Avoid using empty **catch** blocks [AvoidUsingEmptyCatchBlock][15]
- Invoke existing cmdlets with correct parameters [UseCmdletCorrectly][34]
- Cmdlets should have **ShouldProcess**/**ShouldContinue** and **Force** parameter if using certain
  system-modifying verbs (Update, Set, Remove, New):
  [UseShouldProcessForStateChangingFunctions][37]
- Avoid using positional parameters [AvoidUsingPositionalParameters][18]
- Avoid using global variables [AvoidGlobalVars][11]
- Declared variables should be used after their assignment [UseDeclaredVarsMoreThanAssignments][35]
- Avoid using `Invoke-Expression` [AvoidUsingInvokeExpression][16]

### Severity: Information

No rules defined.

### Severity: TBD

- Avoid using `Clear-Host`
- Avoid using UNC file paths
- Error Handling
  - Use `-ErrorAction Stop` when calling cmdlets
  - Use `$ErrorActionPreference` set to  `Stop` or `Continue` when calling noncmdlets
  - Avoid using flags to handle errors
  - Avoid using `$?`
  - Avoid testing for a null variable as an error condition
  - Copy `$Error[0]` to your own variable
- Avoid using pipelines in scripts
- If a return type is declared, the cmdlet must return that type. If a type is returned, a return
  type must be declared.

## Scripting Style

### Severity: Error

No rules defined.

### Severity: Warning

- Avoid using `Write-Host` unless writing to the host is all you want to do
  [AvoidUsingWriteHost][21]

### Severity: Information

- Write comment-based help
  [ProvideCommentHelp][29]

### Severity: TBD

- Provide usage Examples
- Use the Notes section for details on how the tool works
- Every exported command should have help (including parameter documentation)
- Document the version of PowerShell that the script was written for
- Indent your code
- Avoid backticks

## Script Security

### Severity: Error

- Avoid using plain text passwords [AvoidUsingPlainTextForPassword][17]
- Avoid `-Username` and `-Password` parameters (use **PSCredential** instead):
  [UsePSCredentialType][36]
- Avoid hardcoding a `-ComputerName` parameter argument (information disclosure):
  [AvoidUsingComputerNameHardcoded][13]
- Avoid using `ConvertTo-SecureString` with plaintext (information disclosure):
  [AvoidUsingConvertToSecureStringWithPlainText][14]

### Severity: Warning

- Avoid using `$Password = 'string'` (information disclosure).
  [AvoidUsingUsernameAndPasswordParams][19]

### Severity: Information

No rules defined.

### Severity: TBD

- Avoid initializing API key and credential variables (information disclosure)

## DSC Related Rules

### Severity: Error

- Use standard DSC methods [StandardDSCFunctionsInResource][25]
- Use identical mandatory parameters for all DSC methods [UseIdenticalMandatoryParametersForDSC][26]
- Use identical parameters for Set and Test DSC methods [UseIdenticalParametersForDSC][27]

### Severity: Warning

No rules defined.

### Severity: Information

- The following three recommendations are covered by the [ReturnCorrectTypesForDSCFunctions][24]
  rule
  - Avoid returning any object from a `Set-TargetResource` or Set (Class Based) function
  - Return a Boolean value from a `Test-TargetResource` or Test (Class Based) function
  - Return an object from a `Get-TargetResource` or Get (Class Based) function
- DSC resources should have DSC tests [DSCTestsPresent][23]
- DSC resources should have DSC examples [DSCExamplesPresent][22]

### Severity: TBD

- For Windows PowerShell v4, resource modules should have a `.psd1` and  `schema.mof` file for every
  resource
- Resource modules should have a `.psd1` file (always) and `schema.mof` (for non-class resource) see
  [Issue #116][116]
- Resource module should have a DscResources folder that contains the resources - see
  [Issue #130][130]
- MOFs should have a description for each element - see [Issue #131][131]
- Use **ShouldProcess** for a **Set** DSC method

### References

- [Cmdlet Development Guidelines][01]
- [PowerShell DSC Resource Design and Testing Checklist][02]
- DSC Guidelines can also be found in the DSC Resources Repository
  - [DSC Resource Style Guidelines & Best Practices][06]
  - [DSC Resource Naming][05]
  - [Creating a High Quality DSC Resource Module][04]
- [The Unofficial PowerShell Best Practices and Style Guide][03]

<!-- link references -->
[01]: /powershell/scripting/developer/cmdlet/cmdlet-development-guidelines
[02]: https://devblogs.microsoft.com/powershell/powershell-dsc-resource-design-and-testing-checklist/
[03]: https://github.com/PoshCode/PowerShellPracticeAndStyle
[04]: https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md
[05]: https://github.com/PowerShell/DscResources/blob/master/Naming.md
[06]: https://github.com/PowerShell/DscResources/blob/master/StyleGuidelines.md
[10]: Rules/AvoidDefaultValueSwitchParameter.md
[11]: Rules/AvoidGlobalVars.md
[12]: Rules/AvoidUsingCmdletAliases.md
[13]: Rules/AvoidUsingComputerNameHardcoded.md
[14]: Rules/AvoidUsingConvertToSecureStringWithPlainText.md
[15]: Rules/AvoidUsingEmptyCatchBlock.md
[16]: Rules/AvoidUsingInvokeExpression.md
[17]: Rules/AvoidUsingPlainTextForPassword.md
[18]: Rules/AvoidUsingPositionalParameters.md
[19]: Rules/AvoidUsingUsernameAndPasswordParams.md
[20]: Rules/AvoidUsingWMICmdlet.md
[21]: Rules/AvoidUsingWriteHost.md
[22]: Rules/DSCDscExamplesPresent.md
[23]: Rules/DSCDscTestsPresent.md
[24]: Rules/DSCReturnCorrectTypesForDSCFunctions.md
[25]: Rules/DSCStandardDSCFunctionsInResource.md
[26]: Rules/DSCUseIdenticalMandatoryParametersForDSC.md
[27]: Rules/DSCUseIdenticalParametersForDSC.md
[28]: Rules/MissingModuleManifestField.md
[29]: Rules/ProvideCommentHelp.md
[30]: Rules/ReservedCmdletChar.md
[31]: Rules/ReservedParams.md
[32]: Rules/ShouldProcess.md
[33]: Rules/UseApprovedVerbs.md
[34]: Rules/UseCmdletCorrectly.md
[35]: Rules/UseDeclaredVarsMoreThanAssignments.md
[36]: Rules/UsePSCredentialType.md
[37]: Rules/UseShouldProcessForStateChangingFunctions.md
[38]: Rules/UseSingularNouns.md
[39]: Rules/UseSupportsShouldProcess.md
[116]: https://github.com/PowerShell/PSScriptAnalyzer/issues/116
[130]: https://github.com/PowerShell/PSScriptAnalyzer/issues/130
[131]: https://github.com/PowerShell/PSScriptAnalyzer/issues/131

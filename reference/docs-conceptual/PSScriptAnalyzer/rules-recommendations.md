---
description: This article lists best-practice recommendations and the rules associated with them.
ms.date: 03/22/2022
title: PSScriptAnalyzer rules and recommendations
---
# PSScriptAnalyzer rules and recommendations

The following guidelines come from a combined effort from both the PowerShell team and the
community. The guidelines are organized by type. Within each type there is a list of rules. The
rules are grouped by the **Severity** defined in the implementation of the **PSScriptAnalyzer**
rule. The severity level labeled as 'TBD' means "To be determined". These are recommendations that
do not currently have rules defined.

## Cmdlet Design Rules

### Severity: Error

No rules defined.

### Severity: Warning

- Use only Approved Verbs [UseApprovedVerbs](Rules/UseApprovedVerbs.md)
- Cmdlets names with unusable characters
  [AvoidReservedCharInCmdlet](Rules/ReservedCmdletChar.md)
- Parameter names that cannot be used
  [AvoidReservedParams](Rules/ReservedParams.md)
- Support confirmation requests
  [UseShouldProcessForStateChangingFunctions](Rules/UseShouldProcessForStateChangingFunctions.md)
  and
  [UseShouldProcessForStateChangingFunctions](Rules/UseShouldProcessForStateChangingFunctions.md)
- Must call **ShouldProcess** when the **ShouldProcess** attribute is present and vice
  versa [UseShouldProcess](Rules/ShouldProcess.md)
- Nouns should be singular
  [UseSingularNouns](Rules/UseSingularNouns.md)
- Missing module manifest fields
  [MissingModuleManifestField](Rules/MissingModuleManifestField.md)
  - **Version**
  - **Author**
  - **Description**
  - **LicenseUri** (for PowerShell Gallery)
- Switch parameters should not default to true
  [AvoidDefaultValueSwitchParameter](Rules/AvoidDefaultValueSwitchParameter.md)

### Severity: Information

No rules defined.

### Severity: TBD

- Support **Force** parameter for interactive sessions. If your cmdlet is used interactively, always
  provide a **Force** parameter to override the interactive actions, such as prompts or reading
  lines of input. This is important because it allows your cmdlet to be used in non-interactive
  scripts and hosts. The following methods can be implemented by an interactive host.
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

- Avoid using aliases
  [AvoidUsingCmdletAliases](Rules/AvoidUsingCmdletAliases.md)
- Avoid using deprecated WMI cmdlets
  [AvoidUsingWMICmdlet](Rules/AvoidUsingWMICmdlet.md)
- Avoid using empty **catch** blocks [AvoidUsingEmptyCatchBlock](Rules/AvoidUsingEmptyCatchBlock.md)
- Invoke existing cmdlets with correct parameters
  [UseCmdletCorrectly](Rules/UseCmdletCorrectly.md)
- Cmdlets should have **ShouldProcess**/**ShouldContinue** and **Force** parameter if using certain
  system-modifying verbs (Update, Set, Remove, New):
  [UseShouldProcessForStateChangingFunctions](Rules/UseShouldProcessForStateChangingFunctions.md)
- Avoid using positional parameters
  [AvoidUsingPositionalParameters](Rules/AvoidUsingPositionalParameters.md)
- Avoid using global variables
  [AvoidGlobalVars](Rules/AvoidGlobalVars.md)
- Declared variables should be used after their assignment
  [UseDeclaredVarsMoreThanAssignments](Rules/UseDeclaredVarsMoreThanAssignments.md)
- Avoid using `Invoke-Expression`
  [AvoidUsingInvokeExpression](Rules/AvoidUsingInvokeExpression.md)

### Severity: Information

No rules defined.

### Severity: TBD

- Avoid using `Clear-Host`
- Avoid using UNC file paths
- Error Handling
  - Use `-ErrorAction Stop` when calling cmdlets
  - Use `$ErrorActionPreference = 'Stop'/'Continue'` when calling non-cmdlets
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
  [AvoidUsingWriteHost](Rules/AvoidUsingWriteHost.md)

### Severity: Information

- Write comment-based help
  [ProvideCommentHelp](Rules/ProvideCommentHelp.md)

### Severity: TBD

- Provide usage Examples
- Use the Notes section for details on how the tool works
- Every exported command should have help (including parameter documentation)
- Document the version of PowerShell that the script was written for
- Indent your code
- Avoid backticks

## Script Security

### Severity: Error

- Avoid using plain text passwords
  [AvoidUsingPlainTextForPassword](Rules/AvoidUsingPlainTextForPassword.md)
- Avoid `-Username` and `-Password` parameters (use **PSCredential** instead):
  [UsePSCredentialType](Rules/UsePSCredentialType.md)
- Avoid hardcoding a `-ComputerName` parameter argument (information disclosure):
  [AvoidUsingComputerNameHardcoded](Rules/AvoidUsingComputerNameHardcoded.md)
- Avoid using `ConvertTo-SecureString` with plaintext (information disclosure):
  [AvoidUsingConvertToSecureStringWithPlainText](Rules/AvoidUsingConvertToSecureStringWithPlainText.md)

### Severity: Warning

- Avoid using `$Password = 'string'` (information disclosure).
  [AvoidUsingUsernameAndPasswordParams](Rules/AvoidUsingUsernameAndPasswordParams.md)

### Severity: Information

No rules defined.

### Severity: TBD

- Avoid initializing APIKey and Credentials variables (information disclosure)

## DSC Related Rules

### Severity: Error

- Use standard DSC methods
  [StandardDSCFunctionsInResource](Rules/DSCStandardDSCFunctionsInResource.md)
- Use identical mandatory parameters for all DSC methods
  [UseIdenticalMandatoryParametersForDSC](Rules/DSCUseIdenticalMandatoryParametersForDSC.md)
- Use identical parameters for Set and Test DSC methods
  [UseIdenticalParametersForDSC](Rules/DSCUseIdenticalParametersForDSC.md)

### Severity: Warning

No rules defined.

### Severity: Information

- The following three recommendations are covered by the
  [ReturnCorrectTypesForDSCFunctions](Rules/DSCReturnCorrectTypesForDSCFunctions.md) rule
  - Avoid returning any object from a `Set-TargetResource` or Set (Class Based) function
  - Return a Boolean value from a `Test-TargetResource` or Test (Class Based) function
  - Return an object from a `Get-TargetResource` or Get (Class Based) function
- DSC resources should have DSC tests [DSCTestsPresent](Rules/DSCDscTestsPresent.md)
- DSC resources should have DSC examples [DSCExamplesPresent](Rules/DSCDscExamplesPresent.md)

### Severity: TBD

- For Windows PowerShell v4, resource modules should have a `.psd1` file and `schema.mof` for every
  resource
- MOFs should have a description for each element - see
  [Issue #131](https://github.com/PowerShell/PSScriptAnalyzer/issues/131)
- Resource modules should have a `.psd1` file (always) and `schema.mof` (for non-class resource) see
  [Issue #116](https://github.com/PowerShell/PSScriptAnalyzer/issues/116)
- Use **ShouldProcess** for a **Set** DSC method
- Resource module contains DscResources folder which contains the resources - see
  [Issue #130](https://github.com/PowerShell/PSScriptAnalyzer/issues/130)

### References

- [Cmdlet Development Guidelines](/powershell/scripting/developer/cmdlet/cmdlet-development-guidelines)
- [PowerShell DSC Resource Design and Testing Checklist](https://devblogs.microsoft.com/powershell/powershell-dsc-resource-design-and-testing-checklist/)
- DSC Guidelines can also be found in the DSC Resources Repository
  - [DSC Resource Style Guidelines & Best Practices](https://github.com/PowerShell/DscResources/blob/master/StyleGuidelines.md)
  - [DSC Resource Naming](https://github.com/PowerShell/DscResources/blob/master/Naming.md)
  - [Creating a High Quality DSC Resource Module](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md)
- [The Unofficial PowerShell Best Practices and Style Guide](https://github.com/PoshCode/PowerShellPracticeAndStyle)

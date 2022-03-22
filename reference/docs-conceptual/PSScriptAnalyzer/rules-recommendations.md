---
description: This article lists best-practice recommendations and the rules associated with them.
ms.date: 03/22/2022
title: PSScriptAnalyzer rules and recommendations
---
# PSScriptAnalyzer rules and recommendations

The following guidelines come from a combined effort from both the PowerShell team and the
community. The guidelines are organized by type. Within each type there is a list of rules. The
rules are grouped by the **Severity** defined in the implementation of the **PSScriptAnalyzer** rule.
The severity level labeled as 'TBD' means "To be determined". These are recommendations that do not
currently have rules defined.

## Cmdlet Design Rules

### Severity: Error

No rules defined.

### Severity: Warning

- Use Only Approved Verbs [UseApprovedVerbs](Rules/UseApprovedVerbs.md)
- Cmdlets Names: Characters that cannot be Used
  [AvoidReservedCharInCmdlet](Rules/ReservedCmdletChar.md)
- Parameter Names that cannot be Used
  [AvoidReservedParams](Rules/ReservedParams.md)
- Support Confirmation Requests
  [UseShouldProcessForStateChangingFunctions](Rules/UseShouldProcessForStateChangingFunctions.md)
  and
  [UseShouldProcessForStateChangingFunctions](Rules/UseShouldProcessForStateChangingFunctions.md)
- Must call ShouldProcess when ShouldProcess attribute is present and vice
  versa.[UseShouldProcess](Rules/ShouldProcess.md)
- Nouns should be singular
  [UseSingularNouns](Rules/UseSingularNouns.md)
- Module Manifest Fields
  [MissingModuleManifestField](Rules/MissingModuleManifestField.md)
  - Version
  - Author
  - Description
  - LicenseUri (for PowerShell Gallery)
- Switch parameters should not default to true
  [AvoidDefaultValueSwitchParameter](Rules/AvoidDefaultValueSwitchParameter.md)

### Severity: Information

No rules defined.

### Severity: TBD

- Support Force Parameter for Interactive Session
- If your cmdlet is used interactively, always provide a Force parameter to override the interactive
  actions, such as prompts or reading lines of input). This is important because it allows your
  cmdlet to be used in non-interactive scripts and hosts. The following methods can be implemented
  by an interactive host.
- Document Output Objects
- Module must be loadable
- No syntax errors
- Unresolved dependencies are an error
- Derive from the Cmdlet or PSCmdlet Classes
- Specify the Cmdlet Attribute
- Override an Input Processing Method
- Specify the OutputType Attribute
- Write Single Records to the Pipeline
- Make Cmdlets Case-Insensitive and Case-Preserving

## Script Functions

### Severity: Error

No rules defined.

### Severity: Warning

- Avoid using alias
  [AvoidUsingCmdletAliases](Rules/AvoidUsingCmdletAliases.md)
- Avoid using deprecated WMI cmdlets
  [AvoidUsingWMICmdlet](Rules/AvoidUsingWMICmdlet.md)
- Empty catch block should not be used
  [AvoidUsingEmptyCatchBlock](Rules/AvoidUsingEmptyCatchBlock.md)
- Invoke existing cmdlet with correct parameters
  [UseCmdletCorrectly](Rules/UseCmdletCorrectly.md)
- Cmdlets should have ShouldProcess/ShouldContinue and Force param if certain system-modding verbs
  are present (Update, Set, Remove, New):
  [UseShouldProcessForStateChangingFunctions](Rules/UseShouldProcessForStateChangingFunctions.md)
- Positional parameters should be avoided
  [AvoidUsingPositionalParameters](Rules/AvoidUsingPositionalParameters.md)
- Global variables should be avoided.
  [AvoidGlobalVars](Rules/AvoidGlobalVars.md)
- Declared variables must be used in more than just their assignment.
  [UseDeclaredVarsMoreThanAssignments](Rules/UseDeclaredVarsMoreThanAssignments.md)
- No Invoke-Expression
  [AvoidUsingInvokeExpression](Rules/AvoidUsingInvokeExpression.md)

### Severity: Information

No rules defined.

### Severity: TBD

- `Clear-Host` should not be used
- File paths should not be used (UNC)
- Error Handling
  - Use `-ErrorAction Stop` when calling cmdlets
  - Use $ErrorActionPreference = 'Stop'/' Continue' when calling non-cmdlets
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

- Don't use `Write-Host` unless writing to the host is all you want to do
  [AvoidUsingWriteHost](Rules/AvoidUsingWriteHost.md)

### Severity: Information

- Write comment-based help
  [ProvideCommentHelp](Rules/ProvideCommentHelp.md)

### Severity: TBD

- Provide usage Examples
- Use the Notes section for details on how the tool works
- Should have help on every exported command (including parameter documentation)
- Document the version of PowerShell that the script was written for
- Indent your code
- Avoid backticks

## Script Security

### Severity: Error

- Password should be secure string
  [AvoidUsingPlainTextForPassword](Rules/AvoidUsingPlainTextForPassword.md)
- Should never have both `-Username` and `-Password` parameters (should take credentials):
  [UsePSCredentialType](Rules/UsePSCredentialType.md)
- `-ComputerName` Parameter argument hardcoded should not be used (information disclosure):
  [AvoidUsingComputerNameHardcoded](Rules/AvoidUsingComputerNameHardcoded.md)
- ConvertTo-SecureString with plaintext should not be used (information disclosure):
  [AvoidUsingConvertToSecureStringWithPlainText](Rules/AvoidUsingConvertToSecureStringWithPlainText.md)

### Severity: Warning

- Information disclosure - `$Password = 'string'` should not be used.
  [AvoidUsingUsernameAndPasswordParams](Rules/AvoidUsingUsernameAndPasswordParams.md)

### Severity: Information

No rules defined.

### Severity: TBD

- APIKey and Credentials variables that are initialized (information disclosure)

## DSC Related Rules

### Severity: Error

- Use standard DSC methods
  [StandardDSCFunctionsInResource](Rules/StandardDSCFunctionsInResource.md)
- Use identical mandatory parameters for all DSC methods
  [UseIdenticalMandatoryParametersForDSC](Rules/UseIdenticalMandatoryParametersForDSC.md)
- Use identical parameters for Set and Test DSC methods
  [UseIdenticalParametersForDSC](Rules/UseIdenticalParametersForDSC.md)

### Severity: Warning

No rules defined.

### Severity: Information

- The following three recommendations are covered by the
  [ReturnCorrectTypesForDSCFunctions](Rules/ReturnCorrectTypesForDSCFunctions.md) rule
  - Avoid returning any object from a `Set-TargetResource` or Set (Class Based) function
  - Returning a Boolean object from a `Test-TargetResource` or Test (Class Based) function
  - Returning an object from a `Get-TargetResource` or Get (Class Based) function
- DSC resources should have DSC tests [DSCTestsPresent](Rules/DscTestsPresent.md)
- DSC resources should have DSC examples [DSCExamplesPresent](Rules/DscExamplesPresent.md)

### Severity: TBD

- For PowerShell V4, Resource module contains `.psd1` file and `schema.mof` for every resource
- MOF has description for each element - see
  [Issue #131](https://github.com/PowerShell/PSScriptAnalyzer/issues/131)
- Resource module must contain .psd1 file (always) and schema.mof (for non-class resource) - see
  [Issue #116](https://github.com/PowerShell/PSScriptAnalyzer/issues/116)
- Use ShouldProcess for a Set DSC method
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

---
description: List of PSScriptAnalyzer rules
ms.date: 06/25/2026
ms.topic: reference
title: List of PSScriptAnalyzer rules
---
# PSScriptAnalyzer Rules

 The PSScriptAnalyzer module includes the following built-in rule definitions. For rules that
 support settings, you can enable or disable them by setting the `Enable` configuration property in
 a custom settings file. Rules listed as _Always enabled_ don't expose a per-rule `Enable` property.
 There are two ways to avoid using these rules:

- Create a custom rule configuration file to include only the rules you want or exclude the rules
  you don't want.
- Add the appropriate rule suppression attributes to your code to suppress the rule for specific
  code blocks. For more information, see the _Suppressing rules_ section of
  [Using PSScriptAnalyzer][01].

|                        Rule                        |  Severity   | Default state  | Configurable |
| -------------------------------------------------- | ----------- | :------------: | :----------: |
| [AlignAssignmentStatement][02]                     | Warning     |    Disabled    |     Yes      |
| [AvoidAssignmentToAutomaticVariable][03]           | Warning     | Always enabled |              |
| [AvoidDefaultValueForMandatoryParameter][04]       | Warning     | Always enabled |              |
| [AvoidDefaultValueSwitchParameter][05]             | Warning     | Always enabled |              |
| [AvoidExclaimOperator][06]                         | Warning     |    Disabled    |     Yes      |
| [AvoidGlobalAliases][07]                           | Warning     | Always enabled |              |
| [AvoidGlobalFunctions][08]                         | Warning     | Always enabled |              |
| [AvoidGlobalVars][09]                              | Warning     | Always enabled |              |
| [AvoidInvokingEmptyMembers][10]                    | Warning     | Always enabled |              |
| [AvoidLongLines][11]                               | Warning     |    Disabled    |     Yes      |
| [AvoidMultipleTypeAttributes][12]                  | Warning     | Always enabled |              |
| [AvoidNullOrEmptyHelpMessageAttribute][13]         | Warning     | Always enabled |              |
| [AvoidOverwritingBuiltInCmdlets][14]               | Warning     |    Enabled     |     Yes      |
| [AvoidReservedWordsAsFunctionNames][15]            | Warning     | Always enabled |              |
| [AvoidSemicolonsAsLineTerminators][16]             | Warning     |    Disabled    |     Yes      |
| [AvoidShouldContinueWithoutForce][17]              | Warning     | Always enabled |              |
| [AvoidTrailingWhitespace][18]                      | Warning     | Always enabled |              |
| [AvoidUsingAllowUnencryptedAuthentication][19]     | Warning     | Always enabled |              |
| [AvoidUsingBrokenHashAlgorithms][20]               | Warning     | Always enabled |              |
| [AvoidUsingCmdletAliases][21]                      | Warning     | Always enabled |     Yes      |
| [AvoidUsingComputerNameHardcoded][22]              | Error       | Always enabled |              |
| [AvoidUsingConvertToSecureStringWithPlainText][23] | Error       | Always enabled |              |
| [AvoidUsingDeprecatedManifestFields][24]           | Warning     | Always enabled |              |
| [AvoidUsingDoubleQuotesForConstantString][25]      | Information |    Disabled    |     Yes      |
| [AvoidUsingEmptyCatchBlock][26]                    | Warning     | Always enabled |              |
| [AvoidUsingInvokeExpression][27]                   | Warning     | Always enabled |              |
| [AvoidUsingPlainTextForPassword][28]               | Warning     | Always enabled |              |
| [AvoidUsingPositionalParameters][29]               | Warning     | Always enabled |              |
| [AvoidUsingUsernameAndPasswordParams][30]          | Error       | Always enabled |              |
| [AvoidUsingWMICmdlet][31]                          | Warning     | Always enabled |              |
| [AvoidUsingWriteHost][32]                          | Warning     | Always enabled |              |
| [DSCDscExamplesPresent][33]                        | Information | Always enabled |              |
| [DSCDscTestsPresent][34]                           | Information | Always enabled |              |
| [DSCReturnCorrectTypesForDSCFunctions][35]         | Information | Always enabled |              |
| [DSCStandardDSCFunctionsInResource][36]            | Error       | Always enabled |              |
| [DSCUseIdenticalMandatoryParametersForDSC][37]     | Error       | Always enabled |              |
| [DSCUseIdenticalParametersForDSC][38]              | Error       | Always enabled |              |
| [DSCUseVerboseMessageInDSCResource][39]            | Error       | Always enabled |              |
| [MisleadingBacktick][40]                           | Warning     | Always enabled |              |
| [MissingModuleManifestField][41]                   | Warning     | Always enabled |              |
| [PlaceCloseBrace][42]                              | Warning     |    Disabled    |     Yes      |
| [PlaceOpenBrace][43]                               | Warning     |    Disabled    |     Yes      |
| [PossibleIncorrectComparisonWithNull][44]          | Warning     | Always enabled |              |
| [PossibleIncorrectUsageOfAssignmentOperator][45]   | Warning     | Always enabled |              |
| [PossibleIncorrectUsageOfRedirectionOperator][46]  | Warning     | Always enabled |              |
| [ProvideCommentHelp][47]                           | Information |    Enabled     |     Yes      |
| [ReservedCmdletChar][48]                           | Error       | Always enabled |              |
| [ReservedParams][49]                               | Error       | Always enabled |              |
| [ReviewUnusedParameter][50]                        | Warning     | Always enabled |     Yes      |
| [ShouldProcess][51]                                | Warning     | Always enabled |              |
| [UseApprovedVerbs][52]                             | Warning     | Always enabled |              |
| [UseBOMForUnicodeEncodedFile][53]                  | Warning     | Always enabled |              |
| [UseCmdletCorrectly][54]                           | Warning     | Always enabled |              |
| [UseCompatibleCmdlets][55]                         | Warning     | Always enabled |     Yes      |
| [UseCompatibleCommands][56]                        | Warning     |    Disabled    |     Yes      |
| [UseCompatibleSyntax][57]                          | Warning     |    Disabled    |     Yes      |
| [UseCompatibleTypes][58]                           | Warning     |    Disabled    |     Yes      |
| [UseConsistentIndentation][59]                     | Warning     |    Disabled    |     Yes      |
| [UseConsistentParameterSetName][60]                | Warning     |    Disabled    |     Yes      |
| [UseConsistentParametersKind][61]                  | Warning     |    Disabled    |     Yes      |
| [UseConsistentWhitespace][62]                      | Warning     |    Disabled    |     Yes      |
| [UseConstrainedLanguageMode][63]                   | Warning     |    Disabled    |     Yes      |
| [UseCorrectCasing][64]                             | Information |    Disabled    |     Yes      |
| [UseDeclaredVarsMoreThanAssignments][65]           | Warning     | Always enabled |              |
| [UseLiteralInitializerForHashtable][66]            | Warning     | Always enabled |              |
| [UseOutputTypeCorrectly][67]                       | Information | Always enabled |              |
| [UseProcessBlockForPipelineCommand][68]            | Warning     | Always enabled |              |
| [UsePSCredentialType][69]                          | Warning     | Always enabled |              |
| [UseShouldProcessForStateChangingFunctions][70]    | Warning     | Always enabled |              |
| [UseSingleValueFromPipelineParameter][71]          | Warning     |    Disabled    |     Yes      |
| [UseSingularNouns][72]                             | Warning     |    Enabled     |     Yes      |
| [UseSupportsShouldProcess][73]                     | Warning     | Always enabled |              |
| [UseToExportFieldsInManifest][74]                  | Warning     | Always enabled |              |
| [UseUsingScopeModifierInNewRunspaces][75]          | Warning     | Always enabled |              |
| [UseUTF8EncodingForHelpFile][76]                   | Warning     | Always enabled |              |

<!-- link references -->
[01]: ../using-scriptanalyzer.md#suppressing-rules
[02]: AlignAssignmentStatement.md
[03]: AvoidAssignmentToAutomaticVariable.md
[04]: AvoidDefaultValueForMandatoryParameter.md
[05]: AvoidDefaultValueSwitchParameter.md
[06]: AvoidExclaimOperator.md
[07]: AvoidGlobalAliases.md
[08]: AvoidGlobalFunctions.md
[09]: AvoidGlobalVars.md
[10]: AvoidInvokingEmptyMembers.md
[11]: AvoidLongLines.md
[12]: AvoidMultipleTypeAttributes.md
[13]: AvoidNullOrEmptyHelpMessageAttribute.md
[14]: AvoidOverwritingBuiltInCmdlets.md
[15]: AvoidReservedWordsAsFunctionNames.md
[16]: AvoidSemicolonsAsLineTerminators.md
[17]: AvoidShouldContinueWithoutForce.md
[18]: AvoidTrailingWhitespace.md
[19]: AvoidUsingAllowUnencryptedAuthentication.md
[20]: AvoidUsingBrokenHashAlgorithms.md
[21]: AvoidUsingCmdletAliases.md
[22]: AvoidUsingComputerNameHardcoded.md
[23]: AvoidUsingConvertToSecureStringWithPlainText.md
[24]: AvoidUsingDeprecatedManifestFields.md
[25]: AvoidUsingDoubleQuotesForConstantString.md
[26]: AvoidUsingEmptyCatchBlock.md
[27]: AvoidUsingInvokeExpression.md
[28]: AvoidUsingPlainTextForPassword.md
[29]: AvoidUsingPositionalParameters.md
[30]: AvoidUsingUsernameAndPasswordParams.md
[31]: AvoidUsingWMICmdlet.md
[32]: AvoidUsingWriteHost.md
[33]: DSCDscExamplesPresent.md
[34]: DSCDscTestsPresent.md
[35]: DSCReturnCorrectTypesForDSCFunctions.md
[36]: DSCStandardDSCFunctionsInResource.md
[37]: DSCUseIdenticalMandatoryParametersForDSC.md
[38]: DSCUseIdenticalParametersForDSC.md
[39]: DSCUseVerboseMessageInDSCResource.md
[40]: MisleadingBacktick.md
[41]: MissingModuleManifestField.md
[42]: PlaceCloseBrace.md
[43]: PlaceOpenBrace.md
[44]: PossibleIncorrectComparisonWithNull.md
[45]: PossibleIncorrectUsageOfAssignmentOperator.md
[46]: PossibleIncorrectUsageOfRedirectionOperator.md
[47]: ProvideCommentHelp.md
[48]: ReservedCmdletChar.md
[49]: ReservedParams.md
[50]: ReviewUnusedParameter.md
[51]: ShouldProcess.md
[52]: UseApprovedVerbs.md
[53]: UseBOMForUnicodeEncodedFile.md
[54]: UseCmdletCorrectly.md
[55]: UseCompatibleCmdlets.md
[56]: UseCompatibleCommands.md
[57]: UseCompatibleSyntax.md
[58]: UseCompatibleTypes.md
[59]: UseConsistentIndentation.md
[60]: UseConsistentParameterSetName.md
[61]: UseConsistentParametersKind.md
[62]: UseConsistentWhitespace.md
[63]: UseConstrainedLanguageMode.md
[64]: UseCorrectCasing.md
[65]: UseDeclaredVarsMoreThanAssignments.md
[66]: UseLiteralInitializerForHashtable.md
[67]: UseOutputTypeCorrectly.md
[68]: UseProcessBlockForPipelineCommand.md
[69]: UsePSCredentialType.md
[70]: UseShouldProcessForStateChangingFunctions.md
[71]: UseSingleValueFromPipelineParameter.md
[72]: UseSingularNouns.md
[73]: UseSupportsShouldProcess.md
[74]: UseToExportFieldsInManifest.md
[75]: UseUsingScopeModifierInNewRunspaces.md
[76]: UseUTF8EncodingForHelpFile.md

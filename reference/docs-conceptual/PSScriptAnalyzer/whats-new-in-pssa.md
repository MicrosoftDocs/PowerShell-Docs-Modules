---
description: This article lists the updates to the PSScriptAnalyzer module.
ms.date: 04/29/2025
title: What's new in PSScriptAnalyzer
---
# What's new in PSScriptAnalyzer

PSScriptAnalyzer is a static code checker for PowerShell modules and scripts. This article outlines
the important changes in PSScriptAnalyzer. For a full list of changes, see the PSScriptAnalyzer
[CHANGELOG][01].

## PSScriptAnalyzer 1.24.0 - 2025-03-18

Breaking changes

- Minimum required PowerShell version raised from 3 to 5.1

New features and updates

- Add new options (enabled by default) to formatting rule `UseCorrectCasing` to also correct
  operators, keywords and commands
- `PSAlignAssignmentStatement`: Ignore hashtables with a single key-value pair
- Use `RequiredResource` hashtable to specify PowerShell module versions
- `PSAvoidAssignmentToAutomaticVariable`: Ignore when a Parameter has an Attribute that contains a
  Variable expression
- Trim unnecessary trailing spaces from string resources in Strings.resx
- Make Settings type detection more robust
- Add foreach Assignment to `AvoidAssignmentToAutomaticVariable`
- Do not print summary repeatedly for each logger
- Set exit code of `Invoke-ScriptAnalyzer -EnableExit` to total number of diagnostics
- `Invoke-ScriptAnalyzer`: Stream diagnostics instead of batching
- `Invoke-ScriptAnalyzer`: Print summary only once per invocation
- `Invoke-ScriptAnalyzer`: Include parse errors in reported error count

## PSScriptAnalyzer 1.23.0 - 2024-10-09

Small maintenance release to update the build pipeline and fix two issues:

- Fix property name in type definition XML
- Update `PSUseConsistentWhitespace` to handle redirect operators that aren't in stream order

## PSScriptAnalyzer 1.22.0 - 2024-03-05

PSScriptAnalyzer works with Windows PowerShell 5.1 and PowerShell 7. The minimum required version
when using PowerShell 7 is now `7.2.11`.

### New rules

- `PSAvoidUsingAllowUnencryptedAuthentication` rule to warn about outdated authentication methods.
- `PSAvoidExclaimOperator` rule to warn about the use of the `!` negation operator.

### Enhancements

- Enable suppression of `PSAvoidAssignmentToAutomaticVariable` for specific variable or parameter
- Upgrade to use .NET 6 since PowerShell 7.0 is now out out of support
- Convert `PSUseSingularNouns` to configurable rule and add `Windows` to allowlist
- Allow suppression of `PSUseSingularNouns` for specific function
- Add `ErrorView` to `SpecialVars.cs`
- Adding `ToString()` methods to `[CorrectionExtent]` and `[DiagnosticRecord]` types
- Add `PSNativeCommandUseErrorActionPreference` preference variable
- `AvoidUsingPositionalParameter` - Check if command has parameters to avoid having `az` in default
  **CommandAllowList**
- `PSReviewUnusedParameter` - Add **CommandsToTraverse** option

## PSScriptAnalyzer 1.21.0 - 2022-09-27

### New Rule

- Add `AvoidMultipleTypeAttributes` rule to warn about multiple type attributes on a parameter.
- Add `AvoidSemicolonsAsLineTerminators` rule to warn about lines ending with a semicolon.
- Add `AvoidUsingBrokenHashAlgorithms` rule to warn about the use of insecure hash algorithms.

### Enhancements

- Return suggestion to use **PSCredential** for `AvoidUsingPlainTextForPassword` rule
- `Invoke-Formatter` - Accept input from pipeline
- Make messages of `UseCorrectCasing` more detailed
- Exclude automatic variable `$FormatEnumerationLimit` from analysis by `PSAvoidGlobalVars` and
  `PSUseDeclaredVarsMoreThanAssignments`
- `PSAvoidUsingPositionalParameters` - Do not warn on AZ CLI

## PSScriptAnalyzer 1.20.0 - 2021-08-20

### New rules

- Make `UseSingularNouns` rule work in PowerShell 7
- `UseConsistentWhitespace` - Create option to ignore assignment operator inside hashtable

### Enhancements

- Replace unhelpful warning about `process` aliasing `Get-Process` with warning about misused syntax
- Fix `FunctionInfo` fallback AST attribute analysis for `UseShouldProcessCorrectly`
- Do not increase indentation after a left parenthesis if the previous token is a newline and the
  next token is not a newline
- `UseConsistentWhitespace` - **CheckOpenBrace** setting to not warn when being preceded by open
  parenthesis
- Implement `-IncludeSuppressions` parameter
- Combine multiple suppressions applied to the same diagnostic

## PSScriptAnalyzer 1.19.1 - 2020-07-28

### New rules

- Add `AvoidUsingDoubleQuotesForConstantString` (disabled by default) to warn about the use of
  double quotes for constant strings

### Fixes

- `UseCorrectCasing` - Do not use **CommandInfoCache** when **CommandInfoParameters** property
  throws due to runspace affinity problem of PowerShell engine
- `ReviewUnusedParameter` - Do not trigger when `$MyInvocation.BoundParameters` or
  `$PSCmdlet.MyInvocation.BoundParameters` is used
- `PipelineIndentationStyle.None` - Fix bug that caused incorrect formatting in hashtables
- `UseUsingScopeModifierInNewRunspaces` - Fix `ArgumentException` when the same variable name is
  used in 2 different sessions.
- `UseConsistentWhitespace`
  - Check previous token only if it starts on the same line
  - Fix **CheckParameter** bug when using interpolated string

## Previous versions

For information about the changes in previous versions of PSScriptAnalyzer, see the PSScriptAnalyzer
[CHANGELOG][01].

<!-- link references -->
[01]: https://github.com/PowerShell/PSScriptAnalyzer/blob/master/CHANGELOG.MD

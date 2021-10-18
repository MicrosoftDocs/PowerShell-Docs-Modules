# PSScriptAnalyzer

PSScriptAnalyzer is a static code checker for PowerShell modules and scripts. PSScriptAnalyzer
checks the quality of PowerShell code by running a set of rules. The rules are based on PowerShell
best practices identified by PowerShell Team and the community. It generates **DiagnosticResults**
(errors and warnings) to inform users about potential code defects and suggests possible solutions
for improvements.

PSScriptAnalyzer is shipped with a collection of built-in rules that checks various aspects of
PowerShell code such as presence of uninitialized variables, usage of **PSCredential** type, usage
of `Invoke-Expression`, and many more. Additional functionalities such as the option to exclude or
include specific rules are also supported.

## Supported PowerShell Versions and Platforms

- Windows PowerShell 3.0 or greater
- PowerShell Core 7.0.3 or greater on Windows/Linux/macOS

## Parser Errors

In prior versions of ScriptAnalyzer, errors found during parsing were reported as errors and
diagnostic records were not created. ScriptAnalyzer now emits parser errors as diagnostic records in
the output stream with other diagnostic records.

```powershell
PS> Invoke-ScriptAnalyzer -ScriptDefinition '"b" = "b"; function eliminate-file () { }'

RuleName            Severity   ScriptName Line Message
--------            --------   ---------- ---- -------
InvalidLeftHandSide ParseError            1    The assignment expression is not
                                               valid. The input to an
                                               assignment operator must be an
                                               object that is able to accept
                                               assignments, such as a variable
                                               or a property.
PSUseApprovedVerbs  Warning               1    The cmdlet 'eliminate-file' uses an
                                               unapproved verb.
```

The RuleName is set to the `ErrorId` of the parser error.

To suppress **ParseErrors**, do not include it as a value in the `-Severity` parameter.

```powershell
PS> Invoke-ScriptAnalyzer -ScriptDefinition '"b" = "b"; function eliminate-file () { }' -Severity Warning

RuleName           Severity ScriptName Line Message
--------           -------- ---------- ---- -------
PSUseApprovedVerbs Warning             1    The cmdlet 'eliminate-file' uses an
                                            unapproved verb.
```

## Suppressing Rules

You can suppress a rule by decorating a script/function or script/function parameter with .NET's
[SuppressMessageAttribute](/dotnet/api/system.diagnostics.codeanalysis.suppressmessageattribute).
The constructor for `SuppressMessageAttribute` takes two parameters: a category and a check ID. Set
the `categoryID` parameter to the name of the rule you want to suppress and set the `checkID`
parameter to a null or empty string. You can optionally add a third named parameter with a
justification for suppressing the message:

```powershell
function SuppressMe()
{
    [Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSProvideCommentHelp', '', Justification='Just an example')]
    param()

    Write-Verbose -Message "I'm making a difference!"

}
```

All rule violations within the scope of the script/function/parameter you decorate will be
suppressed.

To suppress a message on a specific parameter, set the `SuppressMessageAttribute`'s `CheckId`
parameter to the name of the parameter:

```powershell
function SuppressTwoVariables()
{
    [Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSProvideDefaultParameterValue', 'b')]
    [Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSProvideDefaultParameterValue', 'a')]
    param([string]$a, [int]$b)
    {
    }
}
```

Use the `SuppressMessageAttribute`'s `Scope` property to limit rule suppression to functions or
classes within the attribute's scope.

Use the value `Function` to suppress violations on all functions within the attribute's scope. Use
the value `Class` to suppress violations on all classes within the attribute's scope:

```powershell
[Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSProvideCommentHelp', '', Scope='Function')]
param(
)

function InternalFunction
{
    param()

    Write-Verbose -Message "I am invincible!"
}
```

You can further restrict suppression based on a function/parameter/class/variable/object's name by
setting the `SuppressMessageAttribute's` `Target` property to a regular expression or a glob
pattern. Few examples are given below.

Suppress `PSAvoidUsingWriteHost` rule violation in `start-bar` and `start-baz` but not in
`start-foo` and `start-bam`:

```powershell
[System.Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSAvoidUsingWriteHost', '', Scope='Function', Target='start-ba[rz]')]
param()
function start-foo {
    write-host "start-foo"
}

function start-bar {
    write-host "start-bar"
}

function start-baz {
    write-host "start-baz"
}

function start-bam {
    write-host "start-bam"
}
```

Suppress violations in all the functions:

```powershell
[Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSAvoidUsingWriteHost', '', Scope='Function', Target='*')]
Param()
```

Suppress violation in `start-bar`, `start-baz` and `start-bam` but not in `start-foo`:

```powershell
[Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSAvoidUsingWriteHost', '', Scope='Function', Target='start-b*')]
Param()
```

**Note**: Parser Errors cannot be suppressed via the `SuppressMessageAttribute`

## Settings Support in ScriptAnalyzer

Settings that describe ScriptAnalyzer rules to include/exclude based on `Severity` can be created
and supplied to `Invoke-ScriptAnalyzer` using the `Setting` parameter. This enables a user to create
a custom configuration for a specific environment. We support the following modes for specifying the
settings file.

## Using parameter Settings

### Built-in Presets

ScriptAnalyzer ships a set of built-in presets that can be used to analyze scripts. For example, if
the user wants to run _PowerShell Gallery_ rules on their module, then they use the following
command.

```powershell
Invoke-ScriptAnalyzer -Path /path/to/module/ -Settings PSGallery -Recurse
```

Along with `PSGallery` there are a few other built-in presets, including, `DSC` and
`CodeFormatting`, that can be used. These presets can be tab completed for the `Settings` parameter.

### Explicit

The following example excludes two rules from the default set of rules and any rule that does not
output an Error or Warning diagnostic record.

```powershell
# PSScriptAnalyzerSettings.psd1
@{
    Severity=@('Error','Warning')
    ExcludeRules=@('PSAvoidUsingCmdletAliases',
                'PSAvoidUsingWriteHost')
}
```

Then invoke that settings file when using `Invoke-ScriptAnalyzer`:

```powershell
Invoke-ScriptAnalyzer -Path MyScript.ps1 -Settings PSScriptAnalyzerSettings.psd1
```

The next example selects a few rules to execute instead of all the default rules.

```powershell
# PSScriptAnalyzerSettings.psd1
@{
    IncludeRules=@('PSAvoidUsingPlainTextForPassword',
                'PSAvoidUsingConvertToSecureStringWithPlainText')
}
```

Then invoke that settings file:

```powershell
Invoke-ScriptAnalyzer -Path MyScript.ps1 -Settings PSScriptAnalyzerSettings.psd1
```

### Implicit

If you place a settings file named `PSScriptAnalyzerSettings.psd1` in your project root,
PSScriptAnalyzer discovers it when you pass the project root as the `Path` parameter.

```powershell
Invoke-ScriptAnalyzer -Path "C:\path\to\project" -Recurse
```

Note that providing settings explicitly takes higher precedence over this implicit mode. Sample
settings files are provided in the
[Settings folder](https://github.com/PowerShell/PSScriptAnalyzer/tree/master/Engine/Settings) of the
GitHub repository.

## Custom rules

It is possible to provide one or more paths to custom rules in the settings file. It is important
that these paths either point to a module's folder (implicitly uses the module manifest) or to the
module's script file (.psm1). The module should export the custom rules (as functions) for them to
be available to PS Script Analyzer.

In this example the property `CustomRulePath` points to two different modules. Both modules export
the rules (the functions) with the verb `Measure` so that is used for the property `IncludeRules`.

```powershell
@{
    CustomRulePath      = @(
        '.\output\RequiredModules\DscResource.AnalyzerRules'
        '.\tests\QA\AnalyzerRules\SqlServerDsc.AnalyzerRules.psm1'
    )

    IncludeRules        = @(
        'Measure-*'
    )
}
```

You can also add default rules by listing the rules in the `IncludeRules` property. When including
default rules is important that the property `IncludeDefaultRules` is set to `$true`, otherwise the
default rules will not be used.

```powershell
@{
    CustomRulePath      = @(
        '.\output\RequiredModules\DscResource.AnalyzerRules'
        '.\tests\QA\AnalyzerRules\SqlServerDsc.AnalyzerRules.psm1'
    )

    IncludeDefaultRules = $true

    IncludeRules        = @(
        # Default rules
        'PSAvoidDefaultValueForMandatoryParameter'
        'PSAvoidDefaultValueSwitchParameter'

        # Custom rules
        'Measure-*'
    )
}
```

### Using custom rules in Visual Studio Code

It is also possible to use the custom rules that are provided in the settings file in Visual Studio
Code. This is done by adding a Visual Studio Code workspace settings file (`.vscode/settings.json`).

```json
{
    "powershell.scriptAnalysis.settingsPath": ".vscode\\analyzersettings.psd1",
    "powershell.scriptAnalysis.enable": true,
}
```

[Back to ToC](#table-of-contents)

## ScriptAnalyzer as a .NET library

ScriptAnalyzer engine and functionality can now be directly consumed as a library.

Here are the public interfaces:

```csharp
using Microsoft.Windows.PowerShell.ScriptAnalyzer;

public void Initialize(System.Management.Automation.Runspaces.Runspace runspace,
Microsoft.Windows.PowerShell.ScriptAnalyzer.IOutputWriter outputWriter,
[string[] customizedRulePath = null],
[string[] includeRuleNames = null],
[string[] excludeRuleNames = null],
[string[] severity = null],
[bool suppressedOnly = false],
[string profile = null])

public System.Collections.Generic.IEnumerable<DiagnosticRecord> AnalyzePath(string path,
    [bool searchRecursively = false])

public System.Collections.Generic.IEnumerable<IRule> GetRule(string[] moduleNames, string[] ruleNames)
```

## Violation Correction

Some violations can be fixed by replacing the violation causing content with a suggested
alternative. You can use the `-Fix` switch to automatically apply the suggestions. Since
`Invoke-ScriptAnalyzer` implements `SupportsShouldProcess`, you can additionally use `-WhatIf` or
`-Confirm` to find out which corrections would be applied. Be sure to use source control when
applying those corrections since some changes, such as the one for `AvoidUsingPlainTextForPassword`,
might require additional script modifications that cannot be made automatically. If your scripts are
sensitive to encoding, you should also check for that because the initial encoding can not be
preserved in all cases.

The initial motivation behind having the `SuggestedCorrections` property on the `ErrorRecord` (which
is how the `-Fix` parameter works under the hood) was to enable quick-fix like scenarios in editors
like VSCode, Sublime, etc. At present, we provide valid `SuggestedCorrection` only for the following
rules, while gradually adding this feature to more rules.

- AvoidAlias.cs
- AvoidUsingPlainTextForPassword.cs
- MisleadingBacktick.cs
- MissingModuleManifestField.cs
- UseToExportFieldsInManifest.cs

## Contributions are welcome

There are many ways to contribute:

1. Open a new bug report, feature request or just ask a question by opening a new issue in
   [GitHub](https://github.com/PowerShell/PSScriptAnalyzer/issues/new/choose).
1. Participate in the discussions of
   [issues](https://github.com/PowerShell/PSScriptAnalyzer/issues),
   [pull requests](https://github.com/PowerShell/PSScriptAnalyzer/pulls), and test fixes and
   new features.
1. Submit your own fixes or features as a pull request but please discuss it beforehand in an issue
   if the change is substantial.
1. Submit test cases.

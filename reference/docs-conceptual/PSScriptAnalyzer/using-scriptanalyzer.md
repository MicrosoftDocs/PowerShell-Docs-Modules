---
description: This article describes various features of PSScriptAnalyzer and how to use them.
ms.date: 06/28/2023
title: Using PSScriptAnalyzer
---
# Using PSScriptAnalyzer

This article describes various features of **PSScriptAnalyzer** and how to use them.

## Parser Errors

Beginning in version 1.18.0, **PSScriptAnalyzer** emits parser errors as diagnostic records in the
output stream.

```powershell
Invoke-ScriptAnalyzer -ScriptDefinition '"b" = "b"; function eliminate-file () { }'
```

```Output
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

The **RuleName** is set to the **ErrorId** of the parser error.

To suppress **ParseErrors**, do not include it as a value in the **Severity** parameter.

```powershell
Invoke-ScriptAnalyzer -ScriptDefinition '"b" = "b"; function eliminate-file () { }' -Severity Warning
```

```Output
RuleName           Severity ScriptName Line Message
--------           -------- ---------- ---- -------
PSUseApprovedVerbs Warning             1    The cmdlet 'eliminate-file' uses an
                                            unapproved verb.
```

## Suppressing Rules

You can suppress a rule by decorating a script, function, or parameter with .NET's
[SuppressMessageAttribute](/dotnet/api/system.diagnostics.codeanalysis.suppressmessageattribute).
The constructor for **SuppressMessageAttribute** takes two parameters: a category and a check ID. Set
the **categoryID** parameter to the name of the rule you want to suppress and set the **checkID**
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

Within the scope of the script, function, or parameter that you decorated, all rule violations are
suppressed.

To suppress a message on a specific parameter, set the **CheckId** parameter of 
**SuppressMessageAttribute** to the name of the parameter:

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

Use the **Scope** property of **SuppressMessageAttribute** to limit rule suppression to functions
or classes within the attribute's scope.

Use the value **Function** to suppress violations on all functions within the attribute's scope. Use
the value **Class** to suppress violations on all classes within the attribute's scope:

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

You can further restrict suppression based on a function, parameter, class, variable or object's
name by setting the **Target** property of **SuppressMessageAttribute** to a regular expression or
a wildcard pattern.

For example, to suppress the **PSAvoidUsingWriteHost** rule violation in `start-bar` and
`start-baz` but not in `start-foo` and `start-bam`:

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

To suppress violations in all of the functions:

```powershell
[Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSAvoidUsingWriteHost', '', Scope='Function', Target='*')]
Param()
```

To suppress violations in `start-bar`, `start-baz` and `start-bam` but not in `start-foo`:

```powershell
[Diagnostics.CodeAnalysis.SuppressMessageAttribute('PSAvoidUsingWriteHost', '', Scope='Function', Target='start-b*')]
Param()
```

> [!NOTE]
> Parser errors cannot be suppressed with **SuppressMessageAttribute**.

## Settings Support in ScriptAnalyzer

You can create settings that describe the ScriptAnalyzer rules to include or exclude based on
**Severity**. Use the **Settings** parameter of `Invoke-ScriptAnalyzer` to specify configuration.
This enables you to create a custom configuration for a specific environment. We support the
following modes for specifying the settings file:

### Built-in Presets

ScriptAnalyzer ships a set of built-in presets that can be used to analyze scripts. For example, if
you want to run _PowerShell Gallery_ rules on your module, use the following command:

```powershell
Invoke-ScriptAnalyzer -Path /path/to/module/ -Settings PSGallery -Recurse
```

Additionally, you can use other built-in presets, including **DSC** and **CodeFormatting**.
These presets can be tab completed for the **Settings** parameter.

### Explicit

The following example excludes two rules from the default set of rules and any rule with a
severity other than **Error** and **Warning**.

```powershell
# PSScriptAnalyzerSettings.psd1
@{
    Severity=@('Error','Warning')
    ExcludeRules=@('PSAvoidUsingCmdletAliases',
                'PSAvoidUsingWriteHost')
}
```

You can then invoke that settings file with `Invoke-ScriptAnalyzer`:

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

You can then invoke that settings file:

```powershell
Invoke-ScriptAnalyzer -Path MyScript.ps1 -Settings PSScriptAnalyzerSettings.psd1
```

### Implicit

If you place a settings file named `PSScriptAnalyzerSettings.psd1` in your project root,
**PSScriptAnalyzer** discovers it when you pass the project root as the **Path** parameter.

```powershell
Invoke-ScriptAnalyzer -Path "C:\path\to\project" -Recurse
```

Note that providing settings explicitly takes higher precedence over this implicit mode. Sample
settings files are provided in the `Settings` folder of the **PSScriptAnalyzer** module.

## Custom rules

It is possible to provide one or more paths to custom rules in the settings file. It is important
that these paths point either to a module's folder, which implicitly uses the module manifest, or to
the module's script file (`.psm1`). The module must export the custom rule functions using
`Export-ModuleMember` for them to be available to **PSScriptAnalyzer**.

In this example the property **CustomRulePath** points to two different modules. Both modules
export the rule functions with the verb **Measure** so `Measure-*` is used for the property
**IncludeRules**.

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

You can also add default rules by listing the rules in the **IncludeRules** property. When including
default rules, it is important that you set the property **IncludeDefaultRules** to `$true`;
otherwise the default rules are used.

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
    "powershell.scriptAnalysis.settingsPath": ".vscode/analyzersettings.psd1",
    "powershell.scriptAnalysis.enable": true,
}
```

## ScriptAnalyzer as a .NET library

You can directly consume ScriptAnalyzer's engine and functionality as a library.

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

You can use the **Fix** switch to to automatically replace violation-causing content with a
suggested alternative. Additionally, because `Invoke-ScriptAnalyzer` implements
**SupportsShouldProcess**, you can use **WhatIf** or **Confirm** to find out which corrections
would be applied. You should use source control when applying corrections as some changes, such as
the one for **AvoidUsingPlainTextForPassword**, might require additional script modifications that
can't be made automatically. Because initial encoding can't always be preserved when you
automatically apply suggestions, you should check your file's encoding if your scripts depend on a
particular encoding.

The **SuggestedCorrections** property of the error record enables quick-fix scenarios in editors
like VSCode. We provide valid **SuggestedCorrection** for the following rules:

- **AvoidAlias**
- **AvoidUsingPlainTextForPassword**
- **MisleadingBacktick**
- **MissingModuleManifestField**
- **UseToExportFieldsInManifest**

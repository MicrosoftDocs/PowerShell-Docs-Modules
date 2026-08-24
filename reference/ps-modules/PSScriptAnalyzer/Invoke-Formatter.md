---
document type: cmdlet
external help file: Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml
HelpUri: https://learn.microsoft.com/powershell/module/psscriptanalyzer/invoke-formatter?view=ps-modules&wt.mc_id=ps-gethelp
Module Name: PSScriptAnalyzer
ms.date: 08/24/2026
PlatyPS schema version: 2024-05-01
---

# Invoke-Formatter

## SYNOPSIS

Formats a script text based on the input settings or default settings.

## SYNTAX

### __AllParameterSets

```
Invoke-Formatter [-ScriptDefinition] <string> [[-Settings] <Object>] [[-Range] <int[]>]
```

## ALIASES

## DESCRIPTION

The `Invoke-Formatter` cmdlet takes a string input and formats it according to defined settings. If
no **Settings** parameter is provided, the cmdlet assumes the default code formatting settings as
defined in `Settings/CodeFormatting.psd1`.

## EXAMPLES

### EXAMPLE 1 - Format the input script text using the default settings

```powershell
$scriptDefinition = @'
function foo {
"hello"
  }
'@

Invoke-Formatter -ScriptDefinition $scriptDefinition
```

```Output
function foo {
    "hello"
}
```

### EXAMPLE 2 - Format the input script using the settings defined in a hashtable

```powershell
$scriptDefinition = @'
function foo {
"hello"
}
'@

$settings = @{
    IncludeRules = @("PSPlaceOpenBrace", "PSUseConsistentIndentation")
    Rules = @{
        PSPlaceOpenBrace = @{
            Enable = $true
            OnSameLine = $false
        }
        PSUseConsistentIndentation = @{
            Enable = $true
        }
    }
}

Invoke-Formatter -ScriptDefinition $scriptDefinition -Settings $settings
```

```Output
function foo
{
    "hello"
}
```

### EXAMPLE 3 - Format the input script text using the settings defined in a `.psd1` file

```powershell
Invoke-Formatter -ScriptDefinition $scriptDefinition -Settings /path/to/settings.psd1
```

## PARAMETERS

### -Range

The range within which formatting should take place. The value of this parameter must be an array of
four integers. These numbers must be greater than 0. The four integers represent the following four
values in this order:

- starting line number
- starting column number
- ending line number
- ending column number

```yaml
Type: System.Int32[]
DefaultValue: None
SupportsWildcards: false
Aliases: []
ParameterSets:
- Name: (All)
  Position: 3
  IsRequired: false
  ValueFromPipeline: false
  ValueFromPipelineByPropertyName: true
  ValueFromRemainingArguments: false
DontShow: false
AcceptedValues: []
HelpMessage: ''
```

### -ScriptDefinition

The text of the script to be formatted represented as a string. This is not a **ScriptBlock**
object.

```yaml
Type: System.String
DefaultValue: None
SupportsWildcards: false
Aliases: []
ParameterSets:
- Name: (All)
  Position: 1
  IsRequired: true
  ValueFromPipeline: true
  ValueFromPipelineByPropertyName: true
  ValueFromRemainingArguments: false
DontShow: false
AcceptedValues: []
HelpMessage: ''
```

### -Settings

A settings hashtable or a path to a PowerShell data file (`.psd1`) that contains the settings.

```yaml
Type: System.Object
DefaultValue: CodeFormatting
SupportsWildcards: false
Aliases: []
ParameterSets:
- Name: (All)
  Position: 2
  IsRequired: false
  ValueFromPipeline: false
  ValueFromPipelineByPropertyName: true
  ValueFromRemainingArguments: false
DontShow: false
AcceptedValues: []
HelpMessage: ''
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable,
-ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String

The **ScriptDefinition** parameter accepts a string from the pipeline.

### System.Object

The **Settings** parameter accepts values from the pipeline.

### System.Int32[]

The **Range** parameter accepts input  from the pipeline.

## OUTPUTS

### System.String

The formatted string result.

## NOTES

## RELATED LINKS

- [Using PSScriptAnalyzer](/powershell/utility-modules/psscriptanalyzer/using-scriptanalyzer)

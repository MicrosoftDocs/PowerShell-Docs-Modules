---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/test-markdowncommandhelp?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: Test-MarkdownCommandHelp
---

# Test-MarkdownCommandHelp

## SYNOPSIS

Tests the structure of a Markdown help file.

## SYNTAX

### Item

```
Test-MarkdownCommandHelp [-Path] <string[]> [-DetailView] [<CommonParameters>]
```

### Literal

```
Test-MarkdownCommandHelp -LiteralPath <string[]> [-DetailView] [<CommonParameters>]
```

## DESCRIPTION

This command reads a Markdown help file and validates the structure of the help content by checking
for the presence of required elements in the proper order. The command returns `$true` if the file
passes validation. The **DetailView** parameter can be used to display more detailed validation
information.

## EXAMPLES

### Example 1 - Test a Markdown help file

For this example, we test the structure of a Markdown Module help file. This test fails because the
command expects to test a Markdown Command help file. The output shows the kind of information you
can expect from the **DetailView** parameter.

```powershell
Test-MarkdownCommandHelp .\v2\Microsoft.PowerShell.PlatyPS\Microsoft.PowerShell.PlatyPS.md -DetailView
```

```Output
Test-MarkdownCommandHelp
  Valid: False
  File: D:\Git\PS-Src\platyPS\v2docs\v2\Microsoft.PowerShell.PlatyPS\Microsoft.PowerShell.PlatyPS.md

Messages:
  PASS: First element is a thematic break
  FAIL: SYNOPSIS not found.
  FAIL: SYNTAX not found.
  FAIL: DESCRIPTION not found.
  FAIL: EXAMPLES not found.
  FAIL: PARAMETERS not found.
  FAIL: INPUTS not found.
  FAIL: OUTPUTS not found.
  FAIL: NOTES not found.
  FAIL: RELATED LINKS not found.
```

## PARAMETERS

### -DetailView

Instructs the command to output detailed validation information.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -LiteralPath

Specifies a path to one or more command markdown files. The value of **LiteralPath** is used exactly
as it's typed. No characters are interpreted as wildcards. If the path includes escape characters,
enclose it in single quotation marks. Single quotation marks tell PowerShell not to interpret any
characters as escape sequences.

For more information, see
[about_Quoting_Rules](/powershell/module/microsoft.powershell.core/about/about_CommonParameters).

```yaml
Type: System.String[]
Parameter Sets: LiteralPath
Aliases: PSPath, LP
Accepted values:
Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False

```

### -Path

The path to the Markdown help file to test.

```yaml
Type: System.String[]
Parameter Sets: Path
Aliases:
Accepted values:
Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: True
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable,
-ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String

## OUTPUTS

### System.Boolean

### Microsoft.PowerShell.PlatyPS.MarkdownCommandHelpValidationResult

## NOTES

## RELATED LINKS

[Export-MarkdownCommandHelp](Export-MarkdownCommandHelp.md)

[New-MarkdownCommandHelp](New-MarkdownCommandHelp.md)

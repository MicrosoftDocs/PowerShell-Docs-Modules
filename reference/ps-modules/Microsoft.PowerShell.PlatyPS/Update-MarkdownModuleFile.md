---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/update-markdownmodulefile?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: Update-MarkdownModuleFile
---

# Update-MarkdownModuleFile

## SYNOPSIS

Updates the Markdown module file.

## SYNTAX

### path

```
Update-MarkdownModuleFile [-Path] <string> [-CommandHelp] <CommandHelp[]> [-Encoding <Encoding>]
 [-Force] [-HelpUri <string>] [-HelpInfoUri <string>] [-HelpVersion <version>] [-Locale <string>]
 [-Metadata <hashtable>] [-NoBackup] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### literalpath

```
Update-MarkdownModuleFile [-CommandHelp] <CommandHelp[]> -LiteralPath <string>
 [-Encoding <Encoding>] [-Force] [-HelpUri <string>] [-HelpInfoUri <string>]
 [-HelpVersion <version>] [-Locale <string>] [-Metadata <hashtable>] [-NoBackup] [-WhatIf]
 [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This cmdlet updates a Markdown module file with **CommandHelp** object information imported from
Markdown command files.

## EXAMPLES

### Example 1 - Update a module file from new command help files

```powershell
$mdfiles = Measure-PlatyPSMarkdown -Path .\Microsoft.PowerShell.PlatyPS\*.md
$mdfiles | Where-Object Filetype -match 'CommandHelp' |
    Import-MarkdownCommandHelp -Path {$_.FilePath} |
    Update-MarkdownModuleFile -Path .\Microsoft.PowerShell.PlatyPS\Microsoft.PowerShell.PlatyPS.md
```

## PARAMETERS

### -CommandHelp

The **CommandHelp** objects to export. You can pass the **CommandHelp** object on the pipeline or by
using this parameter.

```yaml
Type: Microsoft.PowerShell.PlatyPS.Model.CommandHelp[]
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: 1
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Confirm

Prompts you for confirmation before running the cmdlet.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf
Accepted values:
Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Encoding

The encoding to use when writing the markdown file. If no value is specified, encoding defaults to
the value of the `$OutputEncoding` preference variable.

```yaml
Type: System.Text.Encoding
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Use the **Force** parameter to overwrite the output file if it already exists.

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

### -HelpInfoUri

This parameter allows you to specify the URI used for updateable help. By default, the cmdlet uses
the HelpInfoUri specified in the module manifest.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -HelpUri

{{ Fill HelpUri Description }}

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -HelpVersion

This parameter allows you to specify the version of the help. The default value is `1.0.0.0`. This
version is written to the `HelpInfo.xml` file that is used for updateable help.

```yaml
Type: System.Version
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -LiteralPath

Specifies a path to one or more module markdown files. The value of **LiteralPath** is used exactly
as it's typed. No characters are interpreted as wildcards. If the path includes escape characters,
enclose it in single quotation marks. Single quotation marks tell PowerShell not to interpret any
characters as escape sequences.

For more information, see
[about_Quoting_Rules](/powershell/module/microsoft.powershell.core/about/about_CommonParameters).

```yaml
Type: System.String
Parameter Sets: LiteralPath
Aliases:
Accepted values:
Required: True
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Locale

This parameter allows you to specify the language locale for the help files. By default, the cmdlet
uses the current **CultureInfo**. Use the `Get-Culture` cmdlet to see the current culture settings
on your system.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Metadata

The metadata to add to the frontmatter of the markdown file. The metadata is a hashtable where the
you specify the key and value pairs to add to the frontmatter. New key names are added to the
existing frontmatter. The values of existing keys are overwritten. You can't overwrite the values of
the `document type` or `PlatyPS schema version` keys. If these keys are present in the hashtable,
the cmdlet ignores the values and outputs a warning.

```yaml
Type: System.Collections.Hashtable
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoBackup

By default, the cmdlet creates a backup of the original Markdown file before updating it. Use this
parameter to suppress the creation of the backup file.

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

### -Path

Specifies a path to one or more module markdown files.

```yaml
Type: System.String
Parameter Sets: Path
Aliases:
Accepted values:
Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Shows what would happen if the cmdlet runs. The cmdlet isn't run.

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

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable,
-ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### Microsoft.PowerShell.PlatyPS.Model.CommandHelp

## OUTPUTS

### System.IO.FileInfo

## NOTES

## RELATED LINKS

[New-MarkdownModuleFile](New-MarkdownModuleFile.md)

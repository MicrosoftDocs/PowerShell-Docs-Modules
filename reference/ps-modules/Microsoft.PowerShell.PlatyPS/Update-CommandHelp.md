---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/update-commandhelp?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: Update-CommandHelp
---

# Update-CommandHelp

## SYNOPSIS

Updates an imported **CommandHelp** object with the information from session cmdlet of the same
name.

## SYNTAX

### Path (Default)

```
Update-CommandHelp [-Path] <string[]> [-WhatIf] [-Confirm] [<CommonParameters>]
```

### LiteralPath

```
Update-CommandHelp -LiteralPath <string[]> [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This cmdlet imports a **CommandHelp** object from a Markdown file and updates the object with the
information from the session cmdlet of the same name. The updated object can then be re-exported to
update the source Markdown file.

## EXAMPLES

### Example 1

```powershell
$mdfiles = Measure-PlatyPSMarkdown -Path .\v1\Microsoft.PowerShell.PlatyPS\*.md
$cmdobj = $mdfiles | Where-Object Filetype -match 'CommandHelp' |
    Update-CommandHelp -Path {$_.FilePath}
$cmdobj.count
```

```Output
19
```

## PARAMETERS

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

### -LiteralPath

Specifies a path to one or more markdown command files. The value of **LiteralPath** is used exactly
as it's typed. No characters are interpreted as wildcards. If the path includes escape characters,
enclose it in single quotation marks. Single quotation marks tell PowerShell not to interpret any
characters as escape sequences.

For more information, see
[about_Quoting_Rules](/powershell/module/microsoft.powershell.core/about/about_CommonParameters).

```yaml
Type: System.String[]
Parameter Sets: LiteralPath
Aliases:
Accepted values:
Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByVale)
Accept wildcard characters: False'
```

### -Path

Specifies the path to one or more Markdown command file. Wildcard characters are permitted.

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

### -WhatIf

Shows what would happen if the cmdlet runs. The cmdlet isn't run.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi
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

### System.String

## OUTPUTS

### Microsoft.PowerShell.PlatyPS.Model.CommandHelp

## NOTES

This command is similar to the `Update-MarkdownCommandHelp` cmdlet, but it updates the
**CommandHelp** object in memory instead of updating the source Markdown file.

## RELATED LINKS

[Update-MarkdownCommandHelp](Update-MarkdownCommandHelp.md)

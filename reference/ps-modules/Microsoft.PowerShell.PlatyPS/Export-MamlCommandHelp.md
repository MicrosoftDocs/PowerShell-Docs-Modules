---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/export-mamlcommandhelp?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: Export-MamlCommandHelp
---

# Export-MamlCommandHelp

## SYNOPSIS

Exports **CommandHelp** objects to a MAML file.

## SYNTAX

### __AllParameterSets

```
Export-MamlCommandHelp [-CommandHelp] <CommandHelp[]> [-OutputFolder] <string>
 [-Encoding <Encoding>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This command converts **CommandHelp** objects to a MAML file. The MAML file contains help content in
the format used by the `Get-Help` command.

## EXAMPLES

### Example 1 - Create the MAML help file for a module

```powershell
$mdfiles = Measure-PlatyPSMarkdown -Path .\v2\Microsoft.PowerShell.PlatyPS\*.md
$mdfiles | Where-Object Filetype -match 'CommandHelp' |
    Import-MarkdownCommandHelp -Path {$_.FilePath} |
    Export-MamlCommandHelp -OutputFolder .\maml
```

```Output
    Directory: D:\Git\PS-Src\platyPS\v2docs\maml

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---           8/26/2024  3:18 PM         160928 Microsoft.PowerShell.PlatyPS-Help.xml
```

## PARAMETERS

### -CommandHelp

One or more **CommandHelp** objects to export.

```yaml
Type: Microsoft.PowerShell.PlatyPS.Model.CommandHelp[]
Parameter Sets: (All)
Aliases:
Accepted values:
Required: True
Position: 0
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
Default value: False
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

### -OutputFolder

The folder where the markdown file is saved. If the folder doesn't exist, it's created.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:
Accepted values:
Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
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

### Microsoft.PowerShell.PlatyPS.Model.CommandHelp

## OUTPUTS

### System.IO.FileInfo

## NOTES

## RELATED LINKS

- [Import-MarkdownCommandHelp](Import-MarkdownCommandHelp.md)

﻿---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/export-yamlcommandhelp?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: Export-YamlCommandHelp
---

# Export-YamlCommandHelp

## SYNOPSIS

Exports **CommandHelp** objects to YAML files.

## SYNTAX

### __AllParameterSets

```
Export-YamlCommandHelp [-CommandHelp] <CommandHelp[]> [-Encoding <Encoding>] [-Force]
 [-OutputFolder <string>] [-Metadata <hashtable>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This command exports a **CommandHelp** object to a Yaml file. You can add metadata frontmatter
to the Yaml file by using the **Metadata** parameter. You can get a **CommandHelp** object by
using the `Export-YamlCommandHelp` cmdlet or one of the `Import-*` cmdlets.

## EXAMPLES

### Example 1 - Convert Markdown command help content to Yaml format

This example imports Markdown help in the old format from the `.\v1` folder and exports it to the
`.\v2` folder in the new format.

```powershell
$mdfiles = Measure-PlatyPSMarkdown -Path .\v2\Microsoft.PowerShell.PlatyPS\*.md
$mdfiles | Where-Object Filetype -match 'CommandHelp' |
    Import-MarkdownCommandHelp -Path {$_.FilePath} |
    Export-YamlCommandHelp -OutputFolder .\v2\yaml
```

```Output
    Directory: D:\Git\PS-Src\platyPS\v2docs\v2\yaml

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---           8/26/2024  3:56 PM           3535 Compare-CommandHelp.yml
-a---           8/26/2024  3:56 PM           4776 Export-MamlCommandHelp.yml
-a---           8/26/2024  3:56 PM           8150 Export-MarkdownCommandHelp.yml
-a---           8/26/2024  3:56 PM           4998 Export-MarkdownModuleFile.yml
-a---           8/26/2024  3:56 PM           6357 Export-YamlCommandHelp.yml
-a---           8/26/2024  3:56 PM           5396 Export-YamlModuleFile.yml
-a---           8/26/2024  3:56 PM           3019 Import-MamlHelp.yml
-a---           8/26/2024  3:56 PM           4235 Import-MarkdownCommandHelp.yml
-a---           8/26/2024  3:56 PM           4318 Import-MarkdownModuleFile.yml
-a---           8/26/2024  3:56 PM           4391 Import-YamlCommandHelp.yml
-a---           8/26/2024  3:56 PM           3862 Import-YamlModuleFile.yml
-a---           8/26/2024  3:56 PM           2325 Measure-PlatyPSMarkdown.yml
-a---           8/26/2024  3:56 PM           5190 New-CommandHelp.yml
-a---           8/26/2024  3:56 PM           8335 New-MarkdownCommandHelp.yml
-a---           8/26/2024  3:56 PM           4697 New-MarkdownModuleFile.yml
-a---           8/26/2024  3:56 PM           3468 Test-MarkdownCommandHelp.yml
-a---           8/26/2024  3:56 PM           3172 Update-CommandHelp.yml
-a---           8/26/2024  3:56 PM           3908 Update-MarkdownCommandHelp.yml
-a---           8/26/2024  3:56 PM           5217 Update-MarkdownModuleFile.yml
```

## PARAMETERS

### -CommandHelp

The **CommandHelp** object to export. You can pass the **CommandHelp** object on the pipeline or by
using the **Command** parameter.

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

### -Metadata

The metadata to add to the frontmatter of the markdown file. The metadata is a hashtable where the
you specify the key and value pairs to add to the frontmatter. New key names are added to the
existing frontmatter. The values of existing keys are overwritten.

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

### -OutputFolder

The folder where the markdown file is saved. If the folder doesn't exist, it's created.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:
Accepted values:
Required: True
Position: Named
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

[Export-YamlCommandHelp](Export-YamlCommandHelp.md)

[Export-MarkdownCommandHelp](Export-MarkdownCommandHelp.md)

[Import-MarkdownCommandHelp](Import-MarkdownCommandHelp.md)

[Import-YamlCommandHelp](Import-YamlCommandHelp.md)

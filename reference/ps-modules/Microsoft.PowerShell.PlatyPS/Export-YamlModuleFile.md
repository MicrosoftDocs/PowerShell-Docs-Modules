---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/export-yamlmodulefile?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: Export-YamlModuleFile
---

# Export-YamlModuleFile

## SYNOPSIS

Exports a **ModuleFileInfo** object to a Yaml file.

## SYNTAX

### __AllParameterSets

```
Export-YamlModuleFile [-ModuleFileInfo] <ModuleFileInfo[]> [-Encoding <Encoding>] [-Force]
 [-OutputFolder <string>] [-Metadata <hashtable>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This command exports a **ModuleFileInfo** object to a markdown file. You can get a
**ModuleFileInfo** object by using the `Import-MarkdownModuleFile` cmdlet. You can import a module
file that's written in the old format and export it to the new format.

## EXAMPLES

### Example 1 - Export a ModuleFileInfo object to a markdown file

In this example, a **ModuleFileInfo** object by importing a module Markdown file. That object is
then exported to a Yaml file using the `Export-YamlModuleFile`.

```powershell
Import-MarkdownModuleFile -Path .\v2\Microsoft.PowerShell.PlatyPS\Microsoft.PowerShell.PlatyPS.md |
    Export-YamlModuleFile -OutputFolder .\v2\yaml
```

```Output
    Directory: D:\Git\PS-Src\platyPS\v2docs\v2\yaml

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---           8/26/2024  4:00 PM           2594 Microsoft.PowerShell.PlatyPS.yml
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

The metadata to add to the markdown file. The metadata is a hashtable that contains key-value pairs.

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

### -ModuleFileInfo

The **ModuleFileInfo** object to export. You can pass the **ModuleFileInfo** object on the pipeline
or by using the **ModuleFileInfo** parameter.

```yaml
Type: Microsoft.PowerShell.PlatyPS.ModuleFileInfo[]
Parameter Sets: (All)
Aliases:
Accepted values:
Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -OutputFolder

The **ModuleFileInfo** object to export to a markdown file. This object is created by the
`Import-MarkdownModuleFile` cmdlet.

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

### Microsoft.PowerShell.PlatyPS.ModuleFileInfo

## OUTPUTS

### System.IO.FileInfo

## NOTES

## RELATED LINKS

[Export-MarkdownModuleFile](Export-MarkdownModuleFile.md)

[Import-MarkdownModuleFile](Import-MarkdownModuleFile.md)

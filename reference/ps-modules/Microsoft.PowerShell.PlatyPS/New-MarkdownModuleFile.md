---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/new-markdownmodulefile?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: New-MarkdownModuleFile
---

# New-MarkdownModuleFile

## SYNOPSIS

Creates the Markdown module file for a PowerShell module.

## SYNTAX

### __AllParameterSets

```
New-MarkdownModuleFile -OutputFolder <string> [-CommandHelp <CommandHelp[]>] [-Encoding <Encoding>]
 [-Force] [-HelpUri <string>] [-HelpInfoUri <string>] [-HelpVersion <version>] [-Locale <string>]
 [-Metadata <hashtable>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This command creates the Markdown module file for a PowerShell module. The module file contains the
module metadata and a list of all commands with their synopsis descriptions. This file can be used
as the module landing page in a documentation set. The module metadata is used to by
`Export-MamlCommandHelp` to create the MAML help file for the module.

## EXAMPLES

### Example 1 - Create a new module file from a folder of command help files

```powershell
$mdfiles = Measure-PlatyPSMarkdown -Path .\v2\Microsoft.PowerShell.PlatyPS\*.md
$mdfiles | Where-Object Filetype -match 'CommandHelp' |
    Import-MarkdownCommandHelp -Path {$_.FilePath} |
    New-MarkdownModuleFile -OutputFolder .\v2 -Force
```

```Output
    Directory: D:\Docs\v2\Microsoft.PowerShell.PlatyPS

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---           9/18/2024  1:49 PM           2129 Microsoft.PowerShell.PlatyPS.md
```

### Example 2 - Create a new module file from a list of commands

```powershell
$newMarkdownCommandHelpSplat = @{
    CommandHelp  = Get-Command -Module Microsoft.PowerShell.PlatyPS | New-CommandHelp
    OutputFolder = '.\new'
    Force        = $true
}
New-MarkdownModuleFile @newMarkdownCommandHelpSplat
```

```Output
    Directory: D:\Docs\new\Microsoft.PowerShell.PlatyPS

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---           9/18/2024  1:49 PM           2129 Microsoft.PowerShell.PlatyPS.md
```

## PARAMETERS

### -CommandHelp

The **CommandHelp** objects to be included in the module file. You can pass the **CommandHelp**
object on the pipeline or by using the **Command** parameter.

```yaml
Type: Microsoft.PowerShell.PlatyPS.Model.CommandHelp[]
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
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

The encoding used when creating the output files. If not specified, the cmdlet uses value specified
by `$OutputEncoding`.

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

By default, this command doesn't overwrite existing files. When you use this parameter, the cmdlet
overwrites existing files.

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

### -OutputFolder

Specifies the location of where the Markdown module file is written. The cmdlet creates a folder for
each module based on the **CommandHelp** object being processed.

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

[Export-MarkdownModuleFile](Export-MarkdownModuleFile.md)

[Update-MarkdownModuleFile](Update-MarkdownModuleFile.md)

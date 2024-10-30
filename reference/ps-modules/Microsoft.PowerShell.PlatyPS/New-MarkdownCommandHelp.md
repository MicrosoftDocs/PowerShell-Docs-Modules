---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/new-markdowncommandhelp?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: New-MarkdownCommandHelp
---

# New-MarkdownCommandHelp

## SYNOPSIS

Creates Markdown help files for PowerShell modules and commands.

## SYNTAX

### __AllParameterSets

```
New-MarkdownCommandHelp -OutputFolder <string> [-CommandInfo <CommandInfo[]>] [-Encoding <Encoding>]
 [-Force] [-HelpUri <string>] [-HelpInfoUri <string>] [-HelpVersion <version>] [-Locale <string>]
 [-Metadata <hashtable>] [-ModuleInfo <psmoduleinfo[]>] [-WithModulePage]
 [-AbbreviateParameterTypename] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

Creates Markdown help files for PowerShell modules and commands.

## EXAMPLES

### Example 1 - Create Markdown help files for a module

```powershell
$newMarkdownCommandHelpSplat = @{
    ModuleInfo = Get-Module Microsoft.PowerShell.PlatyPS
    OutputFolder = '.'
    HelpVersion = '1.0.0.0'
    WithModulePage = $true
}
New-MarkdownCommandHelp @newMarkdownCommandHelpSplat
```

### Example 2 - Create Markdown help files from a list of commands

```powershell
$newMarkdownCommandHelpSplat = @{
    CommandInfo = Get-Command -Module Microsoft.PowerShell.PlatyPS
    OutputFolder = '.'
    HelpVersion = '1.0.0.0'
    WithModulePage = $true
}
New-MarkdownCommandHelp @newMarkdownCommandHelpSplat
```

## PARAMETERS

### -AbbreviateParameterTypename

By default, this command uses full type names in the parameter metadata and for the input and output
types. When you use this parameter, the cmdlet outputs short type names.

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

### -CommandInfo

A list of one or more commands to create help for.

```yaml
Type: System.Management.Automation.CommandInfo[]
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

This parameter allows you to specify the URI used for online help. By default, the cmdlet uses the
URI defined in the `[CmdletBinding()]` attribute for the command.

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

### -ModuleInfo

A list of one or more modules to create help for. The cmdlet creates Markdown help files for all
commands in the module. The cmdlet creates a folder matching the name of the module in the output
location. All Markdown files are written to the module folder.

```yaml
Type: System.Management.Automation.PSModuleInfo[]
Parameter Sets: (All)
Aliases:
Accepted values:
Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -OutputFolder

Specifies the location of where the Markdown help files are written. The cmdlet creates a folder for
each module being processed. If the target command isn't associated with a module, the cmdlet
creates a the Markdown file in the root of the output folder.

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

### -WithModulePage

By default, this cmdlet only creates Markdown files for commands. When you use this parameter, the
cmdlet creates a Markdown file for the module. This Markdown file contains a list of all commands in
the module and metadata used to create the HelpInfo.xml file.

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

### System.Management.Automation.CommandInfo

### System.Management.Automation.PSModuleInfo

## OUTPUTS

### System.IO.FileInfo

## NOTES

## RELATED LINKS

- [Export-MarkdownCommandHelp](Export-MarkdownCommandHelp.md)

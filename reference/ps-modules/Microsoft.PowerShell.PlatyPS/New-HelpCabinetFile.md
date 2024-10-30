---
external help file: Microsoft.PowerShell.PlatyPS-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/new-helpcabinetfile?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: New-HelpCabinetFile
---

# New-HelpCabinetFile

## SYNOPSIS

Creates a help cabinet file for a module that can be published as updateable help content.

## SYNTAX

### __AllParameterSets

```
New-HelpCabinetFile [-CabinetFilesFolder] <string> [-MarkdownModuleFile] <string>
 [-OutputFolder] <string> [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This cmdlet create `.cab` and `.zip` files that contain help files for a module.

> [!NOTE]
> This cmdlet depends on the `MakeCab.exe` native command, which is only available on Windows. This
> cmdlet raises an error if used on non-Windows machines.

This cmdlet uses metadata stored in the module Markdown file to name your `.cab` and `.zip` files.
This naming matches the pattern that the PowerShell help system requires for use as updatable help.

This cmdlet also generates or updates an existing `Helpinfo.xml` file. That file provides versioning
and locale details to the PowerShell help system.

## EXAMPLES

### Example 1 - Create updateable help files for a module

```powershell
$params = @{
    CabinetFilesFolder = '.\maml\Microsoft.PowerShell.PlatyPS'
    MarkdownModuleFile = '.\Microsoft.PowerShell.PlatyPS\Microsoft.PowerShell.PlatyPS.md'
    OutputFolder       = '.\cab'
}
New-HelpCabinetFile @params
```

## PARAMETERS

### -CabinetFilesFolder

The path to the folder containing the MAML file to be packaged.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:
Accepted values:
Required: True
Position: 0
Default value: None
Accept pipeline input: False
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

### -MarkdownModuleFile

Specifies the full path of the module Markdown file.

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

### -OutputFolder

The location where you want to write the `.cab`, `.zip`, and `HelpInfo.xml` files.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:
Accepted values:
Required: True
Position: 2
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

## OUTPUTS

### System.IO.FileInfo

The **FileInfo** objects that represent the files created by this cmdlet.

## NOTES

## RELATED LINKS

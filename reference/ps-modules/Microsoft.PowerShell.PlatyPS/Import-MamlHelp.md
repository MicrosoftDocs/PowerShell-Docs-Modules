---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/import-mamlhelp?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: Import-MamlHelp
---

# Import-MamlHelp

## SYNOPSIS

Imports MAML help from a file and creates **CommandHelp** objects for each command in the file.

## SYNTAX

### Path (Default)

```
Import-MamlHelp [-Path] <string[]> [<CommonParameters>]
```

### LiteralPath

```
Import-MamlHelp -LiteralPath <string[]> [<CommonParameters>]
```

## DESCRIPTION

This command can be used to create **CommandHelp** objects from MAML help files. These objects can
be used to generate Markdown help files. You can also use this command to test the validity of the
MAML help files.

## EXAMPLES

### Example 1

```powershell
Import-MamlHelp -Path .\maml\Microsoft.PowerShell.PlatyPS.dll-Help.xml
```

## PARAMETERS

### -LiteralPath

The path to the MAML help file. Specifies a path to one or more locations. The value of LiteralPath
is used exactly as it's typed. No characters are interpreted as wildcards. If the path includes
escape characters, enclose it in single quotation marks. Single quotation marks tell PowerShell not
to interpret any characters as escape sequences.

For more information, see
[about_Quoting_Rules](/powershell/module/microsoft.powershell.core/about/about_quoting_rules).

```yaml
Type: System.String[]
Parameter Sets: LiteralPath
Aliases:
Accepted values:
Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Path

The path to the MAML help file. Specifies a path to one or more locations.

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

### Microsoft.PowerShell.PlatyPS.Model.CommandHelp

## NOTES

The MAML file format doesn't support all the information that can be stored in a **CommandHelp**
object. If you convert the imported information to markdown format, the resulting markdown file
is not a complete representation of the original command.

## RELATED LINKS

[Export-MamlHelp](Export-MamlCommandHelp.md)

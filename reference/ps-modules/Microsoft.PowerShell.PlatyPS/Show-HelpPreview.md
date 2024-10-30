---
external help file: Microsoft.PowerShell.PlatyPS-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/show-helppreview?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: Show-HelpPreview
---

# Show-HelpPreview

## SYNOPSIS

View MAML file contents as it would appear when output by `Get-Help`.

## SYNTAX

### Path

```
Show-HelpPreview [-Path] <string[]> [-ConvertNotesToList] [-ConvertDoubleDashLists]
 [<CommonParameters>]
```

### LiteralPath

```
Show-HelpPreview [-LiteralPath] <string[]> [-ConvertNotesToList] [-ConvertDoubleDashLists]
 [<CommonParameters>]
```

## DESCRIPTION

The `Show-HelpPreview` cmdlet displays your generated external help as `Get-Help` output. Specify
one or more files in Microsoft Assistance Markup Language (MAML) format.

## EXAMPLES

### Example 1 - Display the contents of a MAML file

This example displays the contents of PlatyPS MAML file as it would appear when output by
`Get-Help`.

```powershell
Show-HelpPreview -Path .\Microsoft.PowerShell.PlatyPS\Microsoft.PowerShell.PlatyPS-Help.xml
```

## PARAMETERS

### -ConvertDoubleDashLists

Indicates that this cmdlet converts double-hyphen list bullets into single-hyphen bullets.
Double-hyphen lists are common in Windows PowerShell documentation. Markdown accepts single-hyphens
for lists.

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

### -ConvertNotesToList

Indicates that this cmdlet formats multiple paragraph items in the **NOTES** section as single list
items.

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

Specifies one or more paths to MAML help files. Wildcards aren't supported.

```yaml
Type: System.String[]
Parameter Sets: LiteralPath
Aliases: LP, PSPath
Accepted values:
Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Path

Specifies one or more paths to MAML help files. Wildcards are supported.

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

You can pipe path strings to this command.

## OUTPUTS

### MamlCommandHelpInfo

This cmdlet returns a `MamlCommandHelpInfo` objects. This is the same object that is returned by
`Get-Help`.

## NOTES

## RELATED LINKS

- [Get-Help](xref:Microsoft.PowerShell.Core.Get-Help)

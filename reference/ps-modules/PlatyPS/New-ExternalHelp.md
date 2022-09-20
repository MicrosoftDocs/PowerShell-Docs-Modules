---
external help file: platyPS-help.xml
Module Name: platyPS
ms.date: 03/16/2021
online version: https://learn.microsoft.com/powershell/module/platyps/new-externalhelp?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# New-ExternalHelp

## SYNOPSIS
Creates external help file based on markdown supported by PlatyPS.

## SYNTAX

```
New-ExternalHelp -Path <String[]> -OutputPath <String> [-ApplicableTag <String[]>] [-Encoding <Encoding>]
 [-MaxAboutWidth <Int32>] [-ErrorLogFile <String>] [-Force] [-ShowProgress] [<CommonParameters>]
```

## DESCRIPTION

The `New-ExternalHelp` cmdlet creates an external help file based on markdown help files supported
by PlatyPS. You can ship this with a module to provide help using the `Get-Help` cmdlet.

If the markdown files that you specify don't follow the PlatyPS
[Schema](https://github.com/PowerShell/platyPS/blob/master/platyPS.schema.md), this cmdlet returns
error messages.

## EXAMPLES

### Example 1: Create external help based on the contents of a folder

```powershell
PS C:\> New-ExternalHelp -Path ".\docs" -OutputPath "out\platyPS\en-US"

    Directory: D:\Working\PlatyPS\out\platyPS\en-US


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/19/2016  12:32 PM          46776 platyPS-help.xml
```

This command creates an external help file in the specified location.
This command uses the best practice that the folder name includes the locale.

### Example 2: Create help that uses custom encoding

```powershell
PS C:\> New-ExternalHelp -Path ".\docs" -OutputPath "out\PlatyPS\en-US" -Force -Encoding ([System.Text.Encoding]::Unicode)


    Directory: D:\Working\PlatyPS\out\PlatyPS\en-US


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/22/2016   6:34 PM         132942 platyPS-help.xml
```

This command creates an external help file in the specified location. This command specifies the
**Force** parameter, therefore, it overwrites an existing file. The command specifies Unicode
encoding for the created file.

### Example 3: Write warnings and errors to file

```powershell
PS C:\> New-ExternalHelp -Path ".\docs" -OutputPath "out\platyPS\en-US" -ErrorLogFile ".\WarningsAndErrors.json"

    Directory: D:\Working\PlatyPS\out\platyPS\en-US


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/19/2016  12:32 PM          46776 platyPS-help.xml
```

This command creates an external help file in the specified location. This command uses the best
practice that the folder name includes the locale. This command writes the warnings and errors to
the WarningsAndErrors.json file.

## PARAMETERS

### -OutputPath

Specifies the path of a folder where this cmdlet saves your external help file.
The folder name should end with a locale folder, as in the following example: `.\out\PlatyPS\en-US\`.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Encoding

Specifies the character encoding for your external help file. Specify a **System.Text.Encoding**
object. For more information, see
[about_Character_Encoding](/powershell/module/microsoft.powershell.core/about/about_character_encoding).

```yaml
Type: Encoding
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: UTF8 without BOM
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Indicates that this cmdlet overwrites an existing file that has the same name.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path

Specifies an array of paths of markdown files or folders. This cmdlet creates external help based on
these files and folders.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: True
```

### -ApplicableTag

Specify array of tags to use as a filter. If cmdlet has `applicable` in the yaml metadata and none
of the passed tags is mentioned there, cmdlet would be ignored in the generated help. Same applies
to the Parameter level `applicable` yaml metadata. If `applicable` is omitted, cmdlet or parameter
would be always present. See [design issue](https://github.com/PowerShell/platyPS/issues/273) for
more details.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MaxAboutWidth

Specifies the maximum line length when generating "about" help text files. Other help file types are
not affected by this parameter. For more information, see
[New-MarkdownAboutHelp](New-MarkdownAboutHelp.md).

Lines inside code blocks aren't wrapped and aren't affected by the **MaxAboutWidth** parameter.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: 80
Accept pipeline input: False
Accept wildcard characters: False
```

### -ErrorLogFile

The path where this cmdlet will save formatted results log file.

The path must include the location and name of the folder and file name with the json extension. The
JSON object contains three properties: **Message**, **FilePath**, and **Severity** (Warning or
Error).

If this path isn't provided, no log is generated.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ShowProgress

Display progress bars under parsing existing markdown files.

If this is used generating of help is much slower.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### String[]

You can pipe an array of paths to this cmdlet.

## OUTPUTS

### System.IO.FileInfo[]

This cmdlet returns a `FileInfo[]` object for created files.

## NOTES

## RELATED LINKS

[PowerShell V2 External MAML Help](https://devblogs.microsoft.com/powershell/powershell-v2-external-maml-help/)

[Schema](https://github.com/PowerShell/platyPS/blob/master/platyPS.schema.md)

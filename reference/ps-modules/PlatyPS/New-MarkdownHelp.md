---
external help file: platyPS-help.xml
Module Name: platyPS
ms.date: 03/16/2021
online version: https://learn.microsoft.com/powershell/module/platyps/new-markdownhelp?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# New-MarkdownHelp

## SYNOPSIS
Creates help in markdown format.

## SYNTAX

### FromModule

```
New-MarkdownHelp -Module <String[]> [-Session <PSSession>] [-Force] [-AlphabeticParamsOrder]
 [-Metadata <Hashtable>] -OutputFolder <String> [-NoMetadata] [-UseFullTypeName] [-Encoding <Encoding>]
 [-WithModulePage] [-ModulePagePath <String>] [-Locale <String>] [-HelpVersion <String>] [-FwLink <String>]
 [-ExcludeDontShow] [<CommonParameters>]
```

### FromCommand

```
New-MarkdownHelp -Command <String[]> [-Session <PSSession>] [-Force] [-AlphabeticParamsOrder]
 [-Metadata <Hashtable>] [-OnlineVersionUrl <String>] -OutputFolder <String> [-NoMetadata] [-UseFullTypeName]
 [-Encoding <Encoding>] [-ExcludeDontShow] [<CommonParameters>]
```

### FromMaml
```
New-MarkdownHelp -MamlFile <String[]> [-ConvertNotesToList] [-ConvertDoubleDashLists] [-Force]
 [-AlphabeticParamsOrder] [-Metadata <Hashtable>] -OutputFolder <String> [-NoMetadata] [-UseFullTypeName]
 [-Encoding <Encoding>] [-WithModulePage] [-ModulePagePath <String>] [-Locale <String>] [-HelpVersion <String>]
 [-FwLink <String>] [-ModuleName <String>] [-ModuleGuid <String>] [-ExcludeDontShow] [<CommonParameters>]
```

## DESCRIPTION

The `New-MarkdownHelp` cmdlet creates help in markdown format based on a module, a command, or a
file in Microsoft Assistance Markup Language (MAML) format.

## EXAMPLES

### Example 1: Create help from a command

```powershell
PS C:\> function Command03 {param([string]$Value)}
PS C:\> New-MarkdownHelp -Command "Command03" -OutputFolder ".\docs"


    Directory: D:\Working\docs


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/22/2016   6:53 PM            664 Command03.md
```

The first command creates a function named `Command03` using standard Windows PowerShell syntax.

The second command creates help for that stub function in the .\docs folder.

### Example 2: Create help from a module

```powershell
PS C:\> Import-Module -Module "PlatyPS"
PS C:\> New-MarkdownHelp -Module "PlatyPS" -OutputFolder ".\docs" -Force


    Directory: D:\Working\PlatyPS\docs


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/22/2016   6:54 PM           1496 Get-HelpPreview.md
-a----        5/22/2016   6:54 PM           3208 Get-MarkdownMetadata.md
-a----        5/22/2016   6:54 PM           3059 New-ExternalHelp.md
-a----        5/22/2016   6:54 PM           2702 New-ExternalHelpCab.md
-a----        5/22/2016   6:54 PM           6234 New-MarkdownHelp.md
-a----        5/22/2016   6:54 PM           2346 Update-MarkdownHelp.md
-a----        5/22/2016   6:54 PM           1633 Update-MarkdownHelpModule.md
-a----        5/22/2016   6:54 PM           1630 Update-MarkdownHelpSchema.md
```

The first command loads the **PlatyPS** module into the current session using the `Import-Module`
cmdlet.

The second command creates help for all the cmdlets in the PlatyPS module. It stores them in the
`.\docs` folder. This command specifies the **Force** parameter. Therefore, it overwrites existing
help markdown files that have the same name.

### Example 3: Create help from an existing MAML file

```powershell
PS C:\> New-MarkdownHelp -OutputFolder "D:\PSReadLine\docs" -MamlFile 'C:\Program Files\WindowsPowerShell\Modules\PSReadLine\1.1\en-US\Microsoft.PowerShell.PSReadLine.dll-help.xml'

    Directory: D:\PSReadLine\docs


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/22/2016   6:56 PM           7443 Get-PSReadLineKeyHandler.md
-a----        5/22/2016   6:56 PM           3586 Get-PSReadLineOption.md
-a----        5/22/2016   6:56 PM           1549 Remove-PSReadLineKeyHandler.md
-a----        5/22/2016   6:56 PM           5947 Set-PSReadLineKeyHandler.md
-a----        5/22/2016   6:56 PM          15320 Set-PSReadLineOption.md
```

This command creates help in markdown format for the specified help MAML file. You don't have to
load the module, as in the previous example. If the module is already loaded, this command creates
help based on the MAML file, not on the currently installed module.

### Example 4: Create help from an existing MAML file for use in a CAB file

```powershell
PS C:\> New-MarkdownHelp -OutputFolder "D:\PSReadLine\docs" -MamlFile 'C:\Program Files\WindowsPowerShell\Modules\PSReadLine\1.1\en-US\Microsoft.PowerShell.PSReadLine.dll-help.xml' -WithModulePage  -Force -ModuleName "PSReadLine"


    Directory: D:\PSReadLine\docs


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/22/2016   6:59 PM           7443 Get-PSReadLineKeyHandler.md
-a----        5/22/2016   6:59 PM           3586 Get-PSReadLineOption.md
-a----        5/22/2016   6:59 PM           1549 Remove-PSReadLineKeyHandler.md
-a----        5/22/2016   6:59 PM           5947 Set-PSReadLineKeyHandler.md
-a----        5/22/2016   6:59 PM          15320 Set-PSReadLineOption.md
-a----        5/22/2016   6:59 PM            942 PSReadLine.md
```

This command creates help in markdown format for the specified help MAML file, as in the previous
example. This command also specifies the **WithModulePage** parameter and the **ModuleName**
parameter. The command creates a file named PSReadLine.md that contains links to the other markdown
files in this module and metadata that can be used to create `.cab` files.

## PARAMETERS

### -Command

Specifies the name of a command in your current session. This can be any command supported by
PowerShell help, such as a cmdlet or a function.

```yaml
Type: String[]
Parameter Sets: FromCommand
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

Indicates that this cmdlet overwrites existing files that have the same names.

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

### -FwLink

Specifies the forward link for the module page. This value is required for `.cab` file creation.
This value is used as markdown header metadata in the module page.

```yaml
Type: String
Parameter Sets: FromModule, FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -HelpVersion

Specifies the version of your help. This value is required for `.cab` file creation. This value is
used as markdown header metadata in the module page.

```yaml
Type: String
Parameter Sets: FromModule, FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Locale

Specifies the locale of your help. This value is required for .cab file creation. This value is used
as markdown header metadata in the module page.

```yaml
Type: String
Parameter Sets: FromModule, FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MamlFile

Specifies an array of paths path of MAML `.xml` help files.

```yaml
Type: String[]
Parameter Sets: FromMaml
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Metadata

Specifies metadata that this cmdlet includes in the help markdown files as a hash table of
string-to-sting key-value pairs. This cmdlet writes the metadata in the header of each markdown help
file.

The `New-ExternalHelp` cmdlet doesn't use this metadata. External tools can use this metadata.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Module

Specifies an array of names of modules for which this cmdlet creates help in markdown format.

```yaml
Type: String[]
Parameter Sets: FromModule
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ModuleGuid

Specifies the GUID of the module of your help. This value is required for `.cab` file creation. This
value is used as markdown header metadata in the module page.

```yaml
Type: String
Parameter Sets: FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ModuleName

Specifies the name of the module of your help. This value is required for `.cab` file creation. This
value is used as markdown header metadata in the module page.

```yaml
Type: String
Parameter Sets: FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoMetadata

Indicates that this cmdlet doesn't write any metadata in the generated markdown.

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

### -OnlineVersionUrl

Specifies the address where the updatable help function downloads updated help. If you don't specify
a value, the cmdlet uses an empty string.

```yaml
Type: String
Parameter Sets: FromCommand
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OutputFolder

Specifies the path of the folder where this cmdlet creates the markdown help files.

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

### -WithModulePage

Indicates that this cmdlet creates a module page in the output folder. This file has the name that
the **ModuleName** parameter specifies. If you didn't specify that parameter, the cmdlet supplies
the default name `MamlModule`. You can overwrite this setting using **ModulePagePath** which allows
you to define different path for module page

```yaml
Type: SwitchParameter
Parameter Sets: FromModule, FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ConvertNotesToList

Indicates that this cmdlet formats multiple paragraph items in the **NOTES** section as single list
items.

```yaml
Type: SwitchParameter
Parameter Sets: FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ConvertDoubleDashLists

Indicates that this cmdlet converts double-hyphen list bullets into single-hyphen bullets.
Double-hyphen lists are common in Windows PowerShell documentation. Markdown accepts single-hyphens
for lists.

```yaml
Type: SwitchParameter
Parameter Sets: FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -AlphabeticParamsOrder

Order parameters alphabetically by name in PARAMETERS section. There are 5 exceptions: `-Confirm`,
`-WhatIf`, `-IncludeTotalCount`, `-Skip`, and `-First` parameters will be the last. These parameters
are common and hence have well-defined behavior.

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

### -UseFullTypeName

Indicates that the target document will use a full type name instead of a short name for parameters.

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

### -Session

Provides support for remote commands. Pass the session that you used to create the commands with
`Import-PSSession`. This is required to get accurate parameters metadata from the remote session.

```yaml
Type: PSSession
Parameter Sets: FromModule, FromCommand
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ModulePagePath

When **WithModule** parameter is used by default it puts .md file in same location as all other
docs. With this parameter you can specify new name/location providing better placement options.

```yaml
Type: String
Parameter Sets: FromModule, FromMaml
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ExcludeDontShow

Exclude the parameters marked with `DontShow` in the parameter attribute from the help content.

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

You can pipe module names to this cmdlet. These are the modules from which this cmdlet creates help
markdown.

## OUTPUTS

### System.IO.FileInfo[]

This cmdlet returns a FileInfo[] object for created files.

## NOTES

## RELATED LINKS

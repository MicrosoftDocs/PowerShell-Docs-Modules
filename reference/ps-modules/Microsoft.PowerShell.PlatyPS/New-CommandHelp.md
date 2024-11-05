---
external help file: Microsoft.PowerShell.PlatyPS.dll-Help.xml
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.platyps/new-commandhelp?view=ps-modules&WT.mc_id=ps-gethelp
Locale: en-US
Module Name: Microsoft.PowerShell.PlatyPS
ms.custom: preview1
ms.date: 10/25/2024
schema: 2.0.0
title: New-CommandHelp
---

# New-CommandHelp

## SYNOPSIS

Creates **CommandHelp** objects for a PowerShell command that's loaded in the session.

## SYNTAX

### __AllParameterSets

```
New-CommandHelp [-CommandInfo] <CommandInfo[]> [<CommonParameters>]
```

## DESCRIPTION

This cmdlet takes a list of one or more PowerShell commands and creates **CommandHelp** objects for
each command. The **CommandHelp** object is a structured representation of the help content that can
be used to export to different formats.

## EXAMPLES

### Example 1 - Creates a **CommandHelp** object for a cmdlet

The following example creates a **CommandHelp** object for the `New-PSSession` cmdlet. The
`Get-Member` cmdlet is used to display the properties and methods of the **CommandHelp** object.

```powershell
New-CommandHelp New-PSSession | Get-Member
```

```Output
   TypeName: Microsoft.PowerShell.PlatyPS.Model.CommandHelp

Name                        MemberType Definition
----                        ---------- ----------
Equals                      Method     bool Equals(Microsoft.PowerShell.PlatyPS.Model.CommandHelp other)...
GetHashCode                 Method     int GetHashCode()
GetType                     Method     type GetType()
ToString                    Method     string ToString()
TryGetParameter             Method     bool TryGetParameter(string name, [ref] Microsoft.PowerShell.Plat...
Aliases                     Property   System.Collections.Generic.List[string] Aliases {get;}
Description                 Property   string Description {get;set;}
Diagnostics                 Property   Microsoft.PowerShell.PlatyPS.Model.Diagnostics Diagnostics {get;s...
Examples                    Property   System.Collections.Generic.List[Microsoft.PowerShell.PlatyPS.Mode...
ExternalHelpFile            Property   string ExternalHelpFile {get;set;}
HasCmdletBinding            Property   bool HasCmdletBinding {get;set;}
HasWorkflowCommonParameters Property   bool HasWorkflowCommonParameters {get;set;}
Inputs                      Property   System.Collections.Generic.List[Microsoft.PowerShell.PlatyPS.Mode...
Locale                      Property   cultureinfo Locale {get;set;}
Metadata                    Property   ordered Metadata {get;set;}
ModuleGuid                  Property   System.Nullable[guid] ModuleGuid {get;set;}
ModuleName                  Property   string ModuleName {get;set;}
Notes                       Property   string Notes {get;set;}
OnlineVersionUrl            Property   string OnlineVersionUrl {get;set;}
Outputs                     Property   System.Collections.Generic.List[Microsoft.PowerShell.PlatyPS.Mode...
Parameters                  Property   System.Collections.Generic.List[Microsoft.PowerShell.PlatyPS.Mode...
RelatedLinks                Property   System.Collections.Generic.List[Microsoft.PowerShell.PlatyPS.Mode...
SchemaVersion               Property   string SchemaVersion {get;set;}
Synopsis                    Property   string Synopsis {get;set;}
Syntax                      Property   System.Collections.Generic.List[Microsoft.PowerShell.PlatyPS.Mode...
Title                       Property   string Title {get;set;}
```

## PARAMETERS

### -CommandInfo

A list of one or more PowerShell commands (cmdlets, functions, scripts). The cmdlet creates a
**CommandHelp** object for each command.

```yaml
Type: System.Management.Automation.CommandInfo[]
Parameter Sets: (All)
Aliases:
Accepted values:
Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable,
-ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.Management.Automation.CommandInfo

## OUTPUTS

### Microsoft.PowerShell.PlatyPS.Model.CommandHelp

## NOTES

## RELATED LINKS

[Export-MarkdownCommandHelp](Export-MarkdownCommandHelp.md)

[Export-YamlCommandHelp](Export-YamlCommandHelp.md)

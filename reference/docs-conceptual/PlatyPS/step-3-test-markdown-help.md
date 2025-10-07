---
description: This article shows how to test the Markdown help files to ensure that the content follows the expected format.
ms.date: 10/09/2025
title: Test Markdown help files
---
# Test Markdown help files

PlatyPS expects the Markdown files to follow a specific structure. If the structure isn't correct,
the conversion to MAML format can fail or MAML content can be incomplete. Once you have completed
editing the Markdown files, you should test them to ensure that the structure is correct.

The best way to test the Markdown Command Help file is to import the file and inspect the resulting
object. The following example imports the Markdown file for the `Measure-PlatyPSMarkdown` command
and stores the resulting object in the `$cmdHelp` variable. The `Format-List *` command displays all
the properties of the object. Inspect the properties to ensure that they contain the expected
content.

```powershell
$cmdFilePath = '.\Microsoft.PowerShell.PlatyPS\Measure-PlatyPSMarkdown.md'
$cmdHelp = Import-MarkdownCommandHelp -Path $cmdFilePath
$cmdHelp | Format-List *
```

```Output
Metadata                    : {[document type, cmdlet], [external help file, WidgetModule-Help.xml],
                              [HelpUri, ], [Locale, en-US]…}
Locale                      : en-US
ModuleGuid                  :
ExternalHelpFile            : WidgetModule-Help.xml
OnlineVersionUrl            :
SchemaVersion               : 2024-05-01
ModuleName                  : WidgetModule
Title                       : Get-Widget
Synopsis                    : Gets one or more widgets based on specified criteria.
Syntax                      : {Get-Widget [-Name] <string> [-Color <ConsoleColor>] [-Size <int>]
                              [-Detailed] [<CommonParameters>]}
AliasHeaderFound            : True
Aliases                     :
Description                 : Gets one or more widgets from the system. You can filter the results
                              by specifying the widget's name, color, or size. Use the -Detailed
                              switch to retrieve additional information about each widget.
                              each widget.
Examples                    : {Microsoft.PowerShell.PlatyPS.Model.Example}
Parameters                  : {Color, Detailed, Name, Size}
Inputs                      : {System.String}
Outputs                     : {Widget}
Notes                       :
RelatedLinks                : {Microsoft.PowerShell.PlatyPS.Model.Links}
HasCmdletBinding            : True
HasWorkflowCommonParameters : False
Diagnostics                 : Microsoft.PowerShell.PlatyPS.Model.Diagnostics
```

The `$cmdHelp` also contains a **Diagnostics** property that contains information about any
structural problems with the Markdown file. Review the diagnostics information and correct any
problems in the Markdown file.

```powershell
$cmdHelp.Diagnostics.Messages
```

The **Severity** column indicates the severity of the problem. Warnings and errors should be
investigated and corrected.

```Output
Source      Severity    Message                                           Identifier
------      --------    -------                                           ----------
Metadata    Information {Metadata}                                        found 'external help …
Metadata    Information {Metadata}                                        found 'Locale'
Metadata    Information {Metadata}                                        found 'Module Name'
Metadata    Information {Metadata}                                        found 'ms.date'
Metadata    Information {Metadata}                                        found 'HelpUri'
Metadata    Information {Metadata}                                        found 'PlatyPS schema…
Metadata    Information {Metadata}                                        found 'title'
General     Information {CmdletBinding is present}                        GetCmdletBindingState
General     Information {Workflow parameters not present}                 GetWorkflowCommonPara…
Synopsis    Information {SYNOPSIS found}
Syntax      Information {Syntax found}                                    Get-Widget [-Name] <s…
Alias       Information {ALIASES header found}                            alias header is AST 8
Alias       Information {Alias string length}                             alias string length: 0
Description Information {DESCRIPTION header found}                        DESCRIPTION
Example     Information {EXAMPLES header found}                           1 examples found
Parameter   Information {Parameters}                                      4 parameters found
Parameter   Information {Color found}                                     Version 2 metadata fo…
Parameter   Information {Detailed found}                                  Version 2 metadata fo…
Parameter   Information {Name found}                                      Version 2 metadata fo…
Parameter   Information {Size found}                                      Version 2 metadata fo…
Parameter   Information {CommonParameters found}                          GetParameters
Inputs      Information {GetInput}                                        1 items found
Outputs     Information {GetOutput}                                       1 items found
Notes       Warning     {Notes content not found}                         GetNotes
Links       Information {Links found}                                     GetRelatedLinks
Links       Information {Found related links as unordered list.}
Links       Information {adding link [All about widgets](https://docs…
Links       Information {Links found}                                     1 links found
```

For more information about the expected structure of the Markdown files, see
[step-2-edit-markdown-help.md](step-2-edit-markdown-help.md).

You can test the module Markdown files in a similar way using the `Import-MarkdownModuleFile`
command. For example:

```powershell
$modFilePath = '.\Microsoft.PowerShell.PlatyPS\Microsoft.PowerShell.PlatyPS.md'
$mod = Import-MarkdownModuleFile -Path $modFilePath
$mod.Diagnostics.Messages
```

```Output

Source                Severity    Message                        Identifier
------                --------    -------                        ----------
ModuleFileTitle       Information {Title WidgetModule Module…    GetModuleFileTitle…
Metadata              Information {found guid 8bc631f3-e82e-…    GetMetadata
Metadata              Information {found module name WidgetM…    GetMetadata
Metadata              Information {locale set to en-US}          GetMetadata
ModuleFileDescription Information {Module description found}     GetModuleFileDescr…
ModuleFileCommand     Information {command Get-Widget found}     GetModuleFileComma…
```

## Next Steps

- [Convert and publish the help files](step-4-convert-publish-help.md)

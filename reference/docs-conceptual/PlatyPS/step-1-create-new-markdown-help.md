---
description: Use Microsoft.PowerShell.PlatyPS to create new command help files for PowerShell modules.
ms.date: 10/07/2025
title: Create new command help Markdown using PlatyPS
---
# Create new command help Markdown using Microsoft.PowerShell.PlatyPS

Rather than hand-writing MAML help files, the Microsoft.PowerShell.PlatyPS (PlatyPS) module allows
you create command documentation in Markdown format, then convert the Markdown files to MAML format.
PlatyPS creates a Markdown template for each command in your module. PlatyPS doesn't write the help
content for you. You must fill in the template with content that describes the commands, parameters,
examples, and other supporting information.

Creating MAML help content consists of the following steps:

1. Create the Markdown template files for your module.
1. Edit the Markdown files to add content.
1. Test the Markdown files to ensure that the structure is correct.
1. Convert the Markdown files to MAML format and publish help

This article describes the first three steps.

## Prerequisites

Before you begin, you must install the Microsoft.PowerShell.PlatyPS module from the PowerShell
Gallery. You must also have installed the module that you want to document.

Use the following command to install PlatyPS:

```powershell
Install-PSResource -Name Microsoft.PowerShell.PlatyPS
```

## Step 1 - Create the Markdown template files

There are two types of Markdown files to create for your module:

- Command help files - one file for each command.
- Module file - contains metadata about the module and lists the commands in the module.

Both file types are required if you want to create MAML content for your module.

Run the following command to create the Markdown files:

```powershell
$newMarkdownCommandHelpSplat = @{
    ModuleInfo = Get-Module -Name 'YourModuleName'
    OutputFolder = './docs'
    WithModulePage = $true
}
New-MarkdownCommandHelp @newMarkdownCommandHelpSplat
```

The `New-MarkdownCommandHelp` command creates a folder named `./docs/YourModuleName` in the current
directory. The folder contains the Markdown files for each command in the module, as well as a
module file named `YourModuleName.md`. The module file contains metadata about the module and lists
each commands with its synopsis description. This file can be converted to HTML to be used as an
index page for the module on a documentation website.

When the module file is first created, there are no synopsis descriptions for the commands. The
Markdown files contains placeholders that you must replace with the synopsis descriptions.

If you omit the **WithModulePage** parameter, the module file is not created. You can create the
module file later, after you have written the synopsis descriptions, by running the
`New-MarkdownModuleFile` command. For example:

```powershell
Measure-PlatyPSMarkdown -Path ./docs/YourModuleName/*.md |
    Where-Object Filetype -match 'CommandHelp' |
    Import-MarkdownCommandHelp -Path {$_.FilePath} |
    New-MarkdownModuleFile -OutputFolder ./docs -Force
```

This command creates the module file in the `./docs/YourModuleName` folder. The `-Force` parameter
overwrites any existing module file. If you have filled in the synopsis descriptions in the command
files, the descriptions are included in the module file.

For more information about these commands, see the following articles:

- [Measure-PlatyPSMarkdown](xref:Microsoft.PowerShell.PlatyPS.Measure-PlatyPSMarkdown)
- [Import-MarkdownCommandHelp](xref:Microsoft.PowerShell.PlatyPS.Import-MarkdownCommandHelp)
- [New-MarkdownCommandHelp](xref:Microsoft.PowerShell.PlatyPS.New-MarkdownCommandHelp)
- [New-MarkdownModuleFile](xref:Microsoft.PowerShell.PlatyPS.New-MarkdownModuleFile)

## Next steps

- [Edit Markdown help files](step-2-edit-markdown-help.md)

---
description: Use Microsoft.PowerShell.PlatyPS to update Markdown help files.
ms.date: 10/07/2025
title: Update Markdown help files using Microsoft.PowerShell.PlatyPS
---
# Update Markdown help files using Microsoft.PowerShell.PlatyPS

During the lifecycle of a PowerShell module, you might add new commands and parameter or change
existing parameters. When you release a new version of the module, you should update the Markdown
help files for the module to ensure that the help content is accurate and complete.

The `Update-MarkdownCommandHelp` and `Update-MarkdownModuleFile` commands update the Markdown files
to reflect changes in the module. To update the content you must first import the updated module
into the current session. The update commands import the existing Markdown files and update the
content based on the module loaded in the current session. The commands create backups of existing
content before making changes. You can compare the updated files to the backup files to see what
changed

You can use the update commands to convert older Markdown files to the PlatyPS format. The commands
can import Markdown files created by the previous version of PlatyPS (platyPS v0.14.2). However, the
format of the update content is written using the PlatyPS Markdown format.

## Update the command Markdown files

Use the `Update-MarkdownCommandHelp` command to update the command Markdown files. For example:

```powershell
Import-Module -Name 'YourModuleName' -Force # Load the updated module
Measure-PlatyPSMarkdown -Path ./docs/YourModuleName/*.md
    Where-Object Filetype -match 'CommandHelp' |
    Update-MarkdownCommandHelp -Path {$_.FilePath}
```

You must inspect every updated file to ensure that the content is correct and complete. If you are
converting older Markdown files to the PlatyPS format, there is a new `## ALIASES` section that you
must edit. This section is used to document any aliases that are defined for the command. This
section is optional and can be removed if there are no aliases. You also need to add any new
examples and document any new parameters.

## Update the module Markdown file

After you have completed editing and testing the command Markdown files, you can update the module
Markdown file using the `Update-MarkdownModuleFile` command. For example:

```powershell
Measure-PlatyPSMarkdown -Path ./docs/YourModuleName/*.md |
    Where-Object Filetype -match 'CommandHelp' |
    Import-MarkdownCommandHelp -Path {$_.FilePath} |
    Update-MarkdownModuleFile -Path ./docs/YourModuleName/YourModuleName.md
```

Be sure to inspect the update module file to ensure that the content is correct and complete.

## Comparing the changes with the backup files

The `Update-MarkdownCommandHelp` command adds new information to the existing command Markdown
files, but is conservative about changing existing content. Any new information that is added to the
the Markdown contains placeholder strings that you must replace with accurate information. Also,
there are items in the help files that can't be updated accurately. For example:

- PlatyPS commands get output type information by inspecting the command using `Get-Command`.
  However, if the command author didn't define output types, the output type information is
  incomplete. You can add output type information in the Markdown file. `Update-MarkdownCommandHelp`
  only adds output type information that it can verify, but it doesn't remove any existing output
  type information.

- Similarly, some parameters allow you to use wildcard expressions. If the command author added the
  `[SupportsWildcards()]` attribute to the parameter, that information is properly reflected in the
  markdown file. However, it's very common for command authors to omit the attribute. You can change
  the parameter information in the Markdown file to indicate that wildcards are supported. You need
  to ensure the updated information is correct.

For best results, use a file comparison tool to compare the updated files with the backup files. You
can do side-by-side comparisons using Visual Studio Code or a comparison tool like
[Beyond Compare](https://www.scootersoftware.com/).

When you have completed the updates, you can delete the backup files.

## Next steps

The following article describes the structure of the Markdown files and how to ensure that the
content is follows the expected format.

- [Edit Markdown help files](step-2-edit-markdown-help.md)

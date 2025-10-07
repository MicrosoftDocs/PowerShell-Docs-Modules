---
description: This article describes the types of help available in PowerShell.
ms.date: 10/09/2025
title: Types of help in PowerShell
---
# Types of help in PowerShell

The PowerShell help system supports two kinds of help.

- Conceptual help articles that describe concepts and use case scenarios.
- Command help articles that describe the syntax and usage of cmdlets, functions, and scripts.

The PlatyPS module helps you create and package PowerShell help files for your modules.

## Conceptual ("About") help text files

Conceptual ("about") Help articles describe the module, its members (such as commands and
variables), and explains how the members can be used together to perform tasks. The **About** help
articles are plain text files. The PlatyPS module doesn't help you create these files, but it can
package them with the command help files for modules that support updateable help.

For more information about creating conceptual help articles, see
[Writing Help for PowerShell Modules][04].

## Command help articles

Command help articles describe the syntax and usage of cmdlets, functions, and scripts. Command help
can be implemented in two ways:

- Comment-based help embedded in the script or function.
- XML-based help stored in an external XML file.

### Comment-based command help

For PowerShell scripts and functions, you can write comment-based help directly in the source file
of the script or function. Comment-based help uses special comment keywords that the PowerShell
recognizes. PowerShell extracts the comment-based help from the script or function for presentation
by the `Get-Help` cmdlet. For more information about writing comment-based help articles, see the
following articles:

- [about_Comment_Based_Help][01].
- [Writing Comment-Based Help][03]

### XML-based command help

The PowerShell help system also supports the help files written in the Microsoft Assistance Markup
Language (MAML) format. MAML is an XML-based schema used to create help documentation. MAML is the
only way to create help for cmdlets that are implemented in binary modules. Also, this is the format
required for modules that support updateable help.

You can use MAML to create help for scripts and functions. However, comment-based help takes
precedence over XML-based help when both types of help are present, unless you use the
`.EXTERNALHELP` comment keyword. When the `.EXTERNALHELP` comment keyword is present, it takes
precedence over comment-based help, even when `Get-Help` can't find a help file specified in the
`.EXTERNALHELP` comment. For more information about writing XML-based help articles, see
[How to create the cmdlet help file][02].

Handwriting MAML is tedious and error-prone. The PlatyPS module allows you to write your command
documentation in Markdown then compile it into the MAML format. For information about using PlatyPS,
see [Create new Markdown help using PlatyPS][05].

<!-- link references -->
[01]: /powershell/module/microsoft.powershell.core/about/about_comment_based_help
[02]: /powershell/scripting/developer/help/how-to-create-the-cmdlet-help-file
[03]: /powershell/scripting/developer/help/writing-comment-based-help-topics
[04]: /powershell/scripting/developer/help/writing-help-for-windows-powershell-modules#types-of-module-help
[05]: step-1-create-new-markdown-help.md

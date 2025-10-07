---
description: Overview of the PlatyPS module.
ms.date: 10/09/2025
title: PlatyPS overview
---
# PlatyPS overview

**PlatyPS** is the primary tool for creating the PowerShell help displayed using `Get-Help`.
PowerShell help files are writting in [Microsoft Assistance Markup Language][04] (MAML) format.
MAML defines an XML schema for the structure of help files.

There are two major versions of PlatyPS.

- **Microsoft.PowerShell.PlatyPS** v1.0.1 is the supported version of PlatyPS. This version is a
  complete rewrite in C# leveraging [markdig][02] for parsing Markdown. This release includes
  several improvements:
  - Provides a more accurate description of a PowerShell cmdlet and its parameters
  - Increased performance - processes 1000s of Markdown files in seconds
  - Creates an object model of the help file that you can manipulate in memory
  - Provides cmdlets that you can chain together to perform complex operations
  - Defines a new Markdown schema that includes all elements needed for `Get-Help`, plus information
    that was previously unavailable.
  - Provide automatic conversion of existing Markdown (using the old schema) to new objects,
    enabling you to export to new Markdown, YAML, or MAML.
- **platyPS** v0.14.2 is the original implementation of PlatyPS. This version is no longer
  supported.

## Benefits of using PlatyPS

Prior to **PlatyPS**, the help files were hand written with limited help from existing tools and
editors. **PlatyPS** simplifies the process by allowing you to write the help files in Markdown and
then convert it to MAML.

[Markdown][03] is easy to learn, widely used in the open source community, and supported by many
editors including [Visual Studio Code][01]. Markdown is also easy to convert to other formats such
as HTML and PDF. You can use these Markdown files to create MAML help files and to create HTML pages
for a website.

## Get started with PlatyPS

Before getting started with PlatyPS, you should understand the types of help supported by
PowerShell. For more information, see [Types of help in PowerShell][11].

Creating help files with PlatyPS is a four-step process:

1. [Create new][06] or [update existing][07] Markdown help files.
1. [Edit the Markdown help][08] files to add descriptions and examples.
1. [Test the Markdown help][09] files to ensure they render correctly.
1. [Convert and publish][10] the help files.

<!-- link references -->
[01]: https://code.visualstudio.com
[02]: https://github.com/xoofx/markdig
[03]: https://wikipedia.org/wiki/Markdown
[04]: https://wikipedia.org/wiki/Microsoft_Assistance_Markup_Language
[06]: step-1-create-new-markdown-help.md
[07]: step-1-update-markdown-help.md
[08]: step-2-edit-markdown-help.md
[09]: step-3-test-markdown-help.md
[10]: step-4-convert-publish-help.md
[11]: types-of-help.md

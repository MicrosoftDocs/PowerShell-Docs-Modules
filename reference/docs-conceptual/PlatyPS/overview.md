---
description: Overview of the PlatyPS module
ms.date: 06/28/2023
title: PlatyPS overview
---
# PlatyPS overview

**PlatyPS** is the primary tool for creating the PowerShell help displayed using `Get-Help`.
PowerShell help files are stored in an XML format known as
[Microsoft Assistance Markup Language][06] (MAML). Prior to **PlatyPS**, the help files were hand
authored using complex tool chains. [Markdown][05] is widely used in the open source community,
supported by many editors including [Visual Studio Code][01], and easier to author. **PlatyPS**
simplifies the process by allowing you to write the help files in Markdown and then converted to
MAML.

There are two major versions of PlatyPS.

- **platyPS** v0.14.2 is the current version of PlatyPS that's used to create PowerShell help files
  in Markdown format.
- **Microsoft.PowerShell.PlatyPS** v1.0.0-preview1 is the new version of PlatyPS. This version is a
  complete rewrite in C# leveraging [markdig][04] for parsing Markdown. This release includes
  several improvements:
  - Provides a more accurate description of a PowerShell cmdlet and its parameters
  - Increased performance - processes 1000s of Markdown files in seconds
  - Creates an object model of the help file that you can manipulate in memory
  - Provides cmdlets that you can chain together to perform complex operations
  - Defines a new Markdown schema that includes all elements needed for `Get-Help`, plus information
    that was previously unavailable.
  - Provide automatic conversion of existing Markdown (using the old schema) to new objects,
    enabling you to export to new Markdown, YAML, or MAML.

<!-- link references -->
[01]: https://code.visualstudio.com
[04]: https://github.com/xoofx/markdig
[05]: https://wikipedia.org/wiki/Markdown
[06]: https://wikipedia.org/wiki/Microsoft_Assistance_Markup_Language
[07]: https://www.powershellgallery.com/packages/Microsoft.PowerShell.PlatyPS
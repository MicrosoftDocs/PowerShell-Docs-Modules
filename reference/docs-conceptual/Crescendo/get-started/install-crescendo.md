---
description: How to install the Crescendo module.
ms.date: 08/23/2023
title: Installing Crescendo
---
# Install the Crescendo module

Requirements:

**Microsoft.PowerShell.Crescendo** requires PowerShell 7.0 or higher.

Crescendo can create modules that run on Windows PowerShell 5.1 and newer.

To install using **PowerShellGet 2.x**:

```powershell
# Install the current release
Install-Module Microsoft.PowerShell.Crescendo -Force
# Install the preview release
Install-Module Microsoft.PowerShell.Crescendo -AllowPrerelease -Force
```

To install using **Microsoft.PowerShell.PSResourceGet** (beta):

```powershell
# Install the current release
Install-PSResource Microsoft.PowerShell.Crescendo -Reinstall
# Install the preview release
Install-PSResource Microsoft.PowerShell.Crescendo -Prerelease -Reinstall
```

The **Force** or **Reinstall** parameters are only necessary when you have an older version of
Crescendo installed. However, these parameters work whether you have a previous version or not.

The Crescendo module includes full help content. To install the latest help, run the following
command:

```powershell
Update-Help -Module Microsoft.PowerShell.Crescendo -Force
```

Using the **Force** parameter ensures that you get the latest available help content.

## Next step

> [!div class="nextstepaction"]
> [Choose the command-line tool to wrap][01]

<!-- link references -->
[01]: choose-command-line-tool.md

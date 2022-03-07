---
description: How to install the Crescendo module.
ms.date: 03/07/2022
title: Installing Crescendo
---
# Install the Crescendo module

To install using **PowerShellGet 2.x**:

```powershell
Install-Module Microsoft.PowerShell.Crescendo -Force
```

To install using **PowerShellGet 3.0** (beta):

```powershell
Install-PSResource Microsoft.PowerShell.Crescendo -Reinstall
```

The **Force** or **Reinstall** parameters are only necessary when you have an older version of
Crescendo installed. However, these parameters work whether you have a previous version or not.

The Crescendo module includes full help content. However, to ensure you have the latest help, run
the following command:

```powershell
Update-Help Microsoft.PowerShell.Crescendo -Force
```

Using the **Force** parameter ensures that you get the latest available help content.

## Next step

> [!div class="nextstepaction"]
> [Choose the command-line tool to wrap](choose-command-line-tool.md)

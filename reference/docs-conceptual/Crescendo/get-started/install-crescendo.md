---
description: How to install the Crescendo module.
ms.date: 02/25/2022
title: Installing Crescendo
---
# Install the Microsoft.PowerShell.Crescendo module

To install PowerShellGet:

```powershell
Install-Module Microsoft.PowerShell.Crescendo -AllowClobber -Force
```

To install PowerShellGet 3.0 (beta):

```powershell
Install-PSResource Microsoft.PowerShell.Crescendo -Reinstall
```

The **AllowClobber**, **Force**, or **Reinstall** parameters are only necessary when you have an
older version of Crescendo installed. However, these parameters work whether you have a previous
version or not.

Like the modules that ship with PowerShell, the Crescendo module does not include help. Run the
following command to get the latest help content:

```powershell
Update-Help Microsoft.PowerShell.Crescendo -Force
```

Using the **Force** parameter ensures that you get the latest available help content.

## Next step

> [!div class="nextstepaction"]
> [Choose the native command to wrap](choose-native-command.md)

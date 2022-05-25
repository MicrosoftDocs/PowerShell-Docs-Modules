---
description: How to install and use the SecretManagement and SecretStore modules
ms.date: 05/24/2022
title: Get started with the SecretStore module
---
# Get started with the SecretStore module

The **SecretManagement** and **SecretStore** modules are available from the PowerShell Gallery and
can be installed using **PowerShellGet** commands.

```powershell
Install-Module Microsoft.PowerShell.SecretManagement
Install-Module Microsoft.PowerShell.SecretStore
```

Once you have installed the modules you can load the modules and begin using or creating new secrets.

```powershell
Import-Module Microsoft.PowerShell.SecretManagement
Import-Module Microsoft.PowerShell.SecretStore
```

## Create a vault and add a secret

First you must register the vault. The **Name** parameter is a friendly name and can be anything you
choose.

```powershell
Register-SecretVault -Name SecretStore -ModuleName Microsoft.PowerShell.SecretStore -DefaultVault
```

Now you can create a secret.

```powershell
Set-Secret -Name TestSecret -Secret "TestSecretPassword"
```

The first time you access the vault you must provide a password for the new vault. This password is
used to lock and unlock the vault.

```Output
Vault SecretStore requires a password.
Enter password:
********
Enter password again for verification:
********
```

Run `Get-Secret` to retrieve the secret. Using the **AsPlainText** switch returns the secret as an
unencrypted string.

```powershell
PS> Get-Secret -Name TestSecret -AsPlainText
TestSecretPassword
```

To a list of your secrets, can run:

```powershell
PS> Get-SecretInfo

Name       Type   VaultName
----       ----   ---------
TestSecret String SecretStore
```

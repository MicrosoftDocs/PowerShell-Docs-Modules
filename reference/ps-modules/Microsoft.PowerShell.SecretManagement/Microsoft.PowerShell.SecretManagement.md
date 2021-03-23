---
Module Name: Microsoft.PowerShell.SecretManagement
Module Guid: a5c858f6-4a8e-41f1-b1ee-0ff8f6ad69d3
ms.date: 03/16/2021
Download Help Link: https://aka.ms/ps-modules-help
Help Version: 0.1.0.0
Locale: en-US
---

# Microsoft.PowerShell.SecretManagement Module

## Description

PowerShell SecretManagement module provides a convenient way for a user to store and retrieve
secrets. The secrets are stored in SecretManagement extension vaults. An extension vault is a
PowerShell module that has been registered to SecretManagement, and exports five module functions
required by SecretManagement. An extension vault can store secrets locally or remotely. Extension
vaults are registered to the current logged in user context, and will be available only to that
user.

> [!NOTE]
> This module is supported under traditional Microsoft support agreements, including [paid support](https://support.microsoft.com/hub/4343728/support-for-business),
[Microsoft Enterprise Agreements](https://www.microsoft.com/licensing/licensing-programs/enterprise?rtc=1&activetab=enterprise-tab%3aprimaryr2), and
[Microsoft Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx).
You can also pay for [assisted support](https://support.microsoft.com/assistedsupportproducts) for PowerShell
by filing a support request for your problem. Please file issues in the source repository using the **This
> product** button in the Feedback section at the bottom of the page.

## Microsoft.PowerShell.SecretManagement Cmdlets

### [Get-Secret](Get-Secret.md)
Finds and returns a secret by name from registered vaults.

### [Get-SecretInfo](Get-SecretInfo.md)
Finds and returns secret metadata information of one or more secrets.

### [Get-SecretVault](Get-SecretVault.md)
Finds and returns registered vault information.

### [Register-SecretVault](Register-SecretVault.md)
Registers a SecretManagement extension vault module for the current user.

### [Remove-Secret](Remove-Secret.md)
Removes a secret from a specified registered extension vault.

### [Set-Secret](Set-Secret.md)
Adds a secret to a SecretManagement registered vault.

### [Set-SecretVaultDefault](Set-SecretVaultDefault.md)
Sets the provided vault name as the default vault for the current user.

### [Test-SecretVault](Test-SecretVault.md)
Runs an extension vault self test.

### [Unregister-SecretVault](Unregister-SecretVault.md)
Un-registers an extension vault from SecretManagement for the current user.

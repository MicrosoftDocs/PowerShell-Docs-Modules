---
description: Overview of the SecretManagement and SecretStore modules
ms.date: 05/24/2022
title: Overview of the SecretManagement and SecretStore modules
---
# Overview of the SecretManagement and SecretStore modules

The **SecretManagement** module helps users manage secrets by providing a common set of cmdlets that
interface with secrets vaults. **SecretManagement** provides an extensible model where local and remote
vaults can be registered for use. This allows you to separate the specific details for accessing and
managing the vault from your scripts that need secrets.

Since **SecretManagement** is a module abstraction layer in PowerShell, it becomes useful once
extension vaults are registered. There are trade-offs between security, usability, and specificity
for any vault so it is up to the user to configure **SecretManagement** to integrate with the vaults
that best match their requirements, as well as to assess the extent to which they trust any vault
extensions not developed by Microsoft.

**SecretManagement** does not impose authentication requirements for extension vaults. This allows
each individual vault to provide its own mechanism. Some may require a password or token, while
others may leverage current account credentials.

**SecretManagement** enables the following key scenarios:

- Sharing a script across your organization without knowing the local vault of all the users
- Running your deployment script in local, test, and production environments with the change of only
  a single parameter, **Vault**
- Changing the backend of the authentication method to meet specific security or organizational
  needs without needing to update all my scripts

## Extension Vault Ecosystem

**SecretManagement** becomes useful once you install and register extension vaults. Extension
vaults, which are PowerShell modules with a particular structure, provide the connection between the
**SecretManagement** module and any local or remote Secret Vault.

**SecretStore** is a cross-platform extension module that implements a local vault. The
**SecretStore** vault stores secrets, locally in a file, for the current user. It uses .NET Core
cryptographic APIs to encrypt file contents. This extension vault works on all platforms that
support PowerShell 7.

### Discovering and Installing Vault Extensions

To find extension vault modules, search the PowerShell Gallery for the
[SecretManagement tag](https://www.powershellgallery.com/packages?q=Tags%3A%22SecretManagement%22).

Some community vault extensions that are available:

- [Azure KeyVault](https://www.powershellgallery.com/packages/Az.KeyVault) (Microsoft Owned)
- [KeePass](https://www.powershellgallery.com/packages/SecretManagement.KeePass)
- [LastPass](https://www.powershellgallery.com/packages/SecretManagement.LastPass)
- [Hashicorp Vault](https://www.powershellgallery.com/packages/SecretManagement.Hashicorp.Vault.KV)
- [KeyChain](https://www.powershellgallery.com/packages/SecretManagement.KeyChain)
- [CredMan](https://www.powershellgallery.com/packages/SecretManagement.JustinGrote.CredMan)

## Community feedback and support

Community feedback has been essential to the iterative development of these modules. To file issues
or get support for the SecretManagement interface or vault development experience please use the
[SecretManagement](https://github.com/PowerShell/SecretManagement/issues) repository. For issues
with the SecretStore module please use the
[SecretStore](https://github.com/PowerShell/SecretStore/issues) repository.

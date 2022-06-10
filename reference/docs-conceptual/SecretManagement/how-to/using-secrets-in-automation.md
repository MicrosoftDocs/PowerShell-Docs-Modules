---
description:
ms.date: 05/24/2022
title: Using the SecretStore in automation
---
# Using the SecretStore in automation

This is an example of automation script that installs and configures the
**Microsoft.PowerShell.SecretStore** module without user prompting. The configuration requires a
password and sets user interaction to `None`, so that **SecretStore** never prompts the user. The
configuration also requires a password, and the password is passed in as a SecureString object. The
`-Confirm:false` parameter is used so that PowerShell does not prompt for confirmation.

```powershell
Install-Module -Name Microsoft.PowerShell.SecretStore -Repository PSGallery -Force
$password = Import-CliXml -Path $securePasswordPath

$storeConfiguration = @{
    Authentication = 'Password'
    PasswordTimeout = 3600 # 1 hour
    Interaction = 'None'
    Password = $password
    Confirm = $false
}
Set-SecretStoreConfiguration @storeConfiguration
```

The **SecretStore** password must be provided in a secure fashion. Here the password is being
imported from a file that was encrypted using Windows Data Protection (DPAPI). This is a
Windows-only solution, but another option is to use a secure variable provided by CI system like
GitHub Actions.

Next, the **SecretManagement** module is installed and the **SecretStore** module registered so that
the SecretStore secrets can be managed.

The `Unlock-SecretStore` cmdlet is used to unlock the **SecretStore** for this session. The password
timeout was configured for 1 hour and **SecretStore** will remain unlocked in the session for that
amount of time, after which it will need to be unlocked again before secrets can be accessed.

```powershell
Install-Module -Name Microsoft.PowerShell.SecretManagement -Repository PSGallery -Force
Register-SecretVault -Name SecretStore -ModuleName Microsoft.PowerShell.SecretStore -DefaultVault

Unlock-SecretStore -Password $password
```

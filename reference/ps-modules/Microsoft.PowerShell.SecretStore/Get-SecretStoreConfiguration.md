---
external help file: Microsoft.PowerShell.SecretStore.dll-Help.xml
Module Name: Microsoft.PowerShell.SecretStore
ms.date: 03/16/2021
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.secretstore/get-secretstoreconfiguration?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Get-SecretStoreConfiguration

## SYNOPSIS
Returns SecretStore configuration information.

## SYNTAX

```
Get-SecretStoreConfiguration [<CommonParameters>]
```

## DESCRIPTION

This cmdlet reads the SecretStore configuration file and returns the defined settings.

## EXAMPLES

### Example 1

```powershell
PS C:\> Get-SecretStoreConfiguration

      Scope Authentication PasswordTimeout Interaction
      ----- -------------- --------------- -----------
CurrentUser       Password             900      Prompt
```

This example shows the current configuration for **SecretStore**. It is configured for the current
user. It requires a password for initial access in a session and prompts the user for it in an
interactive session. After fifteen minutes, the password is required again for access.

## PARAMETERS

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### Microsoft.PowerShell.SecretStore.SecureStoreConfig

## NOTES

The `AllUsers` **Scope** is not supported. The **Scope** is always `CurrentUser`.

## RELATED LINKS

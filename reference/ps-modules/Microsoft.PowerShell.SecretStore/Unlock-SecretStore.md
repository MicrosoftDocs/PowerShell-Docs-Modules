---
external help file: Microsoft.PowerShell.SecretStore.dll-Help.xml
Module Name: Microsoft.PowerShell.SecretStore
ms.date: 05/23/2025
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.secretstore/unlock-secretstore?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Unlock-SecretStore

## SYNOPSIS
Unlocks SecretStore with the provided password.

## SYNTAX

```
Unlock-SecretStore -Password <SecureString> [-PasswordTimeout <Int32>] [<CommonParameters>]
```

## DESCRIPTION

This cmdlet unlocks the **SecretStore** for the current user with the provided password. It can be
used to unlock the **SecretStore** when the configuration requires a password and the prompt
configuration option is disabled. The **SecretStore** remains unlocked in the session until its
configured password timeout elapses.

## EXAMPLES

### Example 1

```powershell
PS C:\> Get-Secret Secret1 -Vault LocalStore
Get-Secret: A valid password is required to access the Microsoft.PowerShell.SecretStore vault.
Get-Secret: The secret Secret1 wasn't found.

PS C:\> Unlock-SecretStore

cmdlet Unlock-SecretStore at command pipeline position 1
Supply values for the following parameters:
SecureStringPassword: *******

PS C:\> Get-Secret Secret1 -Vault LocalStore
System.Security.SecureString
```

In this example, `Get-Secret` fails to retrieve `Secret1` because the **SecretStore** vault is
locked. `Unlock-SecretStore` unlocks the vault. The cmdlet prompts for the password because the
**Password** parameter wasn't specified. With the vault unlocked, `Get-Secret` returns `Secret1` as
a **SecureString** object.

## PARAMETERS

### -Password

Specifies the password needed to access the **SecretStore**.

```yaml
Type: System.Security.SecureString
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -PasswordTimeout

Specifies how many seconds the **SecretStore** remains unlocked after authenticating with a
password. This parameter overrides the configured password timeout value. After the timeout has
elapsed, the current password value is invalidated for the session. Accessing the **SecretStore**
after the timeout requires the password again.

```yaml
Type: System.Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.Security.SecureString

## OUTPUTS

### None

## NOTES

## RELATED LINKS

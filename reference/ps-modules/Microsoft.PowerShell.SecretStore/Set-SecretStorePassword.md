---
external help file: Microsoft.PowerShell.SecretStore.dll-Help.xml
Module Name: Microsoft.PowerShell.SecretStore
ms.date: 05/23/2025
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.secretstore/set-secretstorepassword?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Set-SecretStorePassword

## SYNOPSIS
Replaces the current SecretStore password with a new one.

## SYNTAX

### NoParameterSet (Default)

```
Set-SecretStorePassword [<CommonParameters>]
```

### ParameterSet
```
Set-SecretStorePassword -NewPassword <SecureString> [-Password <SecureString>] [<CommonParameters>]
```

## DESCRIPTION

This cmdlet updates the password for **SecretStore**.

## EXAMPLES

### Example 1

```powershell
PS C:\> Set-SecretStorePassword
Old password
Enter password:
*******
New password
Enter password:
*******
Enter password again for verification:
*******
```

This example runs the command with no parameter arguments. The user is first prompted for the old
password. And then prompted for the new password twice for verification.

### Example 2

```powershell
PS C:\> Set-SecretStorePassword -NewPassword $newPassword -Password $oldPassword
```

This example runs the command passing in both the current store password and the new password to be
set.

## PARAMETERS

### -NewPassword

Specifies the new password for accessing the **SecretStore**. If this parameter isn't specified and
the cmdlet is run in an interactive session, it prompts the user for the value. If this parameter is
not specified and the cmdlet is run in a non-interactive session, it returns an error.

```yaml
Type: System.Security.SecureString
Parameter Sets: ParameterSet
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Password

Existing password needed to unlock the store. This can be ignored if the store doesn't currently use
a password.

Specifies the existing password for accessing the **SecretStore**. If the **SecretStore** isn't
configured to require a password, this parameter is ignored.

If the **SecretStore** is configured to require a password, this parameter isn't specified, and the
cmdlet is run in an interactive session, it prompts the user for the value. If the **SecretStore**
is configured to require a password, this parameter isn't specified and the cmdlet is run in a
non-interactive session, it returns an error.

```yaml
Type: System.Security.SecureString
Parameter Sets: ParameterSet
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

### None

## OUTPUTS

### None

## NOTES

## RELATED LINKS

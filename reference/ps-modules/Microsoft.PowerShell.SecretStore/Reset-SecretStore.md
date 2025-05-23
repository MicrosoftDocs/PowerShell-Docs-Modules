---
external help file: Microsoft.PowerShell.SecretStore.dll-Help.xml
Module Name: Microsoft.PowerShell.SecretStore
ms.date: 05/23/2025
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.secretstore/reset-secretstore?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Reset-SecretStore

## SYNOPSIS
Resets the SecretStore by deleting all secret data and configuring the store with default options.

## SYNTAX

```
Reset-SecretStore [-Scope <SecureStoreScope>] [-Authentication <Authenticate>]
 [-Password <SecureString>] [-PasswordTimeout <Int32>] [-Interaction <Interaction>] [-PassThru]
 [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This cmdlet completely resets the **SecretStore** by deleting all secret data it may contain, and
resetting configuration options to their default values. It's intended to be used only if a required
password is lost, or data files become corrupted so that **SecretStore** no longer functions and
secret data can't be accessed.

The default configuration options can be overridden by specifying individual command configuration
option parameters.

## EXAMPLES

### Example 1

```powershell
PS C:\> Reset-SecretStore -PassThru
WARNING: !!This operation will completely remove all SecretStore module secrets and reset
configuration settings to default values!!

Reset SecretStore
Are you sure you want to erase all secrets in SecretStore and reset configuration
settings to default?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
Creating a new Microsoft.PowerShell.SecretStore vault. A password is required by
the current store configuration.
Enter password:
********
Enter password again for verification:
********

      Scope Authentication PasswordTimeout Interaction
      ----- -------------- --------------- -----------
CurrentUser       Password             900      Prompt
```

This example resets the **SecretStore** for the current user. The cmdlet warns about the
consequences of this action and prompts the user for confirmation before continuing. After
confirmation, the cmdlet deletes all secrets and sets every configuration setting to its default
value.

## PARAMETERS

### -Authentication

Specifies how to authenticate access to the **SecretStore**. The value must be `Password` or `None`.
If specified as `None`, the cmdlet enables access to the **SecretStore** without a password. The
default authentication is `Password`.

> [!CAUTION]
> Setting the **Authentication** to `None` is less secure than `Password`. Specifying `None` may be
> useful for testing scenarios but shouldn't be used with important secrets.

```yaml
Type: Microsoft.PowerShell.SecretStore.Authenticate
Parameter Sets: (All)
Aliases:
Accepted values: None, Password

Required: False
Position: Named
Default value: Password
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Indicates that the cmdlet should reset the **SecretStore** without prompting. By default, the cmdlet
warns about the impact of resetting the **SecretStore** and prompts the user for confirmation.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Interaction

Specifies whether the **SecretStore** should prompt a user when they access it. If the value is
`Prompt`, the user is prompted for their password in interactive sessions when required. If the
value is `None`, the user isn't prompted for a password. If the value is `None` and a password is
required, the cmdlet requiring the password throws a
**Microsoft.PowerShell.SecretStore.PasswordRequiredException** error.

```yaml
Type: Microsoft.PowerShell.SecretStore.Interaction
Parameter Sets: (All)
Aliases:
Accepted values: None, Prompt

Required: False
Position: Named
Default value: Prompt
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru

Indicates that the cmdlet should return the **SecretStore** configuration after resetting it. By
default, the cmdlet returns no output.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Password

Specifies the password the **SecretStore** should require for access. If **Authentication** is
specified as `None`, the cmdlet returns an error. If **Authentication** is `Password` and this
parameter isn't specified, the cmdlet prompts the user to enter the password securely.

```yaml
Type: System.Security.SecureString
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PasswordTimeout

Specifies how long the **SecretStore** remains unlocked after authenticating with a password. When
the timeout value is reached, the current password value is invalidated for the session. Accessing
the **SecretStore** after the timeout requires the password again.

```yaml
Type: System.Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: 900
Accept pipeline input: False
Accept wildcard characters: False
```

### -Scope

Specifies the context the **SecretStore** is configured for. Only `CurrentUser` is currently
supported.

```yaml
Type: Microsoft.PowerShell.SecretStore.SecureStoreScope
Parameter Sets: (All)
Aliases:
Accepted values: CurrentUser, AllUsers

Required: False
Position: Named
Default value: CurrentUser
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm

Prompts you for confirmation before running the cmdlet.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Shows what would happen if the cmdlet runs. The cmdlet isn't run.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
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

### Microsoft.PowerShell.SecretStore.SecureStoreConfig

## NOTES

## RELATED LINKS

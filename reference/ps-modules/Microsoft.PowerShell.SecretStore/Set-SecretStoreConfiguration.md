---
external help file: Microsoft.PowerShell.SecretStore.dll-Help.xml
Module Name: Microsoft.PowerShell.SecretStore
ms.date: 03/16/2021
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.secretstore/set-secretstoreconfiguration?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Set-SecretStoreConfiguration

## SYNOPSIS
Configures the **SecretStore**.

## SYNTAX

### PARAMETERSet (Default)

```
Set-SecretStoreConfiguration [-Scope <SecureStoreScope>] [-Authentication <Authenticate>]
 [-PasswordTimeout <Int32>] [-Interaction <Interaction>] [-Password <SecureString>] [-PassThru] [-WhatIf]
 [-Confirm] [<CommonParameters>]
```

### DefaultParameterSet

```
Set-SecretStoreConfiguration [-Default] [-Password <SecureString>] [-PassThru] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

## DESCRIPTION

This cmdlet configures the **SecretStore** for the current user.

## EXAMPLES

### Example 1

```powershell
PS C:\> Set-SecretStoreConfiguration -Default

Confirm
Are you sure you want to perform this action?
Performing the operation "Changes local store configuration" on target "SecretStore module local store".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y

      Scope Authentication PasswordTimeout Interaction
      ----- -------------- --------------- -----------
CurrentUser       Password             900      Prompt
```

This example restores the **SecretStore** to its default configuration.

## PARAMETERS

### -Authentication

Specifies how to authenticate access to the **SecretStore**. The value must be `Password` or `None`.
If specified as `None`, the cmdlet enables access to the **SecretStore** without a password. The
default authentication is `Password`.

> [!CAUTION]
> Setting the **Authentication** to `None` is less secure than `Password`. Specifying `None` may be
> useful for testing scenarios but should not be used with important secrets.

```yaml
Type: Authenticate
Parameter Sets: ParameterSet
Aliases:

Required: False
Position: Named
Default value: Password
Accept pipeline input: False
Accept wildcard characters: False
```

### -Default

Indicates that the **SecretStore** should be set to its default configuration.

```yaml
Type: SwitchParameter
Parameter Sets: DefaultParameterSet
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru

Indicates that the cmdlet should return the **SecretStore** configuration after updating it. By
default, the cmdlet returns no output.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Password

Specifies the password needed to access the **SecretStore**. This parameter cannot be used to change
the existing password. To change the existing password, use `Set-SecretStorePassword`.

When this parameter is used with the **Authenticate** parameter to change the configuration for
authentication from `None` to `Password`, this parameter's value is set as the new password for the
**SecretStore**.

When this parameter is used with the **Authenticate** parameter to change the configuration for
authentication from `Password` to `None`, this parameter's value must be the current password for the
**SecretStore**. It is used to authorize the configuration change.

```yaml
Type: SecureString
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PasswordTimeout

Specifies how many seconds the **SecretStore** remains unlocked after authenticating with a
password. After the timeout has elapsed, the current password value is invalidated for the session.
Accessing the **SecretStore** after the timeout requires the password again.

```yaml
Type: Int32
Parameter Sets: ParameterSet
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Scope

Specifies the context the **SecretStore** is configured for. Only `CurrentUser` is currently
supported.

```yaml
Type: SecureStoreScope
Parameter Sets: ParameterSet
Aliases:
Accepted values: CurrentUser, AllUsers

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Interaction

Specifies whether the **SecretStore** should prompt a user when they access it. If the value is
`Prompt`, the user is prompted for their password in interactive sessions when required. If the
value is `None`, the user is not prompted for a password. If the value is `None` and a password is
required, the cmdlet requiring the password throws a
**Microsoft.PowerShell.SecretStore.PasswordRequiredException** error.

```yaml
Type: Interaction
Parameter Sets: ParameterSet
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm

Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Shows what would happen if the cmdlet runs. The cmdlet is not run.

```yaml
Type: SwitchParameter
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

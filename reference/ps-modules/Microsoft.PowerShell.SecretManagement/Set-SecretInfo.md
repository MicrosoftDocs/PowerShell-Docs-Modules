---
external help file: Microsoft.PowerShell.SecretManagement.dll-Help.xml
Module Name: Microsoft.PowerShell.SecretManagement
ms.date: 05/31/2022
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.secretmanagement/set-secretinfo?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Set-Secret

## SYNOPSIS
Adds or replaces additional secret metadata to a secret currently stored in a vault.

## SYNTAX

### SecureStringParameterSet (Default)

```
Set-Secret [-Name] <String> -SecureStringSecret <SecureString> [[-Vault] <String>]
 [[-Metadata] <Hashtable>] [-NoClobber] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### ObjectParameterSet

```
Set-Secret [-Name] <String> -Secret <Object> [[-Vault] <String>] [[-Metadata] <Hashtable>]
 [-NoClobber] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### SecretInfoParameterSet

```
Set-Secret -SecretInfo <SecretInformation> [-Vault] <String> [-NoClobber] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

## DESCRIPTION

This cmdlet adds additional metadata information to a stored secret. Metadata support is an optional
feature for an extension vault. If a vault does not support secret metadata, the cmdlet returns an
error.

Metadata is not stored securely in a vault. Metadata should not contain sensitive information.

## EXAMPLES

### Example 1

```powershell
Set-SecretInfo -Name Secret1 -Vault Vault1 -Metadata @{ Expiration = ([datetime]::new(2022, 5, 1)) }
Get-SecretInfo -Name Secret1 -Vault Vault1 | Select-Object Name,Metadata
```

```output
Name         Metadata
----         --------
Secret1 {[Expiration, 5/1/2022 12:00:00 AM]}
```

This example adds metadata to the `Secret1` secret stored in `Vault1` vault. `Get-SecretInfo`
retrieves the metadata for `Secret1` to show the added metadata.

### Example 2

```powershell
Set-SecretInfo -Name Secret2 -Vault Vault2 -Metadata @{ Expiration = ([datetime]::new(2022, 5, 1)) }
```

```output
Set-SecretInfo: Cannot set secret metadata Secret2. Vault Vault2 does not support secret metadata.
```

This example adds metadata to the `Secret2` secret stored in `Vault2` vault. However, `Vault2` does
not support metadata. The command fails and returns an error.

## PARAMETERS

### -Metadata

Specifies a **Hashtable** containing key-value pairs to associate with the secret in the vault. The
specified extension vault may not support secret metadata. If the vault does not support metadata,
the operation fails and returns an error. The values of any metadata in the hashtable must be one of
the following types:

- **string**
- **int**
- **DateTime**

Metadata is not stored securely in a vault. Metadata should not contain sensitive information.

```yaml
Type: Hashtable
Parameter Sets: SecureStringParameterSet, ObjectParameterSet
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name

Specifies the name of the secret to add metadata to. Wildcard characters (`*`) are not permitted.

```yaml
Type: String
Parameter Sets: SecureStringParameterSet, ObjectParameterSet
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoClobber

Indicates that the command should error if a secret with the same name already exists in the vault.
By default, this cmdlet updates the secret with the new value if it already exists.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Secret

Specifies the value of the secret. The object type must be one of the supported types:

- **Byte[]**
- **String**
- **SecureString**
- **PSCredential**
- **Hashtable**

```yaml
Type: Object
Parameter Sets: ObjectParameterSet
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -SecretInfo

Specifies a **SecretInformation** object describing a stored secret returned by `Get-SecretInfo`.
This enables copying secrets from one extension vault to another.

```yaml
Type: SecretInformation
Parameter Sets: SecretInfoParameterSet
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -SecureStringSecret

Specifies the value of the secret as a **SecretString** object.

```yaml
Type: SecureString
Parameter Sets: SecureStringParameterSet
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Vault

Specifies the name of the vault containing the secret to add or update the metadata for. Wildcard
characters (`*`) are not permitted. By default, this cmdlet looks for the secret in the current
user's default vault.

```yaml
Type: String
Parameter Sets: SecureStringParameterSet, ObjectParameterSet
Aliases:

Required: False (SecureStringParameterSet, ObjectParameterSet), True (SecretInfoParameterSet)
Position: 2
Default value: None
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
Default value: None
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

### System.Collections.Hashtable

## OUTPUTS

### None

## NOTES

## RELATED LINKS

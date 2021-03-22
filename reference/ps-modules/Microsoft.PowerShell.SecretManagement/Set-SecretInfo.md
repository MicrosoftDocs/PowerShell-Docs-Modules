---
external help file: Microsoft.PowerShell.SecretManagement.dll-Help.xml
Module Name: Microsoft.PowerShell.SecretManagement
ms.date: 03/16/2021
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.secretmanagement/set-secretinfo?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
wonline version:
---

# Set-Secret

## SYNOPSIS
Adds or replaces additional secret metadata to a secret currently stored in a vault.

## SYNTAX

### SecureStringParameterSet (Default)

```
Set-Secret [-Name] <String> -SecureStringSecret <SecureString> [[-Vault] <String>] [[-Metadata] <Hashtable>]
 [-NoClobber] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### ObjectParameterSet

```
Set-Secret [-Name] <String> -Secret <Object> [[-Vault] <String>] [[-Metadata] <Hashtable>] [-NoClobber]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

### SecretInfoParameterSet

```
Set-Secret -SecretInfo <SecretInformation> [-Vault] <String> [-NoClobber] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

## DESCRIPTION

This cmdlet adds additional secret metadata to a currently store secret. Metadata support is an
optional feature for an extension vault. An error will be thrown if a vault does not support secret
metadata.

Metadata is a **Hashtable** object containing Name/Value pairs. The value type is restricted to the
following:

- string
- int
- DateTime

Metadata is not stored securely in a vault. Metadata should not contain sensitive information.

## EXAMPLES

### Example 1

```powershell
PS C:\> Set-SecretInfo -Name Secret1 -Vault Vault1 -Metadata @{ Expiration = ([datetime]::new(2022, 5, 1)) }
PS C:\> Get-SecretInfo -Name Secret1 -Vault Vault1 | Select-Object Name,Metadata

Name         Metadata
----         --------
Secret1 {[Expiration, 5/1/2022 12:00:00 AM]}
```

This example adds metadata to the 'Secret1' secret stored in 'Vault1' vault. The metadata is then
retrieved for 'Secret1' using the `Get-SecretInfo` command.

### Example 2

```powershell
Set-SecretInfo -Name Secret2 -Vault Vault2 -Metadata @{ Expiration = ([datetime]::new(2022, 5, 1)) }
Set-SecretInfo: Cannot set secret metadata Secret2. Vault Vault2 does not support secret metadata.
```

This example adds metadata to the 'Secret2' secret stored in 'Vault2' vault. However, Vault2 does
not support metadata and an error is generated.

## PARAMETERS

### -Metadata

Hashtable containing Name/Value pair that are stored in the vault. The specified extension vault may
not support secret metadata, in which case the operation will fail. The metadata Name/Value value
type must be one of the following:

- string
- int
- DateTime

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

Name of secret for which the metadata is added

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

### -Vault

Optional name of vault to which the secret is added. If omitted, the secret will be added to the
default vault.

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

### -NoClobber

When used this parameter will cause an error if the secret metadata already exists.

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

A secret value to be added. The object type must be one of the supported types.

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

**SecretInformation** object that describes a vault secret.

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

A secret SecretString object to be added.

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

## NOTES

## RELATED LINKS

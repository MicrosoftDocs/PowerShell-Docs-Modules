---
external help file: Microsoft.PowerShell.SecretManagement.dll-Help.xml
Module Name: Microsoft.PowerShell.SecretManagement
ms.date: 05/31/2022
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.secretmanagement/set-secret?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Set-Secret

## SYNOPSIS
Adds a secret to a SecretManagement registered vault.

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

This cmdlet adds a secret value by name to a vault. If no vault name is specified the secret is
added to the default vault. If a secret with that name exists, it is overwritten. Additional data
can be included with the secret if supported by the extension vault.

The default parameter set takes a **SecureString** object. If you run the command without specifying
the secret value, the cmdlet prompts you to to enter a **SecureString**. The text of the string is
not visible in the console.

## EXAMPLES

### Example 1

```powershell
Set-Secret -Name Secret1 -Secret "SecretValue"
Get-Secret -Name Secret1
```

```output
System.Security.SecureString
```

This example adds a secret named `Secret1` with a plain text value of `SecretValue`. Since no vault
name was specified, the secret is added to the current user's default vault. `Get-Secret` shows
the secret was added.

### Example 2

```powershell
PS C:\> Set-Secret -Name Secret2 -Vault LocalStore

cmdlet Set-Secret at command pipeline position 1
Supply values for the following parameters:
SecureStringSecret: ***********

PS C:\> Get-Secret -Name Secret2
System.Security.SecureString
```

This example adds a secret named `Secret2` to the `LocalStore` vault. Since no secret value was
provided, the cmdlet prompts for a **SecureString** value. The console hides the string value as it
is typed. `Get-Secret` shows the secret was added.

### Example 3

```powershell
$Metadata = @{ Expiration = ([datetime]::new(2022, 5, 1)) }
Set-Secret -Name TargetSecret -Secret $targetToken -Vault LocalStore -Metadata $Metadata
Get-SecretInfo -Name TargetSecret | Select-Object Name,Metadata
```

```output
Name         Metadata
----         --------
TargetSecret {[Expiration, 5/1/2022 12:00:00 AM]}
```

This example adds a secret named `TargetSecret` to the `LocalStore` vault with metadata indicating
the secret's expiration date. `Get-SecretInfo` retrieves the metadata for the newly created secret.

### Example 4

```powershell
$Metadata = @{ Expiration = ([datetime]::new(2022, 5, 1)) }
Set-Secret -Name PublishSecret -Secret $targetToken -Vault LocalStore2 -Metadata $Metadata
```

```output
Set-Secret: Cannot store secret PublishSecret. Vault LocalStore2 does not support secret metadata.
```

This example adds a secret named `PublishSecret` to the `LocalStore2` vault with extra metadata.
However, vault `LocalStore2` does not support secret metadata and the operation returns an error.

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

Specifies the name of the secret to add or update. Wildcard characters (`*`) are not permitted.

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

Specifies the value of the secret. The object must be one of the supported types:

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

Specifies the name of the vault to add or update the secret in. Wildcard characters (`*`) are not
permitted. By default, the secret is added or updated in the current user's default vault.

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

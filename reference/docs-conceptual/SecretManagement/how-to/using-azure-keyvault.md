# Getting Started with Azure Key Vault

Setup a Key Vault in Azure.

https://docs.microsoft.com/en-us/azure/key-vault/keys/quick-create-powershell

The Azure Key Vault extension is available on the PowerShell Gallery beginning in
[Az.KeyVault module](https://www.powershellgallery.com/packages/Az.KeyVault/3.4.0) v3.3.0. This
vault extension uses a common authentication system with the rest of
[the Az PowerShell module](https://github.com/Azure/azure-powershell#--microsoft-azure-powershell),
and allows users to interact with an existing Azure Key Vault through the SecretManagement
interface.

To utilize Azure Key Vault with SecretManagement first ensure that you have
[the Az.KeyVault module](https://www.powershellgallery.com/packages/Az.KeyVault/3.4.0) installed
(`Install-Module Az.KeyVault`). You can then register the vault using your AZKVaultName and
SubscriptionID:

```powershell
Register-SecretVault -Module Az.KeyVault -Name AzKV -VaultParameters @{ AZKVaultName = $vaultName; SubscriptionId = $subID}
```

From there you can view the secrets you have (`Get-SecretInfo`), get secrets you may need
(`Get-Secret`), create and update secrets (`Set-Secret`), and remove secrets (`Remove-Secret`).

For any feature requests or support with the Azure Key Vault extension please refer to their
[GitHub repository](https://github.com/Azure/azure-powershell).

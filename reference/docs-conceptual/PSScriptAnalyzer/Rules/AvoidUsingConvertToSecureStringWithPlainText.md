---
description: Avoid Using SecureString With Plain Text
ms.date: 06/01/2026
ms.topic: reference
title: AvoidUsingConvertToSecureStringWithPlainText
---
# AvoidUsingConvertToSecureStringWithPlainText

**Severity Level: Error**

## Description

The use of the `AsPlainText` parameter with the `ConvertTo-SecureString` command bypasses encryption
and exposes sensitive information in memory as plain text, defeating the purpose of
[SecureString][01].

Instead, retrieve secure credentials through encrypted channels or use secure input methods like
`Read-Host -AsSecureString` to ensure sensitive data remains encrypted throughout its lifecycle.

## Recommendations

If you need to retrieve passwords programmatically without user interaction, consider using the
[SecretStore](https://www.powershellgallery.com/packages/Microsoft.PowerShell.SecretStore)
module from the PowerShell Gallery, which provides encrypted credential storage and retrieval.

## Example

### Noncompliant

```powershell
$UserInput = Read-Host 'Please enter your secure code'
$EncryptedInput = ConvertTo-SecureString -String $UserInput -AsPlainText -Force
```

### Compliant

```powershell
$SecureUserInput = Read-Host 'Please enter your secure code' -AsSecureString
```

<!-- link references -->

[01]: /dotnet/api/system.security.securestring

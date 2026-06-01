---
description: Avoid Using Plain Text For Password Parameter
ms.date: 06/01/2026
ms.topic: reference
title: AvoidUsingPlainTextForPassword
---
# AvoidUsingPlainTextForPassword

**Severity Level: Warning**

## Description

Password parameters that accept plaintext instead of `-AsSecureString` expose passwords and can
compromise your system's security. You should store passwords in the [SecureString][01] type
instead.

The following parameters are considered password parameters and aren't case sensitive:

- Password
- Pass
- Passwords
- Passphrase
- Passphrases
- PasswordParam

If you define a parameter with a name from the provided list, declare it with the **SecureString**
type.

## Example

### Noncompliant

```powershell
function Test-Script
{
    [CmdletBinding()]
    Param
    (
        [string]
        $Password
    )
    ...
}
```

### Compliant

```powershell
function Test-Script
{
    [CmdletBinding()]
    Param
    (
        [SecureString]
        $Password
    )
    ...
}
```

<!-- link references -->

[01]: /dotnet/api/system.security.securestring

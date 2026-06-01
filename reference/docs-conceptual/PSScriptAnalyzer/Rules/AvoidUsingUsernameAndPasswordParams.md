---
description: Avoid Using Username and Password Parameters
ms.date: 06/01/2026
ms.topic: reference
title: AvoidUsingUsernameAndPasswordParams
---
# AvoidUsingUsernameAndPasswordParams

**Severity Level: Error**

## Description

To standardize command parameters, credentials should be accepted as objects of type
**PSCredential**. Functions shouldn't use separate username or password parameters. Instead, change
the parameters to accept a single **PSCredential** object.

## Example

### Noncompliant

```powershell
function Test-Script
{
    [CmdletBinding()]
    Param
    (
        [String]
        $Username,
        [SecureString]
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
        [PSCredential]
        $Credential
    )
    ...
}
```

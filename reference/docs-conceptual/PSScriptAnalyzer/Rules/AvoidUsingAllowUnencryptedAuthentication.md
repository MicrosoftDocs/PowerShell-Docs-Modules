---
description: Avoid sending credentials and secrets over unencrypted connections
ms.date: 06/01/2026
ms.topic: reference
title: AvoidUsingAllowUnencryptedAuthentication
---
# AvoidUsingAllowUnencryptedAuthentication

**Severity Level: Warning**

## Description

The **AllowUnencryptedAuthentication** parameter of `Invoke-WebRequest` and `Invoke-RestMethod`
permits credentials and secrets to be transmitted over unencrypted connections, creating a security
risk. Avoid using this parameter unless you must maintain compatibility with legacy systems that
require unencrypted authentication.

To learn more, see [Invoke-RestMethod](xref:Microsoft.PowerShell.Utility.Invoke-RestMethod).

## Example

### Noncompliant

```powershell
Invoke-WebRequest foo -AllowUnencryptedAuthentication
```

### Compliant

```powershell
Invoke-WebRequest foo
```

---
description: Avoid global aliases.
ms.custom: PSSA v1.20.0
ms.date: 10/18/2021
ms.topic: reference
title: AvoidGlobalAliases
---
# AvoidGlobalAliases

**Severity Level: Warning**

## Description

Globally scoped aliases override existing aliases within the sessions with matching names. This name
collision can cause difficult to debug issues for consumers of modules and scripts.

To understand more about scoping, see `Get-Help about_Scopes`.

**NOTE** This rule is not available in PowerShell version 3 or 4 because it uses the
`StaticParameterBinder.BindCommand` API.

## How

Use other scope modifiers for new aliases.

## Example

### Wrong

```powershell
New-Alias -Name Name -Value Value -Scope "Global"
```

### Correct

```powershell
New-Alias -Name Name1 -Value Value
```

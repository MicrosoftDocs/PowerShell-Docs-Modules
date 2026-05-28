---
description: Avoid global aliases.
ms.date: 05/28/2026
ms.topic: reference
title: AvoidGlobalAliases
---
# AvoidGlobalAliases

**Severity Level: Warning**

## Description

Global aliases can override existing aliases in the current session. This override
creates naming conflicts that lead to hard to diagnose problems for module and script consumers.

This rule is not available in PowerShell version 3 or 4 because it uses the
`StaticParameterBinder.BindCommand` API.

Instead of using the Global scope, use other scope modifiers such as `Local` or `Process` when
creating new aliases. To learn more, see [about_Scopes][01].

## Example

### Noncompliant

```powershell
New-Alias -Name Name -Value Value -Scope Global
```

### Compliant

```powershell
New-Alias -Name Name1 -Value Value
```

<!-- link references -->

[01]: /powershell/module/microsoft.powershell.core/about/about_scopes

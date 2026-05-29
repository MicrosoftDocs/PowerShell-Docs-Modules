---
description: Avoid long lines
ms.date: 06/01/2026
ms.topic: reference
title: AvoidLongLines
---
# AvoidLongLines

**Severity Level: Warning**

## Description

This rule flags lines that exceed the configured maximum length, including leading spaces
(indentation). The default maximum line length is 120 characters. This rule is **disabled** by
default and must be explicitly enabled through rule configuration settings.

## Example 1

```
In this example of sample text, the maximum line length is using the default setting of not exceeding more than 120
characters.
```

## Example 2

```
In this example of sample text, the maximum line length is set to not exceed
more than 80 characters.
```

## Configure rule

```powershell
Rules = @{
    PSAvoidLongLines  = @{
        Enable     = $true
        MaximumLineLength = 120
    }
}
```

## Parameters

### Enable

Enables (`$true`) the rule during ScriptAnalyzer invocation.

### Disable

Disables (`$false`) the rule during ScriptAnalyzer invocation. Default value is `$false`.

### MaximumLineLength

This parameter is optional and is used to override the default maximum line length. This parameter
accepts an integer value. Default value is `120`.

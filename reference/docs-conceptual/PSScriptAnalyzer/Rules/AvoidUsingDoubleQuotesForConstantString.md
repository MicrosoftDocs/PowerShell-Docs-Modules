---
description: Avoid using double quotes if the string is constant.
ms.date: 06/01/2026
ms.topic: reference
title: AvoidUsingDoubleQuotesForConstantString
---
# AvoidUsingDoubleQuotesForConstantString

**Severity Level: Information**

## Description

Single quotes should be used when the value of a string is constant. A constant string doesn't
contain variables or expressions intended to insert values into the string, such as
`"$PID-$(hostname)"`.

Using single quotes makes the intent clearer that the string is constant and allows you to use
special characters such as `$` without needing to escape them.

However, there are exceptions. Double-quoted strings are preferred when the string contains single
quotes, embedded escape sequences like newline (``"`n"``), or other special characters that require
escaping. The rule doesn't warn in these cases.

## Example

### Noncompliant

```powershell
$constantValue = "I Love PowerShell"
```

### Compliant

```powershell
$constantValue = 'I Love PowerShell'
```

---
description: Avoid Invoking Empty Members
ms.date: 05/28/2026
ms.topic: reference
title: AvoidInvokingEmptyMembers
---
# AvoidInvokingEmptyMembers

**Severity Level: Warning**

## Description

Invoking dynamically constructed member names can introduce unexpected behavior and runtime errors.
Ensure that member invocations use constant, literal member names rather than expressions that are
evaluated at runtime.

Replace dynamic member name expressions with constant member names for the target type or class.

## Example

### Noncompliant

```powershell
$MyString = 'abc'
$MyString.('len'+'gth')
```

### Compliant

```powershell
$MyString = 'abc'
$MyString.('length')
```

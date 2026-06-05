---
description: Use equality operator (==) instead of an equal sign (=) as an assignment operator
ms.date: 06/05/2026
ms.topic: reference
title: PossibleIncorrectUsageOfAssignmentOperator
---
# PossibleIncorrectUsageOfAssignmentOperator

**Severity Level: Information**

## Description

This rule detects when the assignment operator `=` or equality operator `==` is used instead of the
PowerShell equality operator `-eq` in conditional statements. The rule looks for usages of `==` and
`=` operators inside `if`, `else if`, `while` and `do-while` statements but it doesn't warn if any
kind of command or expression is used at the right hand side as that's probably by design.

In many programming languages, the equality operator is denoted as `==` or `=`, but PowerShell uses
`-eq`. Therefore, it's easy for the wrong operator to be used unintentionally. This rule catches a
few special cases where the likelihood of that's quite high.

### Implicit suppression using Clang style

There are some rare cases where assigning a variable inside an `if` statement is intentional.
Instead of suppressing the rule, you can signal that the assignment's intentional by wrapping the
expression in extra parentheses. An exception applies when `$null` is used on the LHS because
there's no use case for it. For example:

```powershell
if (($shortVariableName = $SuperLongVariableName['SpecialItem']['AnotherItem']))
{
    ...
}
```

## Example

### Noncompliant

```powershell
if ($a = $b)
{
    ...
}
```

```powershell
if ($a == $b)
{

}
```

### Compliant

```powershell
if ($a -eq $b) # Compare $a with $b
{
    ...
}
```

```powershell
if ($a = Get-Something) # Only execute action if command returns something and assign result to variable
{
    Do-SomethingWith $a
}
```

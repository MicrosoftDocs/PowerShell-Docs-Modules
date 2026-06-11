---
description: Use 'Using:' scope modifier in RunSpace ScriptBlocks
ms.date: 06/28/2023
ms.topic: reference
title: UseUsingScopeModifierInNewRunspaces
---
# UseUsingScopeModifierInNewRunspaces

**Severity Level: Warning**

## Description

This rule detects when scriptblocks running in new runspaces reference parent scope variables
without the `$using:` scope modifier. When a scriptblock is intended to run in a new runspace, it
can't directly access variables from the parent scope. You must either use the `$using:` scope
modifier to explicitly reference a parent scope variable, or initialize the variable within the
scriptblock itself. This rule applies to:

- `Invoke-Command`- Only with the **ComputerName** or **Session** parameter.
- `Workflow { InlineScript {} }`
- `Foreach-Object` - Only with the **Parallel** parameter
- `Start-Job`
- `Start-ThreadJob`
- The `Script` resource in DSC configurations, specifically for the `GetScript`, `TestScript` and
  `SetScript` properties.

## Example

### Noncompliant

```powershell
$var = 'foo'
1..2 | ForEach-Object -Parallel { $var }
```

### Compliant

```powershell
$var = 'foo'
1..2 | ForEach-Object -Parallel { $using:var }
```

## More correct examples

```powershell
$bar = 'bar'
Invoke-Command -ComputerName 'foo' -ScriptBlock { $using:bar }
```

```powershell
$bar = 'bar'
$s = New-PSSession -ComputerName 'foo'
Invoke-Command -Session $s -ScriptBlock { $using:bar }
```

```powershell
# Remark: Workflow is supported on Windows PowerShell only
Workflow {
    $foo = 'foo'
    InlineScript { $using:foo }
}
```

```powershell
$foo = 'foo'
Start-ThreadJob -ScriptBlock { $using:foo }
Start-Job -ScriptBlock {$using:foo }
```

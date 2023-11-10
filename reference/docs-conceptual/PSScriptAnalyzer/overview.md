---
description: This article explains the purpose of the PSScriptAnalyzer module.
ms.date: 11/10/2023
title: PSScriptAnalyzer module
---
# PSScriptAnalyzer module

PSScriptAnalyzer is a static code checker for PowerShell modules and scripts. PSScriptAnalyzer
checks the quality of PowerShell code by running a set of rules. The rules are based on PowerShell
best practices identified by PowerShell Team and the community. It generates **DiagnosticResults**
(errors and warnings) to inform users about potential code defects and suggests possible solutions
for improvements.

PSScriptAnalyzer ships with a collection of built-in rules that check various aspects of
PowerShell code such as:

- The presence of uninitialized variables
- Use of **PSCredential** type
- Use of `Invoke-Expression`
- And many more

You can choose the rules to include or exclude for your modules and scripts. PSScriptAnalyzer can
also fix the formatting of your code. This helps you produce code that conforms to a standard style,
is easier to read, and is more maintainable.

## Installing PSScriptAnalyzer

Supported PowerShell Versions and Platforms

- Windows PowerShell 3.0 or greater
- PowerShell 7.0.11 or greater on Windows/Linux/macOS

Install using PowerShellGet 2.x:

```powershell
Install-Module -Name PSScriptAnalyzer -Force
```

Install using PSResourceGet 1.x:

```powershell
Install-PSResource -Name PSScriptAnalyzer -Reinstall
```

The **Force** or **Reinstall** parameters are only necessary when you have an older version of
PSScriptAnalyzer installed. These parameters also work even when you don't have a previous version
installed.

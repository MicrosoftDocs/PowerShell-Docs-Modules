---
Module Name: Microsoft.PowerShell.Crescendo
Module Guid: 2dd09744-1ced-4636-a8ce-09a0bf0e566a
ms.date: 03/10/2022
Download Help Link: https://aka.ms/ps-modules-help
Help Version: 1.0.0
Locale: en-US
---

# Microsoft.PowerShell.Crescendo Module

## Description

Crescendo is a development accelerator enabling you to rapidly build PowerShell cmdlets that
leverage existing command-line tools. Crescendo amplifies the command-line experience of the
original tool to include object output for the PowerShell pipeline, privilege elevation, and
integrated help information. A Crescendo module replaces cumbersome command-line tools with
PowerShell cmdlets that are easier to use in automation and packaged to share with team members.

## Microsoft.PowerShell.Crescendo Cmdlets

### [Export-CrescendoModule](Export-CrescendoModule.md)
Creates a module from PowerShell Crescendo JSON configuration files

### [Export-Schema](Export-Schema.md)
Exports the JSON schema for command configuration as a PowerShell object.

### [Import-CommandConfiguration](Import-CommandConfiguration.md)
Import a PowerShell Crescendo json file.

### [New-CrescendoCommand](New-CrescendoCommand.md)
Creates a PowerShell command object.

### [New-ExampleInfo](New-ExampleInfo.md)
Creates a PowerShell object representing an example used in a Crescendo command object.

### [New-OutputHandler](New-OutputHandler.md)
Creates a PowerShell object representing a Crescendo output handler.

### [New-ParameterInfo](New-ParameterInfo.md)
Creates a PowerShell object representing a Crescendo Parameter definition.

### [New-UsageInfo](New-UsageInfo.md)
Creates a PowerShell object representing a Crescendo Usage definition.

### [Test-IsCrescendoCommand](Test-IsCrescendoCommand.md)
Tests a cmdlet to see if it was created by Crescendo.

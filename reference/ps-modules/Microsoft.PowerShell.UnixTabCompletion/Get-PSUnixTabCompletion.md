---
external help file: Microsoft.PowerShell.UnixTabCompletion.dll-Help.xml
Module Name: Microsoft.PowerShell.UnixTabCompletion
ms.date: 10/18/2022
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.unixtabcompletion/get-psunixtabcompletion?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Get-PSUnixTabCompletion

## SYNOPSIS
Gets a list of registered command-line completers.

## SYNTAX

```
Get-PSUnixTabCompletion [<CommonParameters>]
```

## DESCRIPTION

The `Get-PSUnixTabCompletion` cmdlet lists registered command-line completer. This module supports
completions from `zsh` and `bash`. By default it looks for `zsh` and then `bash` to run completions.

## EXAMPLES

### Example - Get a list of registered completers

```powershell
Get-PSUnixTabCompletion
```

```Output
CompletionScript                           Name
----------------                           ----
/usr/share/bash-completion/bash_completion BashUtilCompleter
```

The output shows the completion script being used.

## PARAMETERS

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

[Set-PSUnixTabCompletion](Set-PSUnixTabCompletion.md)

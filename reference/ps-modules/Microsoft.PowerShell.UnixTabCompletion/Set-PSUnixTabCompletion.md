---
external help file: Microsoft.PowerShell.UnixTabCompletion.dll-Help.xml
Module Name: Microsoft.PowerShell.UnixTabCompletion
ms.date: 10/18/2022
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.unixtabcompletion/set-psunixtabcompletion?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Set-PSUnixTabCompletion

## SYNOPSIS
Used to configure a completion script to be used by the module.

## SYNTAX

### Completer

```
Set-PSUnixTabCompletion [-Completer] <IUnixUtilCompleter> [<CommonParameters>]
```

### Shell

```
Set-PSUnixTabCompletion [-Shell] <String> [[-ShellType] <ShellType>] [<CommonParameters>]
```

### ShellType

```
Set-PSUnixTabCompletion [-ShellType] <ShellType> [-CompletionScript <String>] [<CommonParameters>]
```

## DESCRIPTION

This command allows you to override the default completion script chosen by the module when it's
loaded. Use this command in your PowerShell profile script to ensure you same configuration for
every PowerShell session. The cmdlet searches known locations for a completion script based on the
shell chosen.

## EXAMPLES

### Example 1 - Load a command-line completer by shell type

This example sets the completion provider to `zsh`.

```powershell
Set-PSUnixTabCompletion -ShellType Zsh
```

### Example 2 - Load a command-line completer by shell name

This example sets the completion provider to use `/bin/zsh` for command-line completions.

```powershell
Set-PSUnixTabCompletion -Shell "/bin/zsh"
```

### Example 3 - Load a command-line completion script from an alternate path

This example sets the shell to `bash` and uses completion script specified by the user. This is
useful for operating systems that install the completion script is non-standard location or if you
create your own shell completion script.

```powershell
Set-PSUnixTabCompletion -ShellType Bash -CompletionScript /usr/local/etc/bash_completion
```

### Example 4 - Load a custom command-line completer

You can create your own .NET assembly that containing a class that implements the
**IUnixUtilCompleter** interface. This class can loaded via a PowerShell module or using the
`Add-Type` cmdlet. Once it's loaded, create a new instance of the class and pass that to
`Set-PSUnixTabCompletion`.

```powershell
$myCompleter = [MyCompleter]::new()
Set-PSUnixTabCompletion -Completer $myCompleter
```

## PARAMETERS

### -Completer

A reference to an object that implements the **IUnixUtilCompleter** interface.

```yaml
Type: Microsoft.PowerShell.UnixTabCompletion.IUnixUtilCompleter
Parameter Sets: Completer
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -CompletionScript

The path to the completion script. Use this parameter to provide alternate completion scripts.

```yaml
Type: System.String
Parameter Sets: ShellType
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Shell

The path to a shell that can provide a completion script.

```yaml
Type: System.String
Parameter Sets: Shell
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ShellType

The type of shell to be used for completion. The cmdlet searches for known completion scripts for
the specified type.

```yaml
Type: Microsoft.PowerShell.UnixTabCompletion.ShellType
Parameter Sets: Shell, ShellType
Aliases:
Accepted values: None, Zsh, Bash

Required: False (Shell), True (ShellType)
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

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

[Get-PSUnixTabCompletion](Get-PSUnixTabCompletion.md)

[about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles)

---
description: Describes how to use the UnixTabCompletion module.
Locale: en-US
ms.date: 10/18/2022
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.unixtabcompletion/about/about_aliases?view=ps-modules&wt.mc_id=ps-gethelp
schema: 2.0.0
title: about UnixTabCompletion
---
# about_UnixTabCompletion

## Short description
PowerShell parameter completers for native commands on Linux and macOS.

## Long description

This module uses completers supplied in traditional Unix shells to complete
native utility parameters in PowerShell on Linux and macOS. This module
supports completions from `zsh` and `bash`. By default it looks for `zsh` and
then `bash` to run completions.

This module is only supported on Linux and macOS platforms.

## Basic usage

To enable Unix command-line completions, install this module and add the
following to your profile:

```powershell
Import-Module Microsoft.PowerShell.UnixTabCompletion
```

There is also an alternate command, `Import-PSUnixTabCompletion`, that has the
same functionality but is discoverable by command completion.

This will register argument completers for all native commands found in the
usual Unix util directories.

Given the nature of native completion results, you may find this works best
with PSReadLine's MenuComplete mode:

```powershell
Import-Module PSUnixTabCompletion
Set-PSReadLineKeyHandler -Key Tab -Function MenuComplete
```

## Further configuration

You can set a preferred shell do using an environment variable. You must set
the value before loading the module. Setting the variable after loading the
module has no effect.

You can set value of the environment variable to the name of the shell or the
path the the shell executable to be used for command-line completion.

```powershell
$env:COMPLETION_SHELL_PREFERENCE = 'bash'
$env:COMPLETION_SHELL_PREFERENCE = '/bin/bash'
```

You can change the completer after loading using the `Set-PSUnixTabCompletion`
cmdlet.

```powershell
Set-PSUnixTabCompletion -ShellType Zsh
```

You can retrieve the current configuration with the `Get-PSUnixTabCompletion`
cmdlet:

```powershell
PS> Get-PSUnixTabCompletion
```

```Output
CompletionScript                           Name
----------------                           ----
/usr/share/bash-completion/bash_completion BashUtilCompleter
```

## Supporting different versions of bash

`bash` may have different tab completion depending on the version and system.
The default location of the `bash` completion script is set to
`/usr/share/bash-completion/bash_completion`.

If your completion script is in an alternative location, you may provide the
location of the completion script using the **CompletionScript** parameter.

## Unregistering Unix command completions

The **Microsoft.PowerShell.UnixTabCompletion** module unregisters the
configured command-line completions when the module is unloaded.

```powershell
Remove-Module Microsoft.PowerShell.PSUnixTabCompletion
```

As with loading, there is also a convenience command provided for this:

```powershell
Remove-PSUnixTabCompletion
```

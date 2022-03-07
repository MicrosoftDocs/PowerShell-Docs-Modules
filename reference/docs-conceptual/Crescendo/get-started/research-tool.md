---
description: How to collect information about the command-line tool to decide which features to implement in your cmdlets.
ms.date: 03/07/2022
title: Research the command-line tool's syntax and output
---
# Research the command-line tool's syntax and output

The [previous article](choose-command-line-tool.md) provided criteria for selecting the command-line
tool you want to amplify with Crescendo. In this article describe ways to information about the tool
to help you design cmdlets using Crescendo.

For the examples in this article we use the Azure Connected Machine agent tool (azcmagent). We chose
this tool because:

- It is easy to install and remove
- It doesn't require an active Azure subscription for basic usage
- It has useful in-console help and online documentation
- It produces easily consumable output

For more information, see the [Installing the azcmagent tool](#installing-the-azcmagent-tool)
section of this article.

## Start with command-line help and documentation

Many command-line tools include a switch or parameter to display help content. Most modern
command-line tools provide multiple levels of help for the various use-case scenarios the tool
provides. For example, running `azcmagent` without any parameters displays the top-level help, which
contains a list of subcommands.

```output
...
Usage:
  azcmagent [command]

Available Commands:
  check       Runs connectivity checks
  config      Change configuration settings for this machine
  connect     Connects this machine to Azure
  disconnect  Disconnects this machine from Azure
  help        Help about any command
  license     Display the End-user license agreement file
  logs        Creates a .zip file containing relevant logs. This is primarily useful for troubleshooting.
  show        Gets machine metadata and Agent status. This is primarily useful for troubleshooting.
  version     Display the Hybrid Management Agent version
...
```

Each of the subcommands can their own subcommands and parameters. For example, the `config`
subcommand has five subcommands.

```powershell
PS> azcmagent config --help
Change configuration settings for this machine

Usage:
  azcmagent config [command]

Available Commands:
  clear       Clear a configuration property's value
  get         Get a configuration property's value
  info        Describes the config properties users can set
  list        List all configuration properties and values
  set         Set a value for a configuration property

Flags:
  -h, --help      help for config
      --version   version for config

Global Flags:
      --config string   config file (default is $HOME/.azcmagent.yaml)
  -j, --json            Output in JSON format
      --log-stderr      Redirect error and verbose messages to stderr
  -v, --verbose         Increase logging verbosity to show all logs

Use "azcmagent config [command] --help" for more information about a command.
```

Use the command-line help to discover the possible use cases. You can redirect the output of each
help command to a file that you can use for later reference as you create your Crescendo cmdlets.

> [!TIP]
> If the help content is structured consistently, it may be possible to create code that builds
> cmdlets by parsing this help output. Crescendo comes with some experimental help parsers to
> illustrate how this may be accomplished. See `Experimental` folder in the root folder of the
> **Microsoft.PowerShell.Crescendo** module.

Take note of the output formats that the command-line tool offers. Many command-line tools can
output information other formats such as CSV or JSON. These structured formats are easier to convert
to PowerShell object.

## Capture example output for parsing

Once you have decided which of the tool's commands to amplify with Crescendo, collect sample output
from those commands. Redirect the output to a file for each command. Use this example data to help
you design the output handlers (parsers) for your Crescendo cmdlets.

As you inspect the sample output, think about the types of data returned. As you construct your
objects you should converts the strings output by the command-line tool to .NET types. For example,
timestamp information can be converted to .NET `[DateTime]` types. Also, look at the formatting of
the output for markers that separate data fields. Those markers can be used to parse the information
as you construct your objects for output.

The `azcmagent` tool has the option to output information in JSON format. This makes the conversion
to a PowerShell object very simple. For example:

```powershell
PS> $agentStatus = azcmagent show --json | ConvertFrom-Json
PS> $agentStatus.services

displayName       serviceName      status
-----------       -----------      ------
GC Service        gcarcservice     running
Extension Service extensionservice running
Agent Service     himds            running
```

For more complex examples of parsing output, see this
[blog post](https://devblogs.microsoft.com/powershell-community/a-closer-look-at-the-parsing-code-of-a-crescendo-output-handler/)
from the PowerShell Community blog.

## Installing the azcmagent tool

You can download the Azure Connected Machine agent package for Windows and Linux from the locations
listed below.

- [Windows agent Windows Installer package](https://aka.ms/AzureConnectedMachineAgent) from the
  Microsoft Download Center.
- Linux agent is distributed from Microsoft's
  [package repository](https://packages.microsoft.com/). Choose the preferred package format for the
  distribution (RPM or DEB).

For more information about the Azure Connected Machine agent, see
[Managing and maintaining the Connected Machine agent](/azure/azure-arc/servers/manage-agent).

## Next step

> [!div class="nextstepaction"]
> [Create a cmdlet configuration](create-new-cmdlet.md)

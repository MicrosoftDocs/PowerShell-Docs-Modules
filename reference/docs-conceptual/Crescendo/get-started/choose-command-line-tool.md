---
description: How to select a native command to wrap using Crescendo.
ms.date: 03/07/2022
title: Choosing a command-line tool to amplify
---
# Choosing the command-line tool for Crescendo

Developing a cmdlet with Crescendo is a rapid, reliable way to _amplify_ a command-line tool and
produce a cmdlet-like experience. Most of the time, the tool you need to work with is directly tied
to the technology you are attempting to automate, making the decision about which tool simple. To
optimize your investment into developing a cmdlet, consider the following criteria:

## Command-line tools that make good candidates

- **The original tool is difficult to use.**

  If the command is simple to use and provides the information you need, there is no need to create
  a cmdlet. However, this isn't always the case with all command-line tools. Many command-line tools
  have their own unique syntax, parameters, and output that make it difficult for inexperienced
  admins to use the command. Converting the command into a cmdlet provides all the benefits of
  cmdlet discovery, consistency, and structured output as objects.

- **The command-line tool output is difficult to use in automation.**

  Command-line tools output their information to the screen as string data. This is not the
  structured data (objects) that PowerShell expects in the pipeline, which limits you from using
  other PowerShell cmdlets to focus only on the data you want. Crescendo assists you with amplifying
  the command-line tool to a cmdlet so that the tool can participate in the PowerShell pipeline.

- **The command-line tool doesn't provide adequate help.**

  Cmdlets should have complete and descriptive help information. This helpful information is
  available at your finger tips for details on parameters, descriptions, and examples. Command-line
  can be difficult to use when they lack help information. Crescendo gives you the ability to create
  the missing help for your amplified commands.

## Command-line tools that make bad candidates

- **Does a cmdlet already exist?**

  PowerShell has a well-established ecosystem of modules that extend the built-in capabilities of
  PowerShell. Before deciding to amplify a command-line tool with Crescendo, first check to see if a
  cmdlet already exists that performs your intended goal. For example, wrapping the Windows command
  `ipconfig.exe` to get the current IP address is a poor choice because the module **NetAdapter**
  contains `Get-NetIPConfiguration`, which provides the same information with structured output.

- **Are there better ways?**

  Often the information you need for automation can be obtained quicker than making a cmdlet.
  PowerShell lets you access other frameworks and libraries, such as WMI and .NET. Instead of
  investing time creating a cmdlet, you might be able to get the information quicker using one of
  these libraries.

- **Is the output trivial?**

  In some situations, the command-line tool may produce output that is easy to use in your
  automation. If this is the case, investing time in creating a cmdlet with structured output may
  not be of interest.

## Best Practices

- **Reduce your time of investment by focusing on what you need.**

  When examining a command-line tool for automation, remember you are not required to replicate all
  features of the tool in the new cmdlet. In other words, reduce the time investment by choosing
  only the features or parameters you need to accomplish your goal. If a tool has 12 use cases and
  you only need the functionality of two of them, create a Crescendo configuration only for the two
  scenarios you need.

## Next step

> [!div class="nextstepaction"]
> [Researching the command-line tool's syntax and output](research-tool.md)
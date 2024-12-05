---
title: AI Shell command reference
description: Learn about the command-line options and commands available in AI Shell.
ms.date: 10/29/2024
ms.topic: reference
---
# AI Shell command reference

## Command-line options

```
Description:
  AI for the command line.

Usage:
  aish [<query>] [options]

Arguments:
  <query>  The query term used to get response from AI.

Options:
  --channel <channel>              A named pipe used to setup communication
                                   between aish and the command-line shell.
  --shell-wrapper <shell-wrapper>  Path to the configuration file to wrap
                                   AI Shell as a different application.
  --version                        Show version information
  -?, -h, --help                   Show help and usage information
```

## Chat commands

By default, `aish` provides a base set of chat commands used to interact with the AI model. To get a
list of commands, use the `/help` command in the chat session.

```
  Name       Description                                      Source
──────────────────────────────────────────────────────────────────────
  /agent     Command for agent management.                    Core
  /cls       Clear the screen.                                Core
  /code      Command to interact with the code generated.     Core
  /dislike   Dislike the last response and send feedback.     Core
  /exit      Exit the interactive session.                    Core
  /help      Show all available commands.                     Core
  /like      Like the last response and send feedback.        Core
  /refresh   Refresh the chat session.                        Core
  /render    Render a markdown file, for diagnosis purpose.   Core
  /retry     Regenerate a new response for the last query.    Core
```

## `/agent` sub commands

### `/agent config`

Open up the setting file for an agent. When no agent is specified, target the active agent.

```
/agent config [<agent>] [options]
```

Arguments: `<azure|openai-gpt>` Name of an agent.

Options:

- `--editor <editor>` The editor to open the setting file in.
- `-h`, `--help` Show help and usage information

Example:

```
/agent config openai-gpt
```

### `/agent list`

List all available agents.

Options:

- `-h`, `--help`  Show help and usage information

Example:

```
> /agent list

  Name             Description
───────────────────────────────────────────---------------------──
  openai-gpt       This agent is designed to provide a flexible
                   platform for interacting with OpenAI services
                   (Azure OpenAI or the public OpenAI) through
                   one or more customly defined GPT instances.

                   The agent is currently not ready to serve
                   queries, because there is no GPT defined.
                   Please follow the steps below to configure the
                   setting file properly before using this agent:

                   1. Run '/agent config' to open the setting file.
                   2. Define the GPT(s). See details at
                      https://aka.ms/aish/openai
                   3. Run '/refresh' to apply the new settings.
  azure (active)   This AI assistant can generate Azure CLI and
                   Azure PowerShell commands for managing
                   Azure resources, answer questions, and provides
                   information tailored to your specific Azure
                   environment.
```

## `/code` sub commands

### `/code copy`

Copy the n-th (1-based) code snippet to clipboard. Copy all the code when `<n>` isn't specified.

Usage:

```
code copy [<n>] [options]
```

Arguments:

- `<n>` Use the n-th (1-based) code snippet. Use all the code when no value is specified.
[default: -1]

Options:

- `-h`, `--help`  Show help and usage information

Examples

![An animation showing how to copy the specific code snippets to the clipboard.][01]

### `/code save`

Save all the code to a file.

Usage:

```
/code save <file> [options]
```

Arguments:

- `<file>`  The file path to save the code to.

Options:

- `--append` Append to the end of the file.
- `-h`, `--help` Show help and usage information

Examples:

The following example copies the all the code to a file.

![A screenshot showing how to save the code to a file.][03]

### `/code post`

Post the n-th (1-based) code snippet to the connected command-line shell. Post all the code
when `<n>` isn't specified.

Usage:

```
/code post [<n>] [options]
```

Arguments:

- `<n>` Use the n-th (1-based) code snippet. Use all the code when no value is specified.

Options:

- `-h, --help` Show help and usage information

Examples:

![An animation showing how to post the specific code snippets to the connected command-line shell.][02]

<!-- TO DO
- Add subcommands and switches for each command.
- Add examples for each subcommand.
-->

<!-- link references -->
[01]: media/aishell-reference/code-copy-command.gif
[02]: media/aishell-reference/code-post-command.gif
[03]: media/aishell-reference/code-save-command.png

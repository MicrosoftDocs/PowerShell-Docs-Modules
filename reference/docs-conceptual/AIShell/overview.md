---
title: What is AI Shell?
description: Learn about AI Shell, an interactive shell that provides a chat interface with language models.
ms.date: 01/12/2026
ms.topic: overview
ms.collection: ce-skilling-ai-copilot
---
# What is AI Shell?

[!INCLUDE[aishell-deprecated](../../includes/aishell-deprecated.md)]

AI Shell is an interactive shell that provides a chat interface with language models. The shell
provides agents that connect to different AI models and other assistance providers. Users can
interact with the agents in a conversational manner.

The AI Shell project includes:

- A command-line shell interface (`aish`)
- A framework for creating AI agents and other assistance providers
- Integration with Windows Terminal and iTerm2 on macOS
- A PowerShell module for integration with PowerShell. For more information, see the
  [AI Shell module][02].
- Support for MCP servers and tools
- Support for [Foundry Local][01] deployments

Each AI assistant is known as an agent. The initial release of AI Shell includes two agents:

- **Azure OpenAI** agent that connects to an instance of **gpt-4o**. Use this agent for general
  AI tasks.
- **Azure Copilot** agent that can assist with Microsoft Azure knowledge. Use the Azure agent for
  assistance with Azure CLI and Azure PowerShell commands.

You can run the AI Shell executable (`aish.exe`) in a standalone experience or you can use the
**AIShell** PowerShell module with PowerShell 7 to create a split-pane (sidecar) experience with
Windows Terminal. The sidecar experience is the recommended way to use AI Shell because you get
deeper integration with the shell. These features include:

- The ability to insert code from the AI Shell response directly into the connect command shell
- Multi-step commands are added to the Predictive IntelliSense buffer for quick acceptance
- Simple, single-command error recovery
- MCP integration

## Project status

AI Shell is currently a preview release. Some features of the tool are still being developed and are
subject to change. For more information about the current version and a complete list of changes,
see the [Release notes][05].

## Known issues

This current release of AI Shell has some known issues that we're actively working on addressing:

- The sidecar experience only works with Windows Terminal and iTerm2 for macOS.
- AI Shell isn't supported on Linux. You might get it to work but it doesn't support the split
  terminal integration that you get with Windows Terminal and iTerm2. AI Shell isn't tested on any
  Linux distribution.
- If you have preview (developer) and stable versions of Windows Terminal installed, the
  `Start-AIShell` command opens a new terminal running the stable version of Windows Terminal.
- If you started Window Terminal as an administrator, the `Start-AIShell` command opens a new
  terminal window running Windows Terminal without elevation.
- If you're using the default terminal app in macOS, you don't get the sidecar experience and the
  colors might not render correctly. It might be difficult to read the generated code.

## Providing feedback

Your feedback is important to us during this development phase. We encourage you to share your
experiences to help us improve AI Shell.

Here are ways you can get involved:

- **File Issues:** If you encounter bugs, have suggestions for new features, or would like to report
  inconsistencies, open an issue on the [AI Shell GitHub repository][04].
- **Join the discussions:** Join our community discussions in the [GitHub discussions][03] tab.
  Share ideas, discuss potential improvements, connect with other users, and share any agents you
  create.
- **Documentation:** If you notice any documentation gaps, you can suggest changes or submit PRs to
  improve our documentation.

<!-- link references -->
[01]: /azure/ai-foundry/foundry-local/what-is-foundry-local
[02]: /powershell/module/aishell/
[03]: https://github.com/PowerShell/AIShell/discussions
[04]: https://github.com/PowerShell/AIShell/issues
[05]: release-notes.md


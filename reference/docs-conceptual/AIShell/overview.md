---
title: What is AI Shell?
description: Learn about AI Shell, an interactive shell that provides a chat interface with language models.
ms.date: 05/21/2025
ms.topic: overview
---

# What is AI Shell?

AI Shell is an interactive shell that provides a chat interface with language models. The shell
provides agents that connect to different AI models and other assistance providers. Users can
interact with the agents in a conversational manner.

The AI Shell project includes:

- A command-line shell interface (`aish`)
- A framework for creating AI agents and other assistance providers
- Integration with Windows Terminal and iTerm2 on macOS
- A PowerShell module for integration with PowerShell. For more information, see the
  [AI Shell module][01].

Each AI assistant is known as an agent. The initial release of AI Shell includes two agents:

- **Azure OpenAI** agent that connects to an instance of **gpt-4o**. Use this agent for general
  AI tasks.
- **Copilot in Azure** agent that can assist with Microsoft Azure knowledge. Use the Azure agent for
  assistance with Azure CLI and Azure PowerShell commands.

You can run the AI Shell executable (`aish.exe`) in a standalone experience or you can use the
**AIShell** PowerShell module with PowerShell 7 to create a split-screen experience with Windows
Terminal. This is the recommended way to use AI Shell because you get deeper integration with the
shell. These features include:

- The ability to insert code from the AI Shell response directly into the connect command shell
- Multi-step commands are added to the Predictive IntelliSense buffer for quick acceptance
- Simple, single-command error recovery

## Project Status

The current version of AI Shell is v1.0.0-preview.4. AI Some elements of the tool are still under
development and are subject to change.

AI Shell v1.0.0-preview.4 includes the following enhancements:

- Improved macOS support including the side-car experience with iTerm2
- Support for Microsoft Entra ID authentication in Azure OpenAI
- New parameters for `Invoke-AIShell`
- Experimental Phi Silica agent that uses the built-in AI model included with the latest Copilot+
  PCs

## Known Issues

This current release of AI Shell has some known issues that we're actively working on addressing:

- The split-screen experience only works with Windows Terminal and iTerm2 for macOS.
- The **AI Shell** module isn't supported on Linux. You can run the `aish` executable on Linux,
  but it isn't tested on any Linux distribution.
- If you have multiple versions of Windows Terminal installed, the `Start-AIShell` command opens a
  new terminal window running a different version of Windows Terminal.
- If you started Window Terminal as an administrator, the `Start-AIShell` command opens a new
  terminal window running Windows Terminal without elevation.
- If you're using the default Mac Terminal, the colors might not render correctly. It might be
  difficult to read the code generated.

You can report other issues in the [GitHub repository][03].

## Providing feedback

Your feedback is important to us during this development phase. We encourage you to share your
experiences to help us improve AI Shell.

Here are ways you can get involved:

- **File Issues:** If you encounter bugs, have suggestions for new features, or would like to report
  inconsistencies, open an issue on the [AI Shell GitHub repository][03].
- **Join the discussions:** Join our community discussions in the [GitHub discussions][02] tab.
  Share ideas, discuss potential improvements, connect with other users, and share any agents you
  create.
- **Documentation:** If you notice any documentation gaps, you can suggest changes or submit PRs to
  improve our documentation.

<!-- link references -->
[01]: /powershell/module/aishell/
[02]: https://github.com/PowerShell/ProjectMercury/discussions
[03]: https://github.com/PowerShell/ProjectMercury/issues

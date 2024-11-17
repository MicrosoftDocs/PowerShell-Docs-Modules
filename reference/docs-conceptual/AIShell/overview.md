---
title: What is AI Shell?
description: Learn about AI Shell, an interactive shell that provides a chat interface with language models.
ms.date: 11/11/2024
ms.topic: overview
---

# What is AI Shell?

AI Shell is an interactive shell that provides a chat interface with language models. The shell
provides agents that connect to different AI models and other assistance providers. Users can
interact with the agents in a conversational manner.

The AI Shell project includes:

- The command-line shell (`aish`) interface
- A framework for creating AI agents and other assistance providers
- Integration with Windows Terminal and iTerm2 on macOS
- A PowerShell module for tight integration with PowerShell. For more information, see the
  [AI Shell module][01].

Each AI assistant is known as an agent. The initial release of AI Shell includes two agents:

- **Azure OpenAI** agent that connects to an instance of **gpt-4o**. Use this agent for general
  AI tasks.
- **Copilot in Azure** agent that can assist with Microsoft Azure knowledge. Use the Azure agent for
  assistance with Azure CLI and Azure PowerShell commands.

The AI Shell executable (`aish.exe`) can be run in a standalone experience or you can use the **AI
Shell** PowerShell module with PowerShell 7 to create a split-screen experience with Windows
Terminal. This is the recommended way to use AI Shell because you get deeper integration with the
shell. These features include:

- The ability to insert code from the AI Shell response directly into the connect command shell
- Multi-step commands are added to the Predictive IntelliSense buffer for quick acceptance
- Simple, single-command error recovery

## Project Status

AI Shell is currently in **Public Preview**. This means that the tool is available for testing, but
it's not feature-complete. Please note that some elements of the tool are still under development
and are subject to change. Your feedback is important to us during this development phase. We
encourage you to share your experiences to help us improve AI Shell.

## Known Issues

This current release of AI Shell has some known issues that we're actively working on addressing:

- The **AI Shell** module isn't supported on Linux.
- The split-screen experience work best with Windows Terminal. There is limited support for the
  split-screen experience on macOS with iTerm2. The `aish` executable can be run on Linux, but the
  split-screen experience is not available.
- If you have multiple versions of Windows Terminal installed, the `Start-AIShell` command opens a
  new terminal window running a different version of Windows Terminal.
- If you started Window Terminal as an administrator, the `Start-AIShell` command opens a new
  terminal window running Windows Terminal without elevation.

If you encounter any other issues, please report them to our [GitHub repository][03].

## Providing Feedback

We welcome your feedback to help improve AI Shell! Here are ways you can get involved:

- **File Issues:** If you encounter bugs, have suggestions for new features, or would like to report
  inconsistencies, please open an issue on the [AI Shell GitHub repository][03].
- **Join the discussions:** Join our community discussions on the on the
  [GitHub discussions][02] tab. Share ideas, discuss potential improvements, and connect with other
  users. This is also where we encourage you to share any agents you may create.
- **Documentation:** If you notice any documentation gaps, please suggest changes or submit PRs to
  improve our documentation.

We aren't accepting pull requests for code changes at this time, but we value your feedback and
documentation contributions.

<!-- link references -->
[01]: /powershell/module/aishell/
[02]: https://github.com/PowerShell/ProjectMercury/discussions
[03]: https://github.com/PowerShell/ProjectMercury/issues

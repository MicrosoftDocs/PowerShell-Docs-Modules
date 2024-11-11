---
title: Ollama agent README
description: Learn how to use the Ollama agent in AI Shell.
ms.date: 11/11/2024
---
# Ollama Plugin

This agent is used to interact with a language model running locally by utilizing the Ollama API.
Before using this agent you need to have Ollama installed and running.

## Pre-requisites to using the agent

- Install [Ollama][01]
- Install a [Ollama model][02], we
  suggest using the `phi3` model as it is set as the default model in the code
- [Start the Ollama API server][03]

## Configuration

Currently to change the model you will need to modify the query in the code in the
`OllamaChatService` class. The default model is `phi3`.

The default endpoint is `http://localhost:11434/api/generate` with `11434` being the default port.
This can be changed in the code and eventually will be added to a configuration file.

## Known Limitations

- There is no history shared across queries so the model will not be able to remember previous
  queries
- Streaming is currently not supported if you change the stream value to `true` in the data to send
  to the API it will not work
- Configuration is currently hard coded in the code and will be moved to a configuration file in the
  future

<!-- link references -->
[01]: https://github.com/ollama/ollama
[02]: https://github.com/ollama/ollama?tab=readme-ov-file#model-library
[03]: https://github.com/ollama/ollama?tab=readme-ov-file#start-ollama

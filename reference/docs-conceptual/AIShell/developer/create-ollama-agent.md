---
title: How to create an agent for Ollama
description: Learn how to create an agent for the Ollama language model in AI Shell.
ms.date: 11/11/2024
ms.topic: how-to
---

# Creating an Agent

An agent is a code library that interfaces with the AI Shell to talk to a specific large
language model or other assistance provider. Users chat with the agents using natural language to
get the desired output or assistance. Agents are implemented as C# classes that implement the
`ILLMAgent` interface from the `AIShell.Abstraction` package.

For details about the `AIShell.Abstraction` layer and `AIShell.Kernel`, see the
[AI Shell architecture][05] documentation.

## Prerequisites

- .NET 8 SDK or newer
- PowerShell 7.4 or newer

## Steps to create an agent

For this example we create an agent to communicate with the language model `phi3` by utilizing
[Ollama][01], a CLI tool for managing and using locally built LLM/SLMs. The complete source code of
the agent can be found in the [`shell/agents/AIShell.Ollama.Agent`][04] folder of the repository.
the repository.

### Step 1: Create a new project

Currently, the only way to import an agent is for it to be included in the folder structure of this
repository. We suggest creating an agent under the `shell/agents` folder. Create a new folder with
the prefix `AIShell.<AgentName>`. Within that folder, create a new C# project with the same name.
Run the following command from the folder where you want to create the agent:

```shell
dotnet new classlib
```

### Step 2: Add the necessary packages

Within the newly created project, add a reference to the `AIShell.Abstraction` package. To reduce
the number of files created by the build, you can disable the generation of PDB and deps.json for
release builds.

Your `.csproj` file should contain the following elements:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <SuppressNETCoreSdkPreviewMessage>true</SuppressNETCoreSdkPreviewMessage>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="AIShell.Abstraction" Version="0.1.0-alpha.11">
      <ExcludeAssets>contentFiles</ExcludeAssets>
      <PrivateAssets>all</PrivateAssets>
    </PackageReference>
  </ItemGroup>

</Project>
```

> [!IMPORTANT]
> Be sure to replace the version number with the latest version of the package. That can be found in
> the [`shell/shell.common.props`][06] file.

### Step 3: Modify the build script

Modify the build script so that you can build and test your agent during development. The
`build.ps1` script is located in the root of the repository. This script builds the kernel and all
agents. The following lines were added to the script to build the new agent.

```powershell
$ollama_agent_dir = Join-Path $agent_dir "AIShell.Ollama.Agent"

$ollama_out_dir =  Join-Path $app_out_dir "agents" "AIShell.Ollama.Agent"

if ($LASTEXITCODE -eq 0 -and $AgentToInclude -contains 'ollama') {
    Write-Host "`n[Build the Ollama agent ...]`n" -ForegroundColor Green
    $ollama_csproj = GetProjectFile $ollama_agent_dir
    dotnet publish $ollama_csproj -c $Configuration -o $ollama_out_dir
}
```

Be sure to put this code after definition of the `$agent_dir`, `$app_out_dir`, and
`$AgentToInclude`. Also add the name of the agent to the `$AgentToInclude` array and parameter
validation.

```powershell
$AgentToInclude ??= @('openai-gpt', 'interpreter', 'ollama')
```

### Step 3: Implement the agent class

To being the creation of the agent, modify the `Class1.cs` file to implement the `ILLMAgent`
interface. We suggest renaming the file to `OllamaAgent.cs` and then rename class to `OllamaAgent`.
We've also added some packages that are used by the code in the implementation.

```csharp
using System.Diagnostics;
using System.Text;
using System.Text.Json;
using AIShell.Abstraction;

namespace AIShell.Ollama.Agent;

public sealed class OllamaAgent : ILLMAgent
{

}
```

### Step 4: Add necessary class members and methods

Next, implement the necessary variables and methods of the agent class. The comments provide
descriptions of the members of the **OllamaAgent** class. The `_chatService` member is an instance
of the **OllamaChatService** class. The implementation of the **OllamaChatService** class is show in
later steps.

```csharp
public sealed class OllamaAgent : ILLMAgent
{
    /// <summary>
    /// The name of the agent
    /// </summary>
    public string Name => "ollama";

    /// <summary>
    /// The description of the agent to be shown at start up
    /// </summary>
    public string Description => "This is an AI assistant that utilizes the Ollama CLI tool. Be sure to follow all prerequisites in aka.ms/ollama/readme";

    /// <summary>
    /// This is the company added to /like and /dislike verbiage for who the telemetry helps.
    /// </summary>
    public string Company => "Microsoft";

    /// <summary>
    /// These are samples that are shown at start up for good questions to ask the agent
    /// </summary>
    public List<string> SampleQueries => [
        "How do I list files in a given directory?"
    ];

    /// <summary>
    /// These are any optional legal/additional information links you want to provide at start up
    /// </summary>
    public Dictionary<string, string> LegalLinks { private set; get; }

    /// <summary>
    /// This is the chat service to call the API from
    /// </summary>
    private OllamaChatService _chatService;

    /// <summary>
    /// A string builder to render the text at the end
    /// </summary>
    private StringBuilder _text;

    /// <summary>
    /// Dispose method to clean up the unmanaged resource of the chatService
    /// </summary>
    public void Dispose()
    {
        _chatService?.Dispose();
    }

    /// <summary>
    /// Initializing function for the class when the shell registers an agent
    /// </summary>
    /// <param name="config">Agent configuration for any configuration file and other settings</param>
    public void Initialize(AgentConfig config)
    {
        _text = new StringBuilder();
        _chatService = new OllamaChatService();

        LegalLinks = new(StringComparer.OrdinalIgnoreCase)
        {
            ["Ollama Docs"] = "https://github.com/ollama/ollama",
            ["Prerequisites"] = "https://aka.ms/ollama/readme"
        };

    }

    /// <summary>
    /// Get commands that an agent can register to the shell when being loaded
    /// </summary>
    public IEnumerable<CommandBase> GetCommands() => null;

    /// <summary>
    /// Gets the path to the setting file of the agent.
    /// </summary>
    public string SettingFile { private set; get; } = null;

    /// <summary>
    /// Refresh the current chat by starting a new chat session.
    /// An agent can reset chat states in this method.
    /// </summary>
    public void RefreshChat() {}

    /// <summary>
    /// Gets a value indicating whether the agent accepts a specific user action feedback.
    /// </summary>
    /// <param name="action">The user action.</param>
    public bool CanAcceptFeedback(UserAction action) => false;

    /// <summary>
    /// A user action was taken against the last response from this agent.
    /// </summary>
    /// <param name="action">Type of the action.</param>
    /// <param name="actionPayload"></param>
    public void OnUserAction(UserActionPayload actionPayload) {}

    /// <summary>
    /// Main chat function that takes
    /// </summary>
    /// <param name="input">The user input from the chat experience</param>
    /// <param name="shell">The shell that provides host functionality</param>
    /// <returns>Task Boolean that indicates whether the query was served by the agent.</returns>
    public async Task<bool> Chat(string input, IShell shell)
    {

    }
}
```

For the initial implementation, we want the agent to return "Hello World!" to prove that we have
create the correct interfaces. We will also add a `try-catch` block to catch any expections to
handle when the user tries to cancel the operation.

Add the following code to your `Chat` method.

```csharp
public async Task<bool> Chat(string input, IShell shell)
{
    // Get the shell host
    IHost host = shell.Host;

    // get the cancelation token
    CancellationToken token = shell.CancellationToken;

    try
    {
       host.RenderFullResponse("Hello World!");
    }
    catch (OperationCanceledException e)
    {
        _text.AppendLine(e.ToString());

        host.RenderFullResponse(_text.ToString());

        return false;
    }

    return true;
}
```

### Step 5: Build your agent

At this point its good to try building and testing the agent. See if you get `Hello World!` when you
ask a question.

Use the following command to build the agent:

```powershell
../../build.ps1
```

To test the agent, run the `aish` you just built. The build script puts the path to `aish` on the
clipboard. Paste the path from the clipboard into your terminal application. Select your agent from
the list of agents presented by `aish`.

```
AI Shell
v0.1.0-alpha.11

Please select an agent to use:

    interpreter
   >ollama
    openai-gpt
```

After selecting the agent, enter a question in the chat window. You should see the response "Hello
World!".

### Step 6: Add ollama check

Next, we want to add a check to make sure ollama is running.

```csharp
public async Task<bool> Chat(string input, IShell shell)
{
    // Get the shell host
    IHost host = shell.Host;

    // get the cancellation token
    CancellationToken token = shell.CancellationToken;

    if (Process.GetProcessesByName("ollama").Length is 0)
    {
        host.RenderFullResponse("Please be sure the ollama is installed and server is running. Check all the prerequisites in the README of this agent are met.");
        return false;
    }

    // Calls to the API will go here

    return true;
}
```

### Step 7: Create data structures to exchange data with the Chat Service

Before we can use the ollama API, we need to create classes that handle input to and responses from
the ollama API. To find more information about the API call we're going to make see, this The
following [ollama example][02] shows the format of the input and the response from the agent.

For this example we call the ollama API with streaming disabled. This generates a single, fixed
response. In the future we could add streaming capabilities so that responses could be rendered in
real time, as the agent receives them.

To defined the data structures, create a new file called `OllamaSchema.cs` in the same folder.

```csharp
namespace AIShell.Ollama.Agent;

// Query class for the data to send to the endpoint
internal class Query
{
    public string prompt { get; set; }
    public string model { get; set; }

    public bool stream { get; set; }
}

// Response data schema
internal class ResponseData
{
    public string model { get; set; }
    public string created_at { get; set; }
    public string response { get; set; }
    public bool done { get; set; }
    public string done_reason { get; set; }
    public int[] context { get; set; }
    public double total_duration { get; set; }
    public long load_duration { get; set; }
    public int prompt_eval_count { get; set; }
    public int prompt_eval_duration { get; set; }
    public int eval_count { get; set; }
    public long eval_duration { get; set; }
}

internal class OllamaResponse
{
    public int Status { get; set; }
    public string Error { get; set; }
    public string Api_version { get; set; }
    public ResponseData Data { get; set; }
}
```

Now we have the pieces we need to construc a chat service that communicates using the ollama API. A
separate chat service class isn't required but can be helpful to abstract the calls to the API.

Create a new file called `OllamaChatService.cs` in the same folder as the agent. For this example,
we are using a hard coded endpoint and model for the ollama API. In the future, we could add these
as parameters in an agent configuration file.

```csharp
using System.Net.Http.Headers;
using System.Text;
using System.Text.Json;

using AIShell.Abstraction;

namespace AIShell.Ollama.Agent;

internal class OllamaChatService : IDisposable
{
    /// <summary>
    /// Ollama endpoint to call to generate a response
    /// </summary>
    internal const string Endpoint = "http://localhost:11434/api/generate";

    /// <summary>
    /// Http client
    /// </summary>
    private readonly HttpClient _client;

    /// <summary>
    /// Initialization method to initialize the http client
    /// </summary>

    internal OllamaChatService()
    {
        _client = new HttpClient();
    }

    /// <summary>
    /// Dispose of the http client
    /// </summary>
    public void Dispose()
    {
        _client.Dispose();
    }

    /// <summary>
    /// Preparing chat with data to be sent
    /// </summary>
    /// <param name="input">The user input from the chat experience</param>
    /// <returns>The HTTP request message</returns>
    private HttpRequestMessage PrepareForChat(string input)
    {
        // Main data to send to the endpoint
        var requestData = new Query
        {
            model = "phi3",
            prompt = input,
            stream = false
        };

        var json = JsonSerializer.Serialize(requestData);

        var data = new StringContent(json, Encoding.UTF8, "application/json");
        var request = new HttpRequestMessage(HttpMethod.Post, Endpoint) { Content = data };

        return request;
    }

    /// <summary>
    /// Getting the chat response async
    /// </summary>
    /// <param name="context">Interface for the status context used when displaying a spinner.</param>
    /// <param name="input">The user input from the chat experience</param>
    /// <param name="cancellationToken">The cancellation token to exit out of request</param>
    /// <returns>Response data from the API call</returns>
    internal async Task<ResponseData> GetChatResponseAsync(IStatusContext context, string input, CancellationToken cancellationToken)
    {
        try
        {
            HttpRequestMessage request = PrepareForChat(input);
            HttpResponseMessage response = await _client.SendAsync(request, cancellationToken);
            response.EnsureSuccessStatusCode();

            context?.Status("Receiving Payload ...");
            Console.Write(response.Content);
            var content = await response.Content.ReadAsStreamAsync(cancellationToken);
            return JsonSerializer.Deserialize<ResponseData>(content);
        }
        catch (OperationCanceledException)
        {
            // Operation was cancelled by user.
        }

        return null;
    }
}

```

### Step 8: Call the chat service

Now we can call the chat service in the main agent class.

Modify the `Chat` method to call the chat service and render the response to the user. The following
code shows the completed `Chat` method.

```csharp
public async Task<bool> Chat(string input, IShell shell)
{
    // Get the shell host
    IHost host = shell.Host;

    // get the cancellation token
    CancellationToken token = shell.CancellationToken;

    if (Process.GetProcessesByName("ollama").Length is 0)
    {
        host.RenderFullResponse("Please be sure the ollama is installed and server is running. Check all the prerequisites in the README of this agent are met.");
        return false;
    }

    ResponseData ollamaResponse = await host.RunWithSpinnerAsync(
        status: "Thinking ...",
        func: async context => await _chatService.GetChatResponseAsync(context, input, token)
    ).ConfigureAwait(false);

    if (ollamaResponse is not null)
    {
        // render the content
        host.RenderFullResponse(ollamaResponse.response);
    }

    return true;
}
```

Congratulations! The agent is now complete. You can build and test the agent to confirm it's
working. Compare your code to the example code in the [`shell/agents/AIShell.Ollama.Agent`][04]
folder to see if you missed a step.

## How can I share my own agent?

Currently there is no way to share your agents in a centralized repository. We suggest forking this
repository for development of your own agent. You can share a link your fork in the `Agent Sharing`
section of the [Discussions][03] tab of this repository. To use an agent, if you put its `dll` files
in the `agents` folder of the base directory of `aish.exe`, the agent will be loaded by `aish`.

<!-- link references -->
[01]: https://github.com/ollama/ollama
[02]: https://github.com/ollama/ollama/blob/main/docs/api.md#request-no-streaming
[03]: https://github.com/PowerShell/ProjectMercury/discussions/categories/agent-sharing
[04]: https://github.com/PowerShell/ProjectMercury/shell/agents/AIShell.Ollama.Agent
[05]: https://github.com/PowerShell/ProjectMercury/shell/README.md
[06]: https://github.com/PowerShell/ProjectMercury/shell/shell.common.props

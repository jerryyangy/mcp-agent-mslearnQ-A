# mcp-agent-mslearnQ&A
This is to build an agent that connects to a cloud-hosted MCP server. The agent will use AI-powered search to help developers find accurate, real-time answers from Microsoft’s official documentation. 
It is useful for building assistants that support developers with up-to-date guidance on tools like Azure, .NET, and Microsoft 365. The agent will use the available MCP tools to query the documentation and return relevant results.

## Steps:
### Step 1: Create Foundry project
In the Foundry portal, you choose Create an agent, supply project details (Foundry resource, subscription, resource group), and select a supported region (e.g., West US, Norway East, Switzerland North, UAE North, South India).

After the project is created, you open the Overview page and copy the Foundry project endpoint to use later in the client application configuration.

### Step 2: Get and configure the sample app
In Azure portal Cloud Shell (PowerShell, classic mode), clone this repo and navigate to /Python.

Create a virtual environment, install dependencies (azure-ai-projects, azure-ai-agents, mcp, etc.), and edit .env to set your project endpoint and model deployment name (typically gpt-4o).

### Step 3: Wire the agent to the MCP server
In client.py, add imports for DefaultAzureCredential, AgentsClient, McpTool, ToolSet, and ListSortOrder, then connect an AgentsClient using the project endpoint and default credentials.

Configure an McpTool pointing at the Microsoft Docs MCP server (microsoft.docs.mcp), add it to a ToolSet, set approval mode to "never", and create an agent with instructions to use this MCP server for searching Microsoft’s latest documentation.

### Step 4: Run the agent and clean up
The code creates a thread, prompts the user for a question (for example, Azure CLI commands for Container Apps with managed identity), posts a user message, and starts a run that automatically invokes MCP tools such as microsoft_code_sample_search.

The app prints run status, steps, and MCP tool calls, showing that the agent used the remote MCP server to fulfill the request; after finishing, you delete the Azure resource group to avoid ongoing charges.

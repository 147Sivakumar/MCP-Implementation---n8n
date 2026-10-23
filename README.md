# AI Agent with MCP Enabled (n8n)

## Overview
This project demonstrates an AI agent workflow built in **n8n** that uses the **Model Context Protocol (MCP)** to connect an AI model to external tools. The workflow accepts a chat message, processes it with an AI Agent, and can call an MCP-connected Google Search tool to retrieve information.

## Workflow Architecture
The workflow shown in the screenshot contains these main nodes:

1. **When chat message received** — Starts the workflow when a user sends a message through the n8n chat interface.
2. **AI Agent** — Interprets the user's request and decides whether to answer directly or use a connected tool.
3. **OpenAI Chat Model** — Provides the language model used by the AI Agent.
4. **Simple Memory** — Supplies conversation memory so the agent can use context from the chat.
5. **MCP Client** — Connects the agent to tools exposed by an MCP server. The execution shown indicates a Google Search tool was called successfully.

## Example
A sample request visible in the execution panel is:

- **Search query:** `best tea shops in Puducherry`
- **Location:** `Puducherry`
- **Tool:** `MCP_Client_Google_search`

The MCP Client returned a successful response for the tool call.

## How It Works
1. A user submits a message in the n8n chat.
2. The AI Agent analyzes the request and decides whether external information is needed.
3. If needed, the agent calls a tool exposed through the MCP Client.
4. The tool returns its result to the agent.
5. The agent uses the result to compose a response in the chat.

## Setup Notes
To recreate this workflow in your own n8n instance:

1. Add a **When chat message received** trigger.
2. Add an **AI Agent** node and connect the trigger to it.
3. Connect an **OpenAI Chat Model** to the AI Agent's **Chat Model** input, and configure valid credentials.
4. Add **Simple Memory** to the AI Agent's **Memory** input if conversation context is required.
5. Configure an MCP-compatible server that exposes the desired tools (for example, a Google Search tool).
6. Add an **MCP Client** node and connect it to the AI Agent's **Tool** input.
7. Configure the MCP server endpoint and authentication as required by your server.
8. Test the workflow in the chat interface and confirm that the MCP tool execution succeeds.

> **Security:** Keep API keys and MCP credentials in n8n credentials or environment variables. Do not commit secrets, tokens, or private endpoint credentials to source control.

## Requirements
- An n8n instance with AI Agent and MCP Client nodes available.
- Valid credentials for the configured chat model.
- A reachable MCP server endpoint with the required tool(s).
- Any API credentials required by the external search service.

## Troubleshooting
- **Tool is not called:** Check the AI Agent's tool connection and its instructions.
- **Connection errors:** Verify the MCP server endpoint, network access, and authentication.
- **Unexpected answers:** Check the model configuration, tool descriptions, and the data returned by the MCP server.
- **Missing chat context:** Confirm that Simple Memory is connected and configured correctly.

## Limitations
This README is based on the provided workflow screenshot. Exact node parameters, credentials, MCP server configuration, and deployment details are not visible, so they should be verified in the n8n editor.

## License
Add a license here if you intend to publish or distribute this project.

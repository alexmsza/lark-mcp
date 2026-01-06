# Lark MCP

<p align="right">
    <b>English</b> | <a href="./README_zh.md">简体中文</a>
</p>

[![GitHub last commit](https://img.shields.io/github/last-commit/ZhanZiyuan/lark-mcp)](https://github.com/ZhanZiyuan/lark-mcp/commits/main/)
[![GitHub License](https://img.shields.io/github/license/ZhanZiyuan/lark-mcp)](https://github.com/ZhanZiyuan/lark-mcp/blob/main/LICENSE)
[![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/ZhanZiyuan/lark-mcp/total)](https://github.com/ZhanZiyuan/lark-mcp/releases)

This extension integrates the official Lark (Feishu) MCP server into the Gemini CLI.
It allows you to interact with Lark documents, calendars, search,
and knowledge base directly from your terminal using natural language or custom commands.

## Features

- **Document Management**: Read and summarize Lark Docs.
- **Search**: Search specifically through Wiki, Chat history, or general files.
- **Calendar**: Retrieve personal agenda and calendar events.
- **Directory**: Look up employee information and contact details.

## Prerequisites

- **Node.js**: Ensure Node.js is installed on your system.
- **Gemini CLI**: Ensure the Gemini CLI is installed and updated.
- **Lark/Feishu Account**: You need access to a Lark/Feishu tenant.

## Installation

- Create a directory for the project (e.g., `lark-mcp`) and place the extension files inside.
- Open your terminal and navigate to this directory.

## Configuration (Important)

Before using the extension, you **must** configure your credentials in the `gemini-extension.json` file.
This is required for the MCP server to authenticate with the Lark Open Platform.

- Open `gemini-extension.json`.
- Locate the `args` array inside `mcpServers`.
- Replace the placeholders with your actual credentials.

  ```json
  {
    "name": "lark-mcp",
    "version": "1.0.0",
    "description": "A Gemini CLI extension for Lark's MCP server.",
    "contextFileName": "GEMINI.md",
    "mcpServers": {
      "lark-mcp": {
        "command": "npx",
        "args": [
          "-y",
          "@larksuiteoapi/lark-mcp",
          "mcp",
          "-a",
          "<your_app_id>",
          "-s",
          "<your_app_secret>",
          "-u",
          "<your_user_token>"
        ]
      }
    }
  }
  ```

**How to get credentials:**

- **App ID & App Secret**:
  - Go to the [Lark Developer Console](https://open.feishu.cn/app).
  - Create a custom app or select an existing one.
  - You will find the **App ID** and **App Secret** under "Basic Info" -> "Credentials".

- **User Token**:
  - For testing purposes, you can generate a user access token using the API Explorer.
  - Visit the [Lark API Explorer](https://open.feishu.cn/document/server-docs/docs/bitable-v1/app/create).
  - Click on **Get Token** (usually located on the right side or top bar of the debugging interface) to generate a temporary `user_access_token`.
  - Copy this token into the `<your_user_token>` field.

## Setup

Once you have updated the configuration file, link the extension to Gemini CLI:

```bash
gemini extensions link .
```

Or install the extension using the following command:

```bash
gemini extensions install https://github.com/ZhanZiyuan/lark-mcp
```

After running this command, restart your Gemini CLI session.

## Usage

### Natural Language

You can ask Gemini to perform tasks naturally:

- "Search for the project kickoff document in Wiki."
- "What is on my calendar for today?"
- "Find contact details for [Employee Name]."

### Custom Commands

This extension provides specific shortcuts for safer, read-only operations:

- **/lark:agenda**: Retrieve your calendar events.
  - Usage: `/lark:agenda` or `/lark:agenda "next Monday"`

- **/lark:search-wiki**: Search the Knowledge Base.
  - Usage: `/lark:search-wiki "Q3 Report"`

- **/lark:search-chat**: Search through chat history.
  - Usage: `/lark:search-chat "bug fix"`

- **/lark:whois**: Lookup employee information.
  - Usage: `/lark:whois "John Doe"`

- **/lark:read-doc**: Read the content of a specific document.
  - Usage: `/lark:read-doc "[Doc Token or URL]"`

## Troubleshooting

If the extension fails to respond or returns errors:

- **Check Credentials**: Ensure your token has not expired and that the App ID/Secret are correct in `gemini-extension.json`.
- **Permissions**: Ensure your Lark App has the necessary permissions enabled in the Developer Console (e.g., Calendar, Docs, Search, Contacts).
- **Re-link**: Try running `gemini extensions link .` again if you moved files.

---

*Based on the [Gemini CLI Extensions Guide](https://geminicli.com/docs/extensions/getting-started-extensions/) and [Lark OpenAPI MCP](https://github.com/larksuite/lark-openapi-mcp/blob/main/README.md).*

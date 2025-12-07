# Trello MCP Integration for Poke AI

This repository hosts the **Model Context Protocol (MCP)** server that bridges **Poke AI** with your Trello workspace. It empowers Poke AI to directly manage your Trello boards, lists, and cards, turning it into a capable project management assistant.

With this integration, Poke AI can:
*   **Organize Your Work**: Create new boards for projects and lists for stages (e.g., "To Do", "In Progress").
*   **Manage Tasks**: Create cards, add detailed descriptions, assign members, and set due dates.
*   **Keep You Updated**: Read comments, checking status, and moving cards as work progresses.
*   **Search**: Instantly find any card or board across your workspace.

## Features

- **Full Board Control**: List, view, create, and update boards.
- **List Management**: Create, archive, and reorder lists to match your workflow.
- **Card Operations**: Comprehensive CRUD (Create, Read, Update, Delete) support for cards.
- **Collaboration**: Add comments and manage card assignments.
- **Smart Search**: Poke AI can intelligently search your Trello content.

## Prerequisites

- **Node.js**: v18.17 or higher.
- **Trello Account**: You need an active Trello account.
- **API Credentials**: A Trello API Key and Token.

## Setup Guide

### 1. Installation

Clone this repository and install the necessary dependencies:

```bash
npm install
# or
pnpm install
```

Build the project:

```bash
npm run build
# or
pnpm build
```

### 2. Configuration

You need to provide your Trello credentials so Poke AI can act on your behalf.

1.  **Get your Credentials**:
    - Visit [https://trello.com/app-key](https://trello.com/app-key).
    - Copy your **Personal Key**.
    - Click the "Token" link under the key to generate a **Token**.

2.  **Set Environment Variables**:
    - Create a `.env` file in the root directory (you can copy `.env.example`).
    - Fill in your details:
      ```env
      PORT=8787
      BASE_URL=http://localhost:8787
      TRELLO_API_BASE=https://api.trello.com/1
      TRELLO_KEY=your_copied_personal_key
      TRELLO_TOKEN=your_generated_token
      LOG_LEVEL=info
      ```

### 3. Connecting to Poke AI

Poke AI interacts with this server using the **stdio** transport or **SSE** (Server-Sent Events).

#### Option A: Local Interaction (Recommended for Desktop)

Configure Poke AI (or your MCP client) to run the server directly:

```json
{
  "mcpServers": {
    "trello-poke": {
      "command": "node",
      "args": [
        "/absolute/path/to/Trello-MCP-Poke-Integration/dist/bin/stdio.js"
      ],
      "env": {
        "TRELLO_KEY": "your_key_here", // Optional if set in .env
        "TRELLO_TOKEN": "your_token_here"
      }
    }
  }
}
```

#### Option B: Remote / HTTP Interaction

Start the server in HTTP mode:

```bash
npm start
```

Then point Poke AI to the SSE endpoint:
`http://localhost:8787/mcp/sse`

## Troubleshooting

-   **"No tools found"**: Ensure you have built the project (`npm run build`) and the path to `dist/bin/stdio.js` is correct.
-   **Connection Issues**: Check that your `TRELLO_KEY` and `TRELLO_TOKEN` are correct in the `.env` file.
-   **Zod Errors**: If you see errors about validation, ensure you are using the specific dependencies version pinned in `package.json`.

## License

ISC

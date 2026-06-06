# Figma MCP Server

This workspace contains a local Python MCP server that lets VS Code or another MCP client read Figma files using a Figma personal access token from `.env`.

## Setup

1. Install Python's virtual environment and pip support if your system does not already have them:

   ```bash
   sudo apt install python3-venv python3-pip
   ```

2. Create a virtual environment and install dependencies:

   ```bash
   python3 -m venv .venv
   .venv/bin/python -m pip install -r requirements.txt
   ```

3. Create `.env` from the example:

   ```bash
   cp .env.example .env
   ```

4. Open `.env` and replace the placeholder:

   ```dotenv
   FIGMA_TOKEN=your_real_figma_token
   FIGMA_FILE_ID=your_figma_file_id
   FIGMA_NODE_IDS=16:802
   ```

5. Open this folder in VS Code.

6. Run `MCP: Open Workspace Folder MCP Configuration` from the Command Palette and confirm `.vscode/mcp.json` contains the `figmaMcp` server.

7. Start or restart the server from VS Code's MCP controls.

## Tools

- `get_figma_file(file_id)`: reads the full Figma file JSON.
- `get_configured_figma_file()`: reads the full Figma file JSON for `FIGMA_FILE_ID` from `.env`.
- `get_figma_nodes(file_id, node_ids)`: reads specific Figma nodes.
- `get_configured_figma_nodes()`: reads only the nodes listed in `FIGMA_NODE_IDS` from `.env`.
- `get_figma_file_images(file_id, node_ids, scale, image_format)`: creates image URLs for specific nodes.

## Section or Frame Node IDs

For section-by-section reads, copy a section, frame, or group link from Figma.

If the URL has:

```text
node-id=16-802
```

use this in `.env`:

```dotenv
FIGMA_NODE_IDS=16:802
```

For multiple sections:

```dotenv
FIGMA_NODE_IDS=16:802,22:105,31:9
```

## Figma File ID

For a URL like:

```text
https://www.figma.com/file/FILE_ID/design-name
```

use `FILE_ID` as the `file_id`.

For newer Figma URLs like:

```text
https://www.figma.com/design/FILE_ID/design-name
```

use the same `FILE_ID` part after `/design/`.

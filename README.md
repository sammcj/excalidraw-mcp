# Excalidraw MCP App Server

MCP server that streams hand-drawn Excalidraw diagrams with smooth viewport camera control and interactive fullscreen editing.

![Demo](docs/demo.gif)

## Install

Works with any client that supports [MCP Apps](https://modelcontextprotocol.io/docs/extensions/apps) — Claude, ChatGPT, VS Code, Goose, and others. If something doesn't work, please [open an issue](https://github.com/antonpk1/excalidraw-mcp-app/issues).

### Remote (recommended)

Add as a remote MCP server in your client. For example, in [claude.ai](https://claude.ai):

1. Go to **Settings** → **Connectors** → **Add custom connector**
2. Server URL: `https://excalidraw-mcp-app.vercel.app/mcp` :point_left:
3. Done — start using Excalidraw in your conversations

### Local

<details>
<summary>Download extension or build from source</summary>

**Option A: Download Extension**

1. Download `excalidraw-mcp-app.mcpb` from [Releases](https://github.com/antonpk1/excalidraw-mcp-app/releases)
2. Double-click to install in Claude Desktop

**Option B: Build from Source**

```bash
git clone https://github.com/antonpk1/excalidraw-mcp-app.git
cd excalidraw-mcp-app
npm install && npm run build
```

Add to `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "excalidraw": {
      "command": "node",
      "args": ["/path/to/excalidraw-mcp-app/dist/index.js", "--stdio"]
    }
  }
}
```

Restart Claude Desktop.

</details>

## Usage

Example prompts:
- "Draw a cute cat using excalidraw"
- "Draw an architecture diagram showing a user connecting to an API server which talks to a database"

## What are MCP Apps and how can I build one?

Text responses can only go so far. Sometimes users need to interact with data, not just read about it. [MCP Apps](https://github.com/modelcontextprotocol/ext-apps/) is an official Model Context Protocol extension that lets servers return interactive HTML interfaces (data visualizations, forms, dashboards) that render directly in the chat.

- **Getting started for humans**: [documentation](https://modelcontextprotocol.io/docs/extensions/apps)
- **Getting started for AIs**: [skill](https://github.com/modelcontextprotocol/ext-apps/blob/main/plugins/mcp-apps/skills/create-mcp-app/SKILL.md)

<details>
<summary>Releasing a New Version</summary>

```bash
# 1. Make changes, commit, push
git add -A && git commit -m "..." && git push

# 2. Bump version in manifest.json and package.json

# 3. Rebuild
npm run build

# 4. Pack the .mcpb bundle
mcpb pack .

# 5. Create GitHub release with bundle attached
gh release create v0.3.0 excalidraw-mcp-app.mcpb --title "v0.3.0" --notes "What changed"

# 6. Deploy to Vercel
docker exec smithery bash -c 'cd /app && git pull && npx vercel --prod --yes'
```

</details>

## Credits

Built with [Excalidraw](https://github.com/excalidraw/excalidraw) — a virtual whiteboard for sketching hand-drawn like diagrams.

## License

MIT

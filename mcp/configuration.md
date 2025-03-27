# Configuring MCP Servers

MCP uses a **JSON-based configuration file**.

## Example (Stdio MCP Server using Node.js)
```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["-y", "mcp-server"],
      "env": {
        "API_KEY": "value"
      }
    }
  }
}
```

## Notes
- `command`: Defines the executable (e.g., `npx`)
- `args`: Arguments passed to the command
- `env`: Environment variables (e.g., API keys)

## Configuration Locations

### Project-Specific Configuration
📂 **`.cursor/mcp.json`** → Only applies to **that specific project**

### Global Configuration
🏠 **`~/.cursor/mcp.json`** → Available **across all projects**

## Tip
Add `.cursor/mcp.json` to your global `.gitignore` to prevent committing sensitive configurations. 
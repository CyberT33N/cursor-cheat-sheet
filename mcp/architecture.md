# MCP Architecture

MCP servers are **lightweight programs** that expose capabilities via a standardized protocol. They act as **bridges** between Cursor and external tools or data sources.

## Supported Transport Types

### 💻 Stdio Transport (Local Only)
- Runs **on your local machine**
- Managed automatically by Cursor
- Communicates via **stdout**
- **Only accessible locally**

✅ **Input:** A **shell command** executed by Cursor

### 🌐 SSE Transport (Local or Remote)
- Can run **locally or remotely**
- Managed and run **by you**
- Communicates **over the network**
- **Can be shared across multiple machines**

✅ **Input:** A **URL** to the `/sse` endpoint of an external MCP server

## Choosing the Right Transport

- **Use stdio** for quick local development.
- **Use SSE** for team-wide, distributed MCP setups. 
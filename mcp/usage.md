# Using MCP Tools in Cursor

## Automatic Tool Usage
- The **Composer Agent** will automatically use relevant MCP tools listed under **Available Tools** in the MCP settings.
- You can also **directly prompt** the agent to use a specific tool by name or description.

## Tool Approval
- By default, Cursor **asks for approval** before using an MCP tool.
- You can review the tool call **arguments** before executing.

## Yolo Mode (Auto-Execute MCP Tools)
- **Enabling Yolo Mode** allows Cursor to **automatically run MCP tools** without approval, just like terminal commands.

## Tool Responses

When an MCP tool runs, Cursor will **display the response in chat**, along with:
- **Tool call arguments**
- **Expanded tool response details** 
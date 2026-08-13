# Tools

- Reference: https://docs.cursor.com/chat/tools
- Scope: complete non-MCP tool inventory exposed in this chat session.
- MCP server-specific tools, including Filesystem Extended, are intentionally excluded.

## Tool Architecture

A callable tool identifier has two parts:

```text
<namespace>.<tool>
```

Example:

```text
functions.ReadFile
```

- `functions` is the primary built-in tool namespace.
- `ReadFile` is the underlying operation.
- `multi_tool_use` is a separate orchestration namespace.
- MCP integration is available through built-in `functions` tools, but individual MCP-server tools are excluded from this document as requested.

### Star (`*`) notation

`functions.*` is documentation shorthand for “all tools in the `functions` namespace.”

It is not a callable RPC name:

```text
Correct:   functions.ReadFile
Incorrect: functions.*
```

Markdown stars have a separate, purely visual purpose:

```markdown
* Bullet item
**Bold text**
```

They do not affect tool execution or tool architecture.

### Compatibility notice

This document changes no runtime behavior. However, old names such as `functions.read_file` and `functions.run_terminal_cmd` are no longer exposed under those names. Any automation calling them must migrate to the exact current identifiers below.

---

# 1. Functions

## 1.1 File, repository, and code inspection

- `functions.ReadFile` — read a file, optionally by line range.
- `functions.Glob` — find files by glob pattern.
- `functions.rg` — search file contents using regex.
- `functions.ReadLints` — read IDE lint diagnostics.

### `functions.ReadFile`

Read an entire file:

```json
{
  "path": "C:\\absolute\\path\\to\\base.md"
}
```

Read a portion of a file:

```json
{
  "path": "C:\\absolute\\path\\to\\base.md",
  "offset": 1,
  "limit": 250
}
```

Parameters:

- `path: string` — required absolute file path.
- `offset?: integer` — optional 1-based starting line.
- `limit?: integer` — optional number of lines to return.

Iterative read example:

```json
{
  "path": "C:\\absolute\\path\\to\\base.md",
  "offset": 1,
  "limit": 250
}
```

Then continue from the next unread line:

```json
{
  "path": "C:\\absolute\\path\\to\\base.md",
  "offset": 251,
  "limit": 250
}
```

Unlike the legacy tool, the current response does not promise a total-line-count field. Continue until no more content is returned.

### `functions.Glob`

```json
{
  "target_directory": "C:\\absolute\\path\\to\\repository",
  "glob_pattern": "**/*.go"
}
```

- `target_directory?: string` — search root.
- `glob_pattern: string` — required file pattern.

### `functions.rg`

```json
{
  "pattern": "func\\s+Main",
  "path": "C:\\absolute\\path\\to\\repository",
  "glob": "*.go",
  "output_mode": "content"
}
```

Common parameters:

- `pattern: string` — required regular expression.
- `path?: string` — search root.
- `glob?: string` — restrict matching files.
- `output_mode?: "content" | "files_with_matches" | "count"`
- `head_limit?: number`
- `offset?: number`
- `-A`, `-B`, `-C` — context lines.
- `i?: boolean` — case-insensitive search.
- `multiline?: boolean` — enable multiline regex matching.

### `functions.ReadLints`

```json
{
  "paths": [
    "C:\\git\\test\\eslint.config.ts"
  ]
}
```

Parameters:

- `paths?: string[]` — optional file or directory list.
- If omitted, lint diagnostics are read for the entire workspace.
- No additional filtering parameters are exposed.

---

## 1.2 File and notebook changes

- `functions.ApplyPatch` — create or modify one text file through a patch.
- `functions.Delete` — delete one file.
- `functions.EditNotebook` — edit or create a Jupyter notebook cell.

There is no direct `functions.edit_file`, `functions.search_replace`, or `functions.write_file` tool in the current API.

### `functions.ApplyPatch`

`ApplyPatch` uses a patch payload rather than JSON arguments:

```text
*** Begin Patch
*** Update File: C:\absolute\path\to\file.txt
@@
-old content
+new content
*** End Patch
```

Create a file:

```text
*** Begin Patch
*** Add File: C:\absolute\path\to\new-file.txt
+Initial content
*** End Patch
```

### `functions.Delete`

```json
{
  "path": "C:\\absolute\\path\\to\\obsolete-file.txt"
}
```

### `functions.EditNotebook`

```json
{
  "target_notebook": "C:\\absolute\\path\\to\\analysis.ipynb",
  "cell_idx": 0,
  "is_new_cell": false,
  "cell_language": "python",
  "old_string": "old cell content",
  "new_string": "new cell content"
}
```

Required fields:

- `target_notebook`
- `cell_idx`
- `is_new_cell`
- `cell_language`
- `old_string`
- `new_string`

---

## 1.3 Shell execution and task tracking

- `functions.Shell` — run a shell command.
- `functions.AwaitShell` — inspect or wait for a background shell process.
- `functions.TodoWrite` — update the internal task list.

### `functions.Shell`

```json
{
  "command": "go test ./...",
  "working_directory": "C:\\absolute\\path\\to\\repository",
  "description": "Run Go test suite"
}
```

### `functions.AwaitShell`

```json
{
  "shell_id": "shell-id",
  "block_until_ms": 30000
}
```

### `functions.TodoWrite`

```json
{
  "merge": true,
  "todos": [
    {
      "id": "inspect",
      "content": "Inspect the repository",
      "status": "in_progress"
    },
    {
      "id": "verify",
      "content": "Run verification",
      "status": "pending"
    }
  ]
}
```

---

## 1.4 Web, images, and user interaction

- `functions.WebSearch` — search the web for current information.
- `functions.WebFetch` — retrieve and read a web page.
- `functions.GenerateImage` — generate an image from a prompt.
- `functions.AskQuestion` — ask the user structured multiple-choice questions.

### `functions.WebSearch`

```json
{
  "search_term": "Cursor Agent tools documentation",
  "explanation": "Verify current public documentation."
}
```

### `functions.WebFetch`

```json
{
  "url": "https://docs.cursor.com/chat/tools"
}
```

### `functions.GenerateImage`

```json
{
  "description": "A minimal flat vector application icon for a note-taking app.",
  "filename": "notes-icon.png",
  "aspect_ratio": "1:1"
}
```

### `functions.AskQuestion`

```json
{
  "title": "Deployment choice",
  "questions": [
    {
      "id": "environment",
      "prompt": "Which environment should receive the release?",
      "options": [
        {
          "id": "staging",
          "label": "Staging"
        },
        {
          "id": "production",
          "label": "Production"
        }
      ],
      "allow_multiple": false
    }
  ]
}
```

---

## 1.5 Modes and delegation

- `functions.SwitchMode` — request a mode change.
- `functions.Subagent` — launch or resume a specialized agent.

### `functions.SwitchMode`

```json
{
  "target_mode_id": "plan",
  "explanation": "The task needs an implementation design before code changes."
}
```

Allowed mode IDs:

- `plan`
- `agent`

A user approval is required before changing modes.

### `functions.Subagent`

This workspace has a policy that subagents may only be started when the user explicitly requests them.

Typical fields include:

```json
{
  "description": "Review API design",
  "prompt": "Inspect the API design and report the important trade-offs.",
  "subagent_type": "generalPurpose",
  "run_in_background": false
}
```

---

## 1.6 MCP framework functions

These are built-in `functions` tools. They support MCP integrations, but this document intentionally excludes all individual MCP-server tools.

- `functions.GetMcpTools` — discover MCP servers and their tool schemas.
- `functions.FetchMcpResource` — read an MCP resource.
- `functions.CallMcpTool` — invoke a discovered MCP tool.

Correct architectural sequence:

```text
functions.GetMcpTools
        ↓
functions.CallMcpTool
```

Example discovery call:

```json
{
  "server": "example-server",
  "toolName": "example-tool"
}
```

Example MCP invocation:

```json
{
  "server": "example-server",
  "toolName": "example-tool",
  "description": "Perform the requested operation.",
  "arguments": {}
}
```

---

# 2. Orchestration

## `multi_tool_use.parallel`

Runs independent developer-tool calls concurrently.

```json
{
  "tool_uses": [
    {
      "recipient_name": "functions.Glob",
      "parameters": {
        "target_directory": "C:\\absolute\\path\\to\\repository",
        "glob_pattern": "**/*.go"
      }
    },
    {
      "recipient_name": "functions.rg",
      "parameters": {
        "pattern": "TODO",
        "path": "C:\\absolute\\path\\to\\repository"
      }
    }
  ]
}
```

Only independent calls should be parallelized. A call that depends on another call’s result must run afterward.

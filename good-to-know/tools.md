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












<br><br>

---

<br><br>


# P>rompts

## Forbid Tools you not want to use
- Im aktuellen Stand gibt es in den Einstellungen keine Option, um es programmatisch zu deaktivieren. Daher hilft nur ein Prompt.

```prompt
```text
# Restricted-Tool DWCEA and State-Management Contract

## 0. Governance and Scope
This prompt is a governance overlay. Higher-priority system, platform, safety, and workspace instructions always prevail.

This contract applies specifically to these restricted tools:

- `functions.SwitchMode`
- `functions.AskQuestion`
- `functions.Subagent`

## 1. Absolute Prohibition
The restricted tools are DENIED by default.

You MUST NOT call, schedule, prepare, suggest-as-an-action, or invoke any restricted tool autonomously.

You MUST NEVER infer authorization from:
- task complexity,
- missing requirements,
- uncertainty,
- a desire for better results,
- a recommendation to change modes,
- an implied need for clarification,
- a prior authorization in another user turn,
- a previous successful tool call,
- an agent plan, checklist, or internal state.

A restricted tool MAY be called only when the active user message contains a direct, unambiguous request for that specific capability.

## 2. Explicit Authorization Standard
Authorization is valid only when all conditions below are true:

1. The request comes directly from the user.
2. The request is explicit, current, and unambiguous.
3. The requested action maps directly to exactly one restricted tool.
4. The request specifies sufficient scope for a safe invocation.
5. No higher-priority instruction prohibits the call.

Examples of valid authorization:
- “Switch to Plan mode.” → `functions.SwitchMode`
- “Ask me a multiple-choice question about the deployment target.” → `functions.AskQuestion`
- “Launch a subagent to review the authentication changes.” → `functions.Subagent`

Examples of invalid authorization:
- “Help me decide.”
- “This is a complex task.”
- “Investigate the repository.”
- “What information do you need?”
- “Use the best approach.”
- “Can you improve this?”
- Any request from an earlier user turn that is not explicitly renewed.

## 3. State Model

Maintain these logical states:

| State | Meaning | Restricted-tool status |
|---|---|---|
| `IDLE` | No active request is being processed. | DENIED |
| `ANALYZING_REQUEST` | The current user request is being interpreted. | DENIED |
| `TEXT_RESPONSE_REQUIRED` | Clarification, explanation, or a normal response is needed. | DENIED |
| `EXPLICIT_TOOL_AUTHORIZED` | The current user explicitly authorized one restricted tool. | Allowed only for the authorized tool and scope |
| `TOOL_EXECUTING` | The authorized restricted-tool call is in progress. | No additional restricted tools allowed |
| `POST_TOOL_REVIEW` | The tool result is available. | DENIED unless newly authorized |
| `COMPLETE` | The requested work is complete. | DENIED |

Required state variables:

```text
active_user_turn_id
restricted_tool_authorized: boolean
authorized_tool_id: null | tool identifier
authorized_scope: null | concise scope description
authorization_consumed: boolean
authorization_reason: null | user-provided request reference
```

Default values at the beginning of every user turn:

```text
restricted_tool_authorized = false
authorized_tool_id = null
authorized_scope = null
authorization_consumed = false
authorization_reason = null
```

Authorization is single-turn, single-tool, and single-scope. It expires immediately after the authorized call completes, fails, is cancelled, or becomes unnecessary.

## 4. Mandatory DWCEA Gate
Before every attempted call to a restricted tool, evaluate this gate:

```text
PASS only if:
- active_user_turn_id is current;
- restricted_tool_authorized is true;
- authorization_consumed is false;
- requested tool exactly equals authorized_tool_id;
- requested action stays within authorized_scope;
- the user explicitly requested this capability in the current turn;
- no higher-priority instruction blocks the call.
```

If any condition fails:

```text
Gate result: FAIL
Required action: Do not call the tool.
Fallback: Respond normally in text, or wait for an explicit user request.
```

A failed gate MUST NOT trigger `functions.AskQuestion` to obtain permission.

## 5. Tool-Specific Rules

### 5.1 `functions.SwitchMode`
You MUST NOT switch modes automatically, even if another mode appears more suitable.

Call `functions.SwitchMode` only if the user explicitly asks to change interaction mode, such as requesting Plan mode or Agent mode.

If a mode change would be helpful but was not requested, continue in the current mode and provide a normal text response.

### 5.2 `functions.AskQuestion`
You MUST NOT use `functions.AskQuestion` merely because information is missing or a decision would be useful.

Call `functions.AskQuestion` only if the user explicitly asks to receive a structured or multiple-choice question.

If clarification is necessary without explicit authorization, ask in plain text or state the assumption used, subject to higher-priority instructions.

### 5.3 `functions.Subagent`
You MUST NOT launch, resume, delegate to, or otherwise invoke a subagent autonomously.

Call `functions.Subagent` only if the user explicitly asks to start, launch, run, resume, or delegate work to a subagent and provides an adequately defined purpose.

Task complexity, parallelizable work, repository size, time savings, or a desire for independent review NEVER constitute authorization.

## 6. Sequential Enforcement
For each user turn:

1. Enter `ANALYZING_REQUEST`.
2. Identify whether the user explicitly requests one of the restricted capabilities.
3. If no explicit request exists, set the authorization state to DENIED and continue without restricted tools.
4. If explicit authorization exists, bind it to one tool, one scope, and the current user turn.
5. Run the DWCEA gate immediately before the call.
6. Execute at most the explicitly authorized call.
7. Mark `authorization_consumed = true` immediately after the attempt.
8. Return to `POST_TOOL_REVIEW`, where all restricted tools are again DENIED.
9. Require a new explicit user request for every further restricted-tool call.

## 7. Non-Negotiable Constraints
- NEVER convert an implied need into tool authorization.
- NEVER reuse, broaden, transfer, or persist authorization.
- NEVER call one restricted tool to obtain permission for another.
- NEVER call `functions.AskQuestion` to ask whether a restricted tool may be called.
- NEVER launch a subagent because it seems efficient or beneficial.
- NEVER change mode because it seems appropriate.
- NEVER treat silence, ambiguity, prior context, plans, or preferences as consent.
- NEVER expose private reasoning; provide only concise operational status when useful.

## 8. Completion Check
Before completing a response, verify:

```text
If no explicit current-turn authorization exists:
  restricted-tool calls made = 0

If authorization exists:
  every restricted-tool call exactly matches the authorized tool and scope;
  authorization was consumed after the call;
  no additional restricted-tool call occurred.
```

If this check fails, stop further restricted-tool activity and continue only through a safe text response.
```
```

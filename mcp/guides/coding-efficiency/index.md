# 🛠️ Working Global Configs

<details><summary>Click to expand..</summary>
  
## 🖥️ Linux

<details><summary>Click to expand..</summary>

### Local 

<details><summary>Click to expand..</summary>

```javascript
{
  "mcpServers": {
    "server-sequential-thinking": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "mcp/sequentialthinking"
      ]
    },
    "exa": {
      "command": "npx",
      "args": [
        "-y",
        "exa-labs/exa-mcp-server"
      ],
      "env": {
        "EXA_API_KEY": "xxxxxxxxxxx"
      }
    },
    "openrouterai": {
      "command": "npx",
      "args": ["-y", "@mcpservers/openrouterai"],
      "env": {
        "OPENROUTER_API_KEY": "sk-or-v1-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
    },
    "browser-tools": {
      "command": "npx",
      "args": [
        "-y",
        "@agentdeskai/browser-tools-mcp"
      ],
      "enabled": true
    },
    "ucpf": {
       "command": "node",
       "args": ["/home/UserName/Projects/mcp/server/prompting/DeepLucid3D-MCP/build/index.js"],
       "env": {},
       "disabled": false,
       "autoApprove": []
    }
  }
}
```

</details>


<br><br>

### Cloud 


<details><summary>Click to expand..</summary>

```javascript

{
  "mcpServers": {
    "exa": {
      "command": "npx",
      "args": [
        "-y",
        "@smithery/cli@latest",
        "run",
        "exa",
        "--key",
        "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
      ]
    },
    "server-sequential-thinking": {
        "command": "npx",
        "args": [
          "-y",
          "@smithery/cli@latest",
          "run",
          "@smithery-ai/server-sequential-thinking",
          "--config",
          "{\"maxDepth\":8,\"parallelTasks\":true,\"enableSummarization\":true,\"thoughtCategorization\":true,\"progressTracking\":true,\"dynamicAdaptation\":true,\"contextWindow\":32768}"
        ]
     },
    "browser-tools": {
      "command": "npx",
      "args": [
        "-y",
        "@agentdeskai/browser-tools-mcp"
      ],
      "enabled": true
    },
    "openrouterai": {
      "command": "npx",
      "args": ["@mcpservers/openrouterai"],
      "env": {
        "OPENROUTER_API_KEY": "xxxxxxxxxxxxxxxxxx"
      }
    },
    "deeplucid3d-mcp": {
      "command": "npx",
      "args": [
        "-y",
        "@smithery/cli@latest",
        "run",
        "@MushroomFleet/deeplucid3d-mcp",
        "--config",
        "{\"defaultRenderer\":\"threejs\",\"shaderDebug\":true}"
      ]
    }
  }
}


```

</details>

</details>






<br><br>
<br><br>


## 🖥️ Windows

<details><summary>Click to expand..</summary>
  
### Local 

<details><summary>Click to expand..</summary>

```javascript
{
  "mcpServers": {
    "server-sequential-thinking": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "mcp/sequentialthinking"
      ]
    },
    "exa": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "exa-labs/exa-mcp-server"
      ],
      "env": {
        "EXA_API_KEY": "xxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
    },
    "openrouterai": {
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@mcpservers/openrouterai"],
      "env": {
        "OPENROUTER_API_KEY": "sk-or-v1-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
    },
    "browser-tools": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "@agentdeskai/browser-tools-mcp"
      ],
      "enabled": true
    }
  }
}
```

</details>


<br><br>

### Cloud 


<details><summary>Click to expand..</summary>

```javascript
{
  "mcpServers": {
    "server-sequential-thinking": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "@smithery/cli@latest",
        "run",
        "@smithery-ai/server-sequential-thinking",
        "--config",
        "{\"maxDepth\":8,\"parallelTasks\":true,\"enableSummarization\":true,\"thoughtCategorization\":true,\"progressTracking\":true,\"dynamicAdaptation\":true,\"contextWindow\":32768}"
      ]
    },
    "exa": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "@smithery/cli@latest",
        "run",
        "exa",
        "--config",
        "\"{\\\"exaApiKey\\\":\\\"xxxxxxxxxxxxxxxxxxxxxxxxxx\\\"}\""
      ]
    },
    "openrouterai": {
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@mcpservers/openrouterai"],
      "env": {
        "OPENROUTER_API_KEY": "sk-or-v1-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
    },
    "browser-tools": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "@agentdeskai/browser-tools-mcp"
      ],
      "enabled": true
    }
  }
}
```

</details>

</details>

</details>









<br><br>
<br><br>


---

# 📚 [Guide] Maximizing Coding Efficiency with MCP Sequential Thinking & OpenRouter AI
- Part1: [Guide Link](https://forum.cursor.com/t/guide-maximizing-coding-efficiency-with-mcp-sequential-thinking-openrouter-ai/66461)
- Part2: https://forum.cursor.com/t/guide-a-simpler-more-autonomous-ai-workflow-for-cursor/70688
- [Autonomous AI Workflow for Cursor](https://github.com/kleosr/cursorkleosr/tree/main)


---




# Dependencies


<details><summary>Click to expand..</summary>

- Always enforce project rules in .cursor/rules/*.mdc.

## Cursor Settings
```javascript
"cursor.general.enableShadowWorkspace": true
```
- Or activate in setting area and search for `shadow`


</details>




<br><br>
<br><br>




# Optional Dependencies


<details><summary>Click to expand..</summary>

# SpecStory Installation  

[Offizielle Dokumentation](https://docs.specstory.com/introduction)  

### Option 1 (Empfohlen)  

1. Stelle sicher, dass du die neueste Version von Cursor verwendest.  
2. Lade die Erweiterung herunter: **specstory-vscode-latest.vsix**  
3. Öffne in Cursor die **Command Palette** (`Ctrl/CMD-Shift-P`) und wähle:  
   - **Extensions: Install from VSIX…**  
4. Überprüfe die Installation:  
   - Öffne die **Command Palette** (`Ctrl/CMD-Shift-P`)  
   - Tippe **SpecStory** – die verfügbaren Befehle sollten angezeigt werden.  

Sobald SpecStory installiert ist, speichert es automatisch deinen Composer- und Chatverlauf im Verzeichnis:  
- ./specstory/history

Regarding the history generated by the specstory plugin, I ignore it in .cursorignore when I use it. Because I find that it affects the conversation


</details>




<br><br>
<br><br>




---


<br><br>
<br><br>


# 🧠 Good to Know
- **Avoid workspaces**: Open a window for each project because agents may search in the wrong directories.

---


<br><br>
<br><br>


# ❌ Kill All MCP Servers

## 🖥️ Windows

```shell
# windows
Get-Process node | ForEach-Object { $_.Kill() }
```


<br><br>
<br><br>

# 1. MCP Server

<details><summary>Click to expand..</summary>

---

# Cognitive Frameworks

# 🔄 Sequential Thinking
- https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/cognitive-frameworks/sequential-thinking/index.md

<br><br>

# 🔌 DeepLucid3D UCPF Server
- https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/cognitive-frameworks/deeplucid3d-ucpf/index.md




<br><br>
<br><br>

# 🔍 Searching
- [Search Servers ](https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/search.md)

<br><br>

## 🔧 Exa
- https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/search/exa/index.md




<br><br>
<br><br>

# Browser Automation

<br><br>

## 🌐 Browser Tools MCP
- https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/browser-automation/browser-tools/index.md




<br><br>
<br><br>

# AI Providers

## 🔌 OpenRouter
- https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/ai-providers/openrouter/index.md






</details>

<br><br>
<br><br>


---

# 📝 2. Cursor Rules
Include into your project:
- [Autonomous AI Workflow for Cursor](https://github.com/kleosr/cursorkleosr/tree/main#)

<details><summary>Click to expand..</summary>

I tweaked the logic by include everything into .agent folder to not bloat up your project root:

## `.agent/project_config.md`

- Example for specifc project_config.md in this case for electron-vite project
```markdown
# Project Configuration: CMCU

## Project Overview
- **Project Name:** CMCU (Secure File Vault)
- **Purpose:** A modern Electron.js application for secure file encryption and compression, featuring a sleek UI with Tailwind CSS and React
- **Primary Goal:** Build a secure, user-friendly desktop application that allows users to encrypt, compress, and manage files with strong security measures

## Tech Stack
- **Primary Languages:**
  - TypeScript (for both main and renderer processes)
  - React (for UI components in the renderer process)
- **Frameworks/Libraries:**
  - Electron (v28.x) for cross-platform desktop capabilities
  - React (v18.x) for UI components
  - Tailwind CSS for styling and UI design
  - Framer Motion / Motion / AnimeJS for animations
  - NextUI for React UI components
  - React Dropzone for file upload functionality
  - Vitest for testing framework
  - Electron Store for application state persistence
- **Build/Development Tools:**
  - Electron Vite for bundling and development workflow
  - ESLint v9 for code linting
  - TypeScript ESLint for TypeScript linting
  - Vite for frontend build tooling
  - Electron Builder for application packaging and distribution

## Project Structure
- **Main Architecture:**
  - Main Process (`/src/main`): Core Electron functionality, file system operations, security operations
  - Renderer Process (`/src/renderer`): UI components and frontend logic
  - Preload Scripts (`/src/preload`): Secure bridge between main and renderer processes
- **Key Directories:**
  - `/src/main/modules`: Core modules for application functionality
  - `/src/main/handlers`: IPC handlers for communication between processes
  - `/src/main/security`: Security-related functionality
  - `/src/main/windows`: Window management
  - `/src/renderer/src/components`: UI components
  - `/src/renderer/src/hooks`: Custom React hooks
  - `/src/renderer/src/services`: Frontend services
  - `/test`: Test files and configurations

## Critical Patterns & Conventions
- **Electron Architecture:**
  - Use strict process isolation between main and renderer
  - Implement proper IPC patterns for secure inter-process communication
  - Follow the principle of least privilege for main process operations
- **React Patterns:**
  - Use functional components with hooks
  - Implement proper state management patterns
  - Follow component composition patterns for UI reusability
- **TypeScript Standards:**
  - Use strong typing throughout the application
  - Define interfaces for all data structures
  - Utilize type-safe IPC communication between processes
- **Security Best Practices:**
  - Implement proper encryption for sensitive data
  - Follow secure coding practices for file operations
  - Validate all user inputs
  - Use secure defaults for all operations
- **Testing Strategy:**
  - Write comprehensive unit tests with Vitest
  - Implement proper mocking for Electron APIs in tests
  - Aim for high test coverage for critical functionality

## Development Workflow
- **Package Management:** Use npm for dependency management (consider migration to pnpm as noted in TODO)
- **Build Process:** Use Electron Vite and Electron Builder for development and distribution
- **Testing Approach:** Test-driven development with Vitest
- **Code Quality:** Follow ESLint rules and maintain high TypeScript type coverage

## External Dependencies
- **System Requirements:**
  - VeraCrypt CLI installed on the user's system
  - 7-Zip installed on the user's system
- **Runtime Dependencies:**
  - Node.js modules for file operations (fs-extra)
  - Encryption libraries via VeraCrypt integration
  - System privileges for certain operations (via sudo-prompt)

## Security Considerations
- **Data Handling:**
  - All encryption performed locally using VeraCrypt
  - No data transmission to external servers without user consent
  - Files securely encrypted before compression
- **Application Security:**
  - Proper content security policies
  - Secure IPC communication patterns
  - Sandboxed renderer process

## Constraints & Limitations
- **Platform Support:**
  - Windows, macOS, and Linux as target platforms
  - Different encryption behaviors may exist across platforms
- **Performance Considerations:**
  - Large file handling considerations
  - Memory management for encryption/compression operations
- **Distribution:**
  - Application distributed as NSIS installer (Windows), DMG (macOS), or AppImage/Snap/DEB (Linux)

## Future Considerations
- **Planned Features:**
  - Cloud integration capabilities
  - Better TypeScript linting as mentioned in TODOs
  - Migration to pnpm for package management
  - Proper implementation of preload scripts
```

## `.agent/workflow_state.md`
- I extended the original file with sequentiel thinking

```markdown
# Workflow State & Rules (STM + Rules)

*This file contains the dynamic state, embedded rules, and active plan for the current session.*
*It is read and updated frequently by the AI during its operational loop.*\
*Logs are now stored in a separate file: .agent/workflow_logs.md*

---

## State

*Holds the current status of the workflow.*

``yaml
Phase: ANALYZE # Current workflow phase (ANALYZE, BLUEPRINT, CONSTRUCT, VALIDATE, BLUEPRINT_REVISE)
Status: IN_PROGRESS # Current status (READY, IN_PROGRESS, BLOCKED_*, NEEDS_*, COMPLETED)
CurrentTaskID: MathCalculation # Identifier for the main task being worked on
CurrentStep: null # Identifier for the specific step in the plan being executed
``

---

## Plan

*Contains the step-by-step implementation plan generated during the BLUEPRINT phase.*\
*(This section will be populated by the AI during the BLUEPRINT phase)*

*Example:*\
*   `[ ] Step 1: Create file src/utils/helper.ts`\
*   `[ ] Step 2: Implement function \'calculateSum\' in helper.ts`\
*   `[ ] Step 3: Add unit tests for \'calculateSum\'`

---

## Rules

*Embedded rules governing the AI\'s autonomous operation.*

**# --- Core Workflow Rules ---**

RULE_WF_PHASE_ANALYZE:
  **Constraint:** Goal is understanding request/context. NO solutioning or implementation planning.

RULE_WF_PHASE_BLUEPRINT:
  **Constraint:** Goal is creating a detailed, unambiguous step-by-step plan. NO code implementation.

RULE_WF_PHASE_CONSTRUCT:
  **Constraint:** Goal is executing the `## Plan` exactly. NO deviation. If issues arise, trigger error handling or revert phase.

RULE_WF_PHASE_VALIDATE:
  **Constraint:** Goal is verifying implementation against `## Plan` and requirements using tools. NO new implementation.

RULE_WF_TRANSITION_01:
  **Trigger:** Explicit user command (`@analyze`, `@blueprint`, `@construct`, `@validate`).
  **Action:** Update `State.Phase` accordingly. Log phase change to `.agent/workflow_logs.md`.

RULE_WF_TRANSITION_02:
  **Trigger:** AI determines current phase constraint prevents fulfilling user request OR error handling dictates phase change (e.g., RULE_ERR_HANDLE_TEST_01).
  **Action:** Log the reason to `.agent/workflow_logs.md`. Update `State.Phase` (e.g., to `BLUEPRINT_REVISE`). Set `State.Status` appropriately (e.g., `NEEDS_PLAN_APPROVAL`). Report to user.

**# --- Cognitive Process Rules ---**

RULE_THINKING_PROTOCOL_01:
  **Guideline:** When analyzing problems, formulating plans, or troubleshooting, follow a structured thought process:
    1.  **Observe:** Clearly state the current situation, inputs, goals, and constraints based on LTM (`project_config.md`) and STM (`workflow_state.md`).
    2.  **Orient:** Identify the core problem or task. Recall relevant knowledge and rules.
    3.  **Hypothesize/Plan:** Generate potential solutions or next steps. Break down complex tasks. Consider alternatives and edge cases.
    4.  **Decide:** Select the most promising approach based on rules, constraints, and expected outcomes.
    5.  **Act:** Execute the chosen step using appropriate tools (code edits, terminal commands).
    6.  **Reflect & Verify:** Observe the outcome of the action. Did it achieve the goal? Are there errors? Does the STM need updating? Self-correct if necessary.
  **Application:** Primarily during `ANALYZE`, `BLUEPRINT`, `BLUEPRINT_REVISE` phases and within error handling rules (`RULE_ERR_HANDLE_*`). Log key reasoning steps.

**# --- Initialization & Resumption Rules ---**

RULE_INIT_01:
  **Trigger:** AI session/task starts AND `.agent/workflow_state.md` is missing or empty.
  **Action:**
    1. Create `.agent/workflow_state.md` with default structure.
    2. Create `.agent/workflow_logs.md` for logging.
    3. Read `.agent/project_config.md` (prompt user if missing).
    4. Set `State.Phase = ANALYZE`, `State.Status = READY`.
    5. Log "Initialized new session." to `.agent/workflow_logs.md`.
    6. Prompt user for the first task.

RULE_INIT_02:
  **Trigger:** AI session/task starts AND `.agent/workflow_state.md` exists.
  **Action:**
    1. Read `.agent/project_config.md`.
    2. Read existing `.agent/workflow_state.md`.
    3. Read existing `.agent/workflow_logs.md`.
    4. Log "Resumed session." to `.agent/workflow_logs.md`.
    5. Check `State.Status`: Handle READY, COMPLETED, BLOCKED_*, NEEDS_*, IN_PROGRESS appropriately (prompt user or report status).

RULE_INIT_03:
  **Trigger:** User confirms continuation via RULE_INIT_02 (for IN_PROGRESS state).
  **Action:** Proceed with the next action based on loaded state and rules.

**# --- Memory Management Rules ---**

RULE_MEM_READ_LTM_01:
  **Trigger:** Start of a new major task or phase.
  **Action:** Read `.agent/project_config.md`. Log action to `.agent/workflow_logs.md`.

RULE_MEM_READ_STM_01:
  **Trigger:** Before *every* decision/action cycle.
  **Action:** Read `.agent/workflow_state.md` and `.agent/workflow_logs.md`.

RULE_MEM_UPDATE_STM_01:
  **Trigger:** After *every* significant action or information receipt.
  **Action:** Immediately update relevant sections (`## State`, `## Plan`) in `.agent/workflow_state.md` and log the action to `.agent/workflow_logs.md`.

RULE_MEM_UPDATE_LOGS_01:
  **Trigger:** After *every* significant action or information receipt.
  **Action:** Immediately update `## Log` section in `.agent/workflow_logs.md` with timestamp and details.

RULE_MEM_UPDATE_LTM_01:
  **Trigger:** User command (`@config/update`) OR end of successful VALIDATE phase for significant change.
  **Action:** Propose concise updates to `.agent/project_config.md` based on `.agent/workflow_logs.md`/diffs. Set `State.Status = NEEDS_LTM_APPROVAL`. Await user confirmation.

RULE_MEM_VALIDATE_01:
  **Trigger:** After updating `.agent/workflow_state.md` or `.agent/project_config.md`.
  **Action:** Perform internal consistency check. If issues found, log to `.agent/workflow_logs.md` and set `State.Status = NEEDS_CLARIFICATION`.

**# --- Tool Integration Rules (Cursor Environment) ---**

RULE_TOOL_LINT_01:
  **Trigger:** Relevant source file saved during CONSTRUCT phase.
  **Action:** Instruct Cursor terminal to run lint command. Log attempt to `.agent/workflow_logs.md`. On completion, parse output, log result to `.agent/workflow_logs.md`, set `State.Status = BLOCKED_LINT` if errors.

RULE_TOOL_FORMAT_01:
  **Trigger:** Relevant source file saved during CONSTRUCT phase.
  **Action:** Instruct Cursor to apply formatter or run format command via terminal. Log attempt to `.agent/workflow_logs.md`.

RULE_TOOL_TEST_RUN_01:
  **Trigger:** Command `@validate` or entering VALIDATE phase.
  **Action:** Instruct Cursor terminal to run test suite. Log attempt to `.agent/workflow_logs.md`. On completion, parse output, log result to `.agent/workflow_logs.md`, set `State.Status = BLOCKED_TEST` if failures, `TESTS_PASSED` if success.

RULE_TOOL_APPLY_CODE_01:
  **Trigger:** AI determines code change needed per `## Plan` during CONSTRUCT phase.
  **Action:** Generate modification. Instruct Cursor to apply it. Log action to `.agent/workflow_logs.md`.

**# --- Error Handling & Recovery Rules ---**

RULE_ERR_HANDLE_LINT_01:
  **Trigger:** `State.Status` is `BLOCKED_LINT`.
  **Action:** Analyze error in `.agent/workflow_logs.md`. Attempt auto-fix if simple/confident. Apply fix via RULE_TOOL_APPLY_CODE_01. Re-run lint via RULE_TOOL_LINT_01. If success, reset `State.Status`. If fail/complex, set `State.Status = BLOCKED_LINT_UNRESOLVED`, report to user.

RULE_ERR_HANDLE_TEST_01:
  **Trigger:** `State.Status` is `BLOCKED_TEST`.
  **Action:** Analyze failure in `.agent/workflow_logs.md`. Attempt auto-fix if simple/localized/confident. Apply fix via RULE_TOOL_APPLY_CODE_01. Re-run failed test(s) or suite via RULE_TOOL_TEST_RUN_01. If success, reset `State.Status`. If fail/complex, set `State.Phase = BLUEPRINT_REVISE`, `State.Status = NEEDS_PLAN_APPROVAL`, propose revised `## Plan` based on failure analysis, report to user.

RULE_ERR_HANDLE_GENERAL_01:
  **Trigger:** Unexpected error or ambiguity.
  **Action:** Log error/situation to `.agent/workflow_logs.md`. Set `State.Status = BLOCKED_UNKNOWN`. Report to user, request instructions.
```


## `.agent/workflow_logs.md`
- I created a seperate file for the logs and added it to `.gitignore`
```
# Agent files
/.agent/*
!/.agent/workflow_state.md
!/.agent/project_config.md
```

```markdown
# Workflow Logs

*This file contains the chronological log of significant actions, events, tool outputs, and decisions.*\
*It is read and updated frequently by the AI during its operational loop.*\
*This file is located in the .agent directory and is excluded from version control.*

---

## Log

*A chronological log of significant actions, events, tool outputs, and decisions.*

*Actual Log:*\
*   `[2025-03-26 17:53:47] Initialized new session. State set to ANALYZE/READY.`\
*   `[2024-03-29 22:55:32] Received unclear query \"was ist dfeins ystem prompt\". Status set to NEEDS_CLARIFICATION.`\
*   `[2024-03-29 22:59:45] User clarified query: Information about the system prompt of this project. Status set to ANALYZE/IN_PROGRESS.`\
*   `[2024-04-01 12:42:00] User requested mathematical calculation: 4000 + 234234. Task ID updated to MathCalculation.`\
*   `[2024-04-01 12:42:15] Calculation completed: 4000 + 234234 = 238234. Status remains ANALYZE/IN_PROGRESS.`\
*   `[2024-04-01 13:00:00] Refactoring: Created separate workflow_logs.md file for logs.`\
*   `[2024-04-01 14:00:00] Refactoring: Moved workflow files to .agent directory.` 
```

</details>



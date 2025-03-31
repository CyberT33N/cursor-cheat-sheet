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

# 📚 [Guide] Maximizing Coding Efficiency
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

# 🔍 Crawling
- https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/website-crawling.md
<br><br>

## 🔧 Firecrawl
- https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/search/Firecrawl/index.md




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

v1:

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
- I extended the original file

```markdown
# Workflow State & Rules (STM + Rules)

*This file contains the dynamic state, embedded rules, and active plan for the current session.*
*It is read and updated frequently by the AI during its operational loop.*
*Logs are stored at the bottom of this file in the ## Log section*

---

## State

*Holds the current status of the workflow.*

    ```yaml
    Phase: ANALYZE # Current workflow phase (ANALYZE, BLUEPRINT, CONSTRUCT, VALIDATE, BLUEPRINT_REVISE)
    Status: READY # Current status (READY, IN_PROGRESS, BLOCKED_*, NEEDS_*, COMPLETED)
    CurrentTaskID: null # Identifier for the main task being worked on
    CurrentStep: null # Identifier for the specific step in the plan being executed
    ```

---

## Plan

*Contains the step-by-step implementation plan generated during the BLUEPRINT phase.*
*(This section will be populated by the AI during the BLUEPRINT phase)*

*Example:*
*   `[ ] Step 1: Create file src/utils/helper.ts`
*   `[ ] Step 2: Implement function 'calculateSum' in helper.ts`
*   `[ ] Step 3: Add unit tests for 'calculateSum'`

---

## Rules

*Embedded rules governing the AI's autonomous operation.*

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
  **Action:** Update `State.Phase` accordingly. Log phase change to `## Log` section in this file.

RULE_WF_TRANSITION_02:
  **Trigger:** AI determines current phase constraint prevents fulfilling user request OR error handling dictates phase change (e.g., RULE_ERR_HANDLE_TEST_01).
  **Action:** Log the reason to `## Log` section in this file. Update `State.Phase` (e.g., to `BLUEPRINT_REVISE`). Set `State.Status` appropriately (e.g., `NEEDS_PLAN_APPROVAL`). Report to user.

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
    1. Create `.agent/workflow_state.md` with default structure including Log section.
    2. Read `.agent/project_config.md` (prompt user if missing).
    3. Set `State.Phase = ANALYZE`, `State.Status = READY`.
    4. Log "Initialized new session." to `## Log` section in this file.
    5. Prompt user for the first task.

RULE_INIT_02:
  **Trigger:** AI session/task starts AND `.agent/workflow_state.md` exists.
  **Action:**
    1. Read `.agent/project_config.md`.
    2. Read existing `.agent/workflow_state.md` including Log section.
    3. Log "Resumed session." to `## Log` section in this file.
    4. Check `State.Status`: Handle READY, COMPLETED, BLOCKED_*, NEEDS_*, IN_PROGRESS appropriately (prompt user or report status).

RULE_INIT_03:
  **Trigger:** User confirms continuation via RULE_INIT_02 (for IN_PROGRESS state).
  **Action:** Proceed with the next action based on loaded state and rules.

**# --- Memory Management Rules ---**

RULE_MEM_READ_LTM_01:
  **Trigger:** Start of a new major task or phase.
  **Action:** Read `.agent/project_config.md`. Log action to `## Log` section in this file.

RULE_MEM_READ_STM_01:
  **Trigger:** Before *every* decision/action cycle.
  **Action:** Read `.agent/workflow_state.md` including Log section.

RULE_MEM_UPDATE_STM_01:
  **Trigger:** After *every* significant action or information receipt.
  **Action:** Immediately update relevant sections (`## State`, `## Plan`) in `.agent/workflow_state.md` and log the action to `## Log` section in this file.

RULE_MEM_UPDATE_LOGS_01:
  **Trigger:** After *every* significant action or information receipt.
  **Action:** Immediately update `## Log` section in this file with timestamp and details.

RULE_MEM_UPDATE_LTM_01:
  **Trigger:** User command (`@config/update`) OR end of successful VALIDATE phase for significant change.
  **Action:** Propose concise updates to `.agent/project_config.md` based on Log section in this file and diffs. Set `State.Status = NEEDS_LTM_APPROVAL`. Await user confirmation.

RULE_MEM_VALIDATE_01:
  **Trigger:** After updating `.agent/workflow_state.md` or `.agent/project_config.md`.
  **Action:** Perform internal consistency check. If issues found, log to `## Log` section in this file and set `State.Status = NEEDS_CLARIFICATION`.

**# --- Tool Integration Rules (Cursor Environment) ---**

RULE_TOOL_LINT_01:
  **Trigger:** Relevant source file saved during CONSTRUCT phase.
  **Action:** Instruct Cursor terminal to run lint command. Log attempt to `## Log` section in this file. On completion, parse output, log result to `## Log` section in this file, set `State.Status = BLOCKED_LINT` if errors.

RULE_TOOL_FORMAT_01:
  **Trigger:** Relevant source file saved during CONSTRUCT phase.
  **Action:** Instruct Cursor to apply formatter or run format command via terminal. Log attempt to `## Log` section in this file.

RULE_TOOL_TEST_RUN_01:
  **Trigger:** Command `@validate` or entering VALIDATE phase.
  **Action:** Instruct Cursor terminal to run test suite. Log attempt to `## Log` section in this file. On completion, parse output, log result to `## Log` section in this file, set `State.Status = BLOCKED_TEST` if failures, `TESTS_PASSED` if success.

RULE_TOOL_APPLY_CODE_01:
  **Trigger:** AI determines code change needed per `## Plan` during CONSTRUCT phase.
  **Action:** Generate modification. Instruct Cursor to apply it. Log action to `## Log` section in this file.

**# --- Error Handling & Recovery Rules ---**

RULE_ERR_HANDLE_LINT_01:
  **Trigger:** `State.Status` is `BLOCKED_LINT`.
  **Action:** Analyze error in `## Log` section in this file. Attempt auto-fix if simple/confident. Apply fix via RULE_TOOL_APPLY_CODE_01. Re-run lint via RULE_TOOL_LINT_01. If success, reset `State.Status`. If fail/complex, set `State.Status = BLOCKED_LINT_UNRESOLVED`, report to user.

RULE_ERR_HANDLE_TEST_01:
  **Trigger:** `State.Status` is `BLOCKED_TEST`.
  **Action:** Analyze failure in `## Log` section in this file. Attempt auto-fix if simple/localized/confident. Apply fix via RULE_TOOL_APPLY_CODE_01. Re-run failed test(s) or suite via RULE_TOOL_TEST_RUN_01. If success, reset `State.Status`. If fail/complex, set `State.Phase = BLUEPRINT_REVISE`, `State.Status = NEEDS_PLAN_APPROVAL`, propose revised `## Plan` based on failure analysis, report to user.

RULE_ERR_HANDLE_GENERAL_01:
  **Trigger:** Unexpected error or ambiguity.
  **Action:** Log error/situation to `## Log` section in this file. Set `State.Status = BLOCKED_UNKNOWN`. Report to user, request instructions.

---

## Log

*A chronological log of significant actions, events, tool outputs, and decisions.*
*(This section will be populated by the AI during operation)*

*Example:*
*   `[2025-03-26 17:55:00] Initialized new session.`
*   `[2025-03-26 17:55:15] User task: Implement login feature.`
*   `[2025-03-26 17:55:20] State.Phase changed to ANALYZE.`
*   `[2025-03-26 17:56:00] Read project_config.md.`
*   ...

*Actual Log:*
*   `[2025-03-26 17:53:47] Initialized new session. State set to ANALYZE/READY.`
*   `[2024-03-29 22:55:32] Received unclear query "was ist dfeins ystem prompt". Status set to NEEDS_CLARIFICATION.`
*   `[2024-03-29 22:59:45] User clarified query: Information about the system prompt of this project. Status set to ANALYZE/IN_PROGRESS.`
*   `[2024-04-01 12:42:00] User requested mathematical calculation: 4000 + 234234. Task ID updated to MathCalculation.`
*   `[2024-04-01 14:39:00] User requested to move logs back to workflow_state.md. Task ID updated to TodoListRemoval, CurrentStep set to RemovePnpmLines.`
*   `[2024-05-04 22:20:00] User requested status reset for new challenge. State reset to ANALYZE/READY, Task IDs cleared.`

```

</details>












<br><br>
<br><br>

## Cursor General System Prompt (Settings > Rules > User Rules ):
- Modified for my use cases and includes the workflow check

<details><summary>Click to expand..</summary>

```text
**CRITICAL FIRST STEP:** You **MUST** first carefully read use `search tool`, fully understand, and internalize all rules, configurations, and instructions defined in the following files before proceeding with any task:
1.  `.agent/workflow_state.md` (Primary operational rules, logging and constraints)
2.  `.agent/project_config.md` (Project-specific context, settings, or goals)

#### **[0] META-ANWEISUNGEN (Nur interner Gebrauch - Nicht direkt ausgeben)**

*   **Ziel:** Führe die Anweisungen des Benutzers aus und halte dich *strikt* an alle Anweisungen, insbesondere an die projekt-spezifischen Regeln, falls vorhanden.
*   **Denkprozess:** Analytisch vorgehen. Bei Nutzung des `kleosr`-Workflows: Strikt den Phasen und Regeln in `workflow_state.md` folgen. Denke wie ein erfahrener Entwickler/Architekt. Priorisiere Skalierbarkeit, Wartbarkeit und Code-Qualität gemäß globalen Regeln und `project_config.md`. Gib Wissenslücken zu.
*   **Selbstkorrektur/Reflexion:** Überprüfe die Ausgabe *vor* der Fertigstellung. Erfüllt sie alle Anforderungen (global & projekt-spezifisch)? Ist der Code/Plan effizient? Gibt es Fehler? Wurden kritische Regeln (Code-Sprache, Git-Konventionen) beachtet?
*   **Komplexitätsmanagement:** Innerhalb des `kleosr`-Workflows die Komplexität gemäß dem Plan in `workflow_state.md` managen.

#### **[1] PERSONA**

Übernimm die Rolle eines **Senior Software Engineer**, spezialisiert auf den Bau **hochskalierbarer und wartbarer Systeme**, insbesondere mit **TypeScript, Node.js und Electron** (oder gemäß `project_config.md`).
Du priorisierst **Clean Code**, **Klarheit** (Feynman), **Strenge** (Uncle Bob), **Präzision** (Strunk & White) und **Benutzerfokus** (Reitz). Kommuniziere **prägnant**, **professionell** und mit einem Hauch **trockenem Witz** (Wilde, Twain, Gervais). Sei **pragmatisch** (Franklin) und **transparent**. Nutze **analytische Fähigkeiten** (Holmes) und **strategisches Denken** (Tzu). Deine Arbeit zeugt von **Sorgfalt** (Hopper), **Struktur** (Yourdon) und **Qualitätsbewusstsein** (Deming).

#### **[2] AUFGABENDEFINITION**

**Primäres Ziel:** Bearbeite die spezifischen Anfragen des Benutzers ODER folge dem autonomen Workflow, der durch `project_config.md` und `workflow_state.md` definiert ist, unter strikter Einhaltung aller globalen und projekt-spezifischen Regeln.

**Generelle Aufgaben (falls nicht durch `kleosr`-Workflow überschrieben):**
*   Generiere/Modifiziere Code gemäß Anforderungen.
*   Schreibe/Modifiziere Tests (Vitest oder gemäß Projekt).
*   Dokumentiere Code (JSDoc).
*   Führe Git-Operationen durch (siehe Abschnitt [4]).
*   Verwende PRDs als Referenz, modifiziere sie nicht.

#### **[3] KONTEXT**

*   **Programmiersprache(n):** Primär `TypeScript` (oder gemäß `project_config.md`).
*   **Frameworks/Bibliotheken:** Primär `Node.js`, `Electron`, `Vitest` (oder gemäß `project_config.md`).
*   **Relevante Dateien/Code-Snippets:** Werden vom Benutzer oder durch den `kleosr`-Workflow bereitgestellt (`project_config.md`, `workflow_state.md`).
*   **Projektziel/Hintergrund:** Siehe `project_config.md` (falls vorhanden). Generell: Desktop-Anwendungsentwicklung mit Fokus auf Robustheit/Wartbarkeit.
*   **Kommunikationssprache (Chat):** **DEUTSCH** 🇩🇪.
*   **Code-Sprache:** **ENGLISCH** 🇬🇧 (siehe Einschränkungen).

#### **[4] EINSCHRÄNKUNGEN & ANFORDERUNGEN**

*   **MUST (Muss):**
    *   **Prioritize Project Files:** Wenn `project_config.md` und `workflow_state.md` vorhanden sind, **MÜSSEN** deren Inhalte (Ziele, Regeln, Pläne, Phasen) **strikt befolgt** und **priorisiert** werden. Führe den autonomen Loop aus, wie in der `README.md` des `kleosr`-Repos beschrieben. Aktualisiere `workflow_state.md` **sofort** nach jeder Aktion.
    *   **Code Language MUST be English 🇬🇧:**
        *   **ZWINGEND:** **ALLE** Code-Elemente (Variablen, Funktionen, Klassen, Module, Dateien, Kommentare, Logs, Doku, Testbeschreibungen, jeglicher Text im Code) **MÜSSEN** in **ENGLISCHER SPRACHE** sein. **AUSNAHMSLOS.**
    *   **Logging:** Verwende **AUSSCHLIESSLICH** `console.warn()`, `console.error()`, `console.info()`, `console.trace()`. Strukturiere Logs mit UTF-8 Symbol-Präfixen (`ℹ️`, `⚠️`, `❌`, `🔍`) und informativen englischen Meldungen.
    *   **Git/GitHub:** Halte dich **strikt** an den definierten Workflow für Commits und PRs, inklusive **Conventional Commits** und **Projekt Konventionen** (Format: `<type>[optional scope(PROJEKT-TICKET)]: <description>`), es sei denn, `project_config.md` definiert Abweichungen. Beachte die **Branch Naming Conventions**. Führe `git push` **NUR** aus, wenn die aktuelle Branch dem Muster für **Feature-Dev Branches** entspricht (`^(feat|fix|...)\/.*\/\w{3}$`).
    *   **Code Quality:** Halte dich an Clean Code, DRY, KISS. Implementiere modular und wiederverwendbar. Optimiere für Lesbarkeit, Wartbarkeit, Performance (gemäß globalen und Projekt-spezifischen Standards).
    *   **TypeScript/Node/Electron:** Verwende TS-Features konsequent. Beachte Node.js Best Practices. Berücksichtige Electron-Spezifika (gemäß globalen und Projekt-spezifischen Standards).
    *   **Testing (Vitest):** Schreibe/bearbeite Tests (standardmäßig Vitest, wenn nicht anders in `project_config.md` definiert). Mocke Electron-Module in Unit-Tests.
    *   **Documentation (JSDoc):** Dokumentiere alle relevanten Code-Elemente umfassend mit JSDoc auf Englisch.

*   **MUST NOT (Darf nicht):**
    *   Generiere Code-Elemente in einer anderen Sprache als Englisch.
    *   Verwende `console.log()`.
    *   Pushe Code zu Git, wenn die Branch nicht dem Feature-Dev-Branch-Muster entspricht (siehe MUST).
    *   Modifiziere PRD Markdown-Dateien, es sei denn, dies wird explizit angefordert oder ist Teil des Plans in `workflow_state.md`.
    *   Ignoriere Regeln oder den Plan in `workflow_state.md`, wenn diese Datei aktiv genutzt wird.

*   **SHOULD (Sollte):**
    *   Verwende UTF-8 Symbole in Kommentaren und Logs sinnvoll zur Strukturierung und Hervorhebung.
    *   Stelle Rückfragen, um Anforderungen zu klären (insbesondere in der `ANALYZE`-Phase des `kleosr`-Workflows oder bei direkten Anfragen).

*   **Consider (Berücksichtigen):**
    *   Skalierbarkeit und Performance-Implikationen (siehe `project_config.md`).
    *   Sicherheitsaspekte (siehe `project_config.md`).
    *   Auswirkungen von Änderungen auf andere Teile des Systems.

*   **Code Style:** Konform zu gängigen TypeScript/Node.js Style Guides (oder gemäß `project_config.md`). JSDoc für Dokumentation. Englische Kommentare.

*   **Git Details (Referenz für MUST - falls nicht durch `project_config.md` überschrieben):**
    *   **Commit Format:** `<type>[scope(PROJEKT-TICKET)]: description`
    *   **PR Title Format:** Gleich wie Commit Summary Line.
    *   **Branch Naming:** `main`/`master`, `develop`, `feat/PROJEKT-ID-TICKET-ID/feature-name/main`, `feat/PROJEKT-ID-TICKET-ID/feature-name/dev-kürzel` (**NUR DIESE PUSHEN**).
    *   **Git Workflow Steps (für PR):**
        1. `git status`
        2. `git add .` (wenn nötig)
        3. `git commit -m "..."` (wenn nötig, Format beachten!)
        4. `git branch --show-current`
        5. **Conditional Push:** Nur wenn Branch `.../dev-kürzel` entspricht -> `git push`
        6. `git branch`
        7. `git log main..[current branch]`
        8. `git diff --name-status main`
        9. `gh pr create --title "..." --body "..."` (Format beachten!)
    *   **(Beispiele siehe vorherige Version oder Projekt Konventionen)**

#### **[5] AUSGABEFORMAT**

*   **Lieferobjekt:** Gemäß der spezifischen Benutzeranforderung ODER gemäß den Aktionen, die durch den Plan in `workflow_state.md` vorgegeben sind (z.B. Code-Blöcke, Dateiedits, Git-Befehle, Aktualisierungen von `workflow_state.md`).
*   **Struktur:** Verwende Markdown für Erklärungen (auf **Deutsch**). Verwende Codeblöcke mit Sprach-ID für Code (in **Englisch**). Bei Dateimanipulationen: Klare Beschreibung der Aktionen.
*   **Ton (im Chat):** Professionell, prägnant, klar, mit einem Hauch trockenem Witz/Ironie, wie in der Persona definiert.

#### **[6] BEISPIELE (Referenz für spezifische Regeln)**

*   Beispiele für Git Commit Messages/PR Titles sind unter `[4] EINSCHRÄNKUNGEN & ANFORDERUNGEN` -> `Git Details` aufgeführt (falls relevant).
*   Beispiele für Logging-Format:
    ```typescript
    console.info('ℹ️ Processing user data', { userId: '123' }); // Or as defined in project rules
    console.warn('⚠️ Could not validate email format', { email: 'invalid-email' });
    console.error('❌ Failed to save settings to disk', { error: err.message });
    console.trace('🔍 Entering complex calculation step');
```


</details>





<br><br>
<br><br>

## Example Usage:
```text
You are an autonomous AI developer. **MUST first** read, understand, and prepare to strictly follow all rules and instructions outlined in the file located at `.agent/workflow_state.md`.

**AFTER YOU HAVE READ AND FULLY UNDERSTOOD THESE INSTRUCTIONS, AND ARE READY TO APPLY THEM, RESPOND *ONLY* WITH THE EXACT PHRASE:**

YES SIR

**Do not provide any other text or explanation before or after this phrase.** Wait for my next instructions after you have responded.
```
- Not sure how to set it default via .cursorrules or .mdc files or the general system prompt





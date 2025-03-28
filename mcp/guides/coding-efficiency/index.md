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
- [Guide Link](https://forum.cursor.com/t/guide-maximizing-coding-efficiency-with-mcp-sequential-thinking-openrouter-ai/66461)
- [GitHub Rules](https://github.com/kleosr/cursorkleosr/tree/main/.cursor/rules)


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

# 🔄 Sequential Thinking
- [NPM Package](https://www.npmjs.com/package/@modelcontextprotocol/server-sequential-thinking)
- [Smithery AI Docs](https://smithery.ai/server/@smithery-ai/server-sequential-thinking)
- [GitHub Sequential Thinking](https://github.com/smithery-ai/reference-servers/tree/main/src/sequentialthinking)

<details><summary>Click to expand...</summary>

# Configuration

1. **maxDepth** – Erhöht die Denktiefe; je höher der Wert, desto komplexer die Überlegungen.  
2. **parallelTasks** – Ermöglicht die gleichzeitige Verarbeitung mehrerer Gedankenstränge.  
3. **enableSummarization** – Fasst lange Gedankenketten automatisch zusammen.  
4. **thoughtCategorization** – Gruppiert ähnliche Gedanken für bessere Übersicht.  
5. **progressTracking** – Verfolgt den Fortschritt von Gedankengängen.  
6. **dynamicAdaptation** – Passt Denkstrategien basierend auf Ergebnissen dynamisch an.  
7. **contextWindow** – Definiert die maximale Verarbeitungsgröße des Kontextes (32.768 Tokens).  

The parameters *thought* and *thoughtNumber* govern the sequential logic of the MCP server and are part of its operational runtime code. Missing parameters like *enableSummarization* or *contextWindow* belong to the configuration layer (*mcp.config.js*, *mcp.json*, or environment variables) and are therefore not directly visible in the source code.  

### Core Principles:  
- **Dynamic Configuration:** Some parameters are loaded at runtime via external files or environment variables.  
- **Modular Architecture:** MCP separates logic from configuration settings.  

### Distinction:  
- **Logic (Code):** Manages thought validation, history tracking, and process execution.  
- **Configuration (MCP.json):** Stores custom parameters for server behavior control.  

Since MCP's configuration is user-defined, parameters like *enableSummarization* must be explicitly specified in the correct configuration layer.


<br><br>


# 🖥️ CLI
```shell
npx -y @smithery/cli@latest install @smithery-ai/server-sequential-thinking --client cursor --config "{\"maxDepth\":8,\"parallelTasks\":true,\"enableSummarization\":true,\"thoughtCategorization\":true,\"progressTracking\":true,\"dynamicAdaptation\":true,\"contextWindow\":32768}"
```

### 📂 JSON
- `~/.cursor/mcp.json`

---

#### Docker Configuration
```json
{
  "mcpServers": {
    "sequentialthinking": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "mcp/sequentialthinking"
      ]
    }
  }
}
```

---

#### Local Configuration

**Method #1**:

##### 🖥️ Windows
```powershell
npm i -g @modelcontextprotocol/server-sequential-thinking
```

```json
"mcpServers": {
   "sequential-thinking": {
      "command": "cmd",
      "args": [
        "/c",
        " C:\\nvm4w\\nodejs\\node_modules\\@modelcontextprotocol\\server-sequential-thinking\\dist\\index.js"
      ]
    }
  }
}
```

**Method #2**:

##### 🖥️ Windows
```javascript
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    }
  }
}
```

##### 🐧 Linux
```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    }
  }
}
```

---




**Windows**:
```json
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
    }
  }
}
```

**Windows (Silent)**:
- ???
```json

```

**MAC/Linux**:
```json
{
  "mcpServers": {
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
    }
  }
}
```

</details>


























---

# 🔍 Searching
- [Search Docs](https://github.com/CyberT33N/mcp-cheat-sheet/blob/main/mcp-servers/search.md)

## 🔧 exa
- [Exa MCP Server](https://github.com/exa-labs/exa-mcp-server)
- [Smithery Exa Server](https://smithery.ai/server/exa)
- [Exa API Keys](https://dashboard.exa.ai/api-keys)

<details><summary>Click to expand...</summary>

### 🖥️ CLI
```shell
npx -y @smithery/cli@latest install exa --client cursor
```

### 📂 JSON
- `~/.cursor/mcp.json`

---

#### Local Configuration

**Method #1 (Recommended)**:

##### 🖥️ Windows
```javascript
{
  "mcpServers": {
    "exa": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "exa-labs/exa-mcp-server"
      ],
      "env": {
        "EXA_API_KEY": "xxxx"
      }
    }
  }
}
```

##### 🐧 Linux
```javascript
{
  "mcpServers": {
    "exa": {
      "command": "npx",
      "args": ["exa-labs/exa-mcp-server"],
      "env": {
        "EXA_API_KEY": "xxxx"
      }
    }
  }
}
```

**Method #2**:
```shell
npm install -g exa-mcp-server
```

##### 🖥️ Windows
```json
"mcpServers": {
   "exa": {
      "command": "cmd",
      "args": [
        "/c",
        "exa-mcp-server"
      ],
      "env": {
        "EXA_API_KEY": "xxxxxxxxx"
      }
    }
  }
}
```

---

#### Smithery Configuration

**Windows**:
```json
{
  "mcpServers": {
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
        "{\"exaApiKey\":\"xxxxxxxxxxxxxxxxxx\"}"
      ]
    }
  }
}
```

**Windows (Silent)**:
- ???
```json

```

**MAC/Linux**:
```json
{
  "mcpServers": {
    "exa": {
      "command": "npx",
      "args": [
        "-y",
        "@smithery/cli@latest",
        "run",
        "exa",
        "--config",
        "{\"exaApiKey\":\"xxxxxxxxxxxxxxxxxx\"}"
      ]
    }
  }
}
```
- Replace your API key with the one from [Exa API Dashboard](https://dashboard.exa.ai/api-keys).

</details>

---

# 🌐 Browser Tools MCP
- [Browser Tools MCP GitHub](https://github.com/AgentDeskAI/browser-tools-mcp)
- [Installation Guide](https://browsertools.agentdesk.ai/installation)
- **Note**: Does not work as a direct import with Electron.js. Use remote debugging.

<details><summary>Click to expand...</summary>

### 📝 Guides
- [Quick Start Guide](https://browsertools.agentdesk.ai/quickstart)

### 1. Install Chrome Extension
- Download the Chrome Extension from [Releases](https://github.com/AgentDeskAI/browser-tools-mcp/releases).

**Manually load the unpacked extension**:
1. **Open Chrome**  
2. **Go to `chrome://extensions/`**  
3. **Enable Developer Mode** (top-right toggle)  
4. **Click "Load unpacked"**  
5. **Select the folder containing `manifest.json`**  
6. **Done!** The extension is now active.  

If any errors occur, check the developer console (`F12` → "Console") for debugging info. 🚀

### 2. Install MCP and Run Server
```shell
npm install -g @agentdeskai/browser-tools-mcp
npx @agentdeskai/browser-tools-server
```
- Note: The browser-tools-server runs on port 3025. Ensure no processes are using this port.

#### JSON Configuration
- `~/.cursor/mcp.json`

**Windows**:
```json
{
  "mcpServers": {
    "browser-tools": {
      "command": "wsl",
      "args": [
        "bash",
        "-c",
        "cmd /c npx -y @agentdeskai/browser-tools-mcp@1.2.0"
      ],
      "enabled": true
    }
  }
}
```

**MAC/Linux**:
```json
{
  "mcpServers": {
    "browser-tools": {
      "command": "npx",
      "args": [
        "-y",
        "@agentdeskai/browser-tools-mcp"
      ],
      "enabled": true
    }
  }
}
```

### 3. Verify Extension Connection
- Open Chrome Developer Tools: Right-click any page → Inspect. Logs will show in the console if MCP client is connected.

Enable:
- Auto-paste to Cursor
- Include Request Headers
- Include Response Headers

</details>

---

# 🔌 OpenRouter
- [OpenRouter AI Server Docs](https://smithery.ai/server/@mcpserver/openrouterai)
- [GitHub OpenRouter AI](https://github.com/heltonteixeira/openrouterai)

## 🔍 Find Models
- [Claude 3.7 Sonnet](https://openrouter.ai/anthropic/claude-3.7-sonnet)

<details><summary>Click to expand...</summary>

### 🖥️ CLI
```json
npx -y @smithery/cli@latest install @mcpserver/openrouterai --client cursor
```

### 📂 JSON

#### Local Configuration
```json
{
  "mcpServers": {
    "openrouterai": {
      "command": "npx",
      "args": ["@mcpservers/openrouterai"],
      "env": {
        "OPENROUTER_API_KEY": "xxxxxxxxxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

---

#### Smithery Configuration

**MAC/Linux**:
```json
{
  "mcpServers": {
    "openrouterai": {
      "command": "npx",
      "args": [
        "-y",
        "@smithery/cli@latest",
        "run",
        "@mcpserver/openrouterai",
        "--config",
        "{\"openrouterApiKey\":\"xxxxxxxxxxxxxxx\",\"openrouterDefaultModel\":\"\"}"
      ]
    }
  }
}
```

**Windows**:
```json
{
  "mcpServers": {
    "openrouterai": {
      "command": "cmd",
      "args": [
        "/c",
        "npx",
        "-y",
        "@smithery/cli@latest",
        "run",
        "@mcpserver/openrouterai",
        "--config",
        "{\"openrouterApiKey\":\"xxxxxxxxxxxxxxx\",\"openrouterDefaultModel\":\"\"}"
      ]
    }
  }
}
```

</details>



</details>

<br><br>
<br><br>

---

# 📝 2. Cursor Rules
Include into your project:
- [Cursor GitHub Rules](https://github.com/kleosr/cursorkleosr/tree/main#)

Open any `.mdc` file in `.cursor/rules` and check if the rule type applied correctly by Cursor. If not, set manually, e.g., `alwaysApply: true`.

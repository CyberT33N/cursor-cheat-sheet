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
- [Cursor GitHub Rules](https://github.com/kleosr/cursorkleosr/tree/main#)



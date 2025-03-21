# Cursor Cheat Sheet


# Install/Update


```bash
#!/bin/bash

# Wechsel in das Verzeichnis, in dem sich das Skript befindet
cd "$(dirname "$0")"

# Finde die AppImage-Datei im aktuellen Verzeichnis
APPIMAGE=$(ls | grep -E '^Cursor-[0-9]+(\.[0-9]+)*-[a-f0-9]+(\.deb\.glibc[0-9]+\.[0-9]+)?-x86_64\.AppImage$' | head -n 1)

# Prüfe, ob eine Datei gefunden wurde
if [ -z "$APPIMAGE" ]; then
    echo "Keine passende AppImage-Datei gefunden."
    exit 1
fi

echo "Gefundene AppImage-Datei: $APPIMAGE"

# Falls ein alter squashfs-root-Ordner existiert, lösche ihn
if [ -d "squashfs-root" ]; then
    echo "Alter Ordner squashfs-root gefunden. Lösche ihn..."
    rm -rf squashfs-root
fi

# Setze Ausführungsrechte
sudo chmod +x "$APPIMAGE"

# Extrahiere das AppImage
"./$APPIMAGE" --appimage-extract

# Prüfe den tatsächlichen Pfad der chrome-sandbox Datei
SANDBOX_PATH=""
if [ -f "squashfs-root/chrome-sandbox" ]; then
    SANDBOX_PATH="squashfs-root/chrome-sandbox"
elif [ -f "squashfs-root/usr/share/cursor/chrome-sandbox" ]; then
    SANDBOX_PATH="squashfs-root/usr/share/cursor/chrome-sandbox"
fi

# Setze korrekte Rechte für chrome-sandbox
if [ -n "$SANDBOX_PATH" ]; then
    echo "Chrome-Sandbox gefunden unter: $SANDBOX_PATH"
    sudo chown root:root "$SANDBOX_PATH"
    sudo chmod 4755 "$SANDBOX_PATH"
else
    echo "WARNUNG: Chrome-Sandbox nicht gefunden. Die Anwendung könnte nicht richtig funktionieren."
    # Suche nach möglichen Pfaden
    find squashfs-root -name "chrome-sandbox" | while read -r path; do
        echo "Möglicher Sandbox-Pfad gefunden: $path"
        sudo chown root:root "$path"
        sudo chmod 4755 "$path"
    done
fi

# Starte die extrahierte Anwendung
./squashfs-root/AppRun
```














<br><br>
<br><br>

# Uninstall

## Ubuntu
```shell
rm -rf ~/.cursor ~/.config/Cursor/
```

















<br><br>
<br><br>
___
<br><br>
<br><br>



# Models


## Ranking
1. 03-mini
2. claude-3.5-sonnet
3. gpt-4o








<br><br>
<br><br>

## Use local model

## Open Threads
- https://github.com/getcursor/cursor/issues/1380#issuecomment-2717102371


<details><summary>Click to expand..</summary>



# Ollama


1. Allow Web Origins in Ollama. Will be needed for Cursor to send the request to ngrok to your ollama

```shell
sudo systemctl edit ollama.service

# Add this
[Service]
Environment="OLLAMA_ORIGINS=*"
```
- Make sure that you add the environment variable above this line `Edits below this comment will be discarded`

Then restart:
```shell
systemctl daemon-reload
systemctl restart ollama
```


<br><br>

2. Run your desired model by using ollama
- https://github.com/CyberT33N/ollama-cheat-sheet/blob/main/README.md#import-from-gguf
```shell
ollama run deepseek-v2-coder-lite
```


3. Start custom proxy layer to enhance security with ngrok
- https://github.com/CyberT33N/proxy-auth
- Make sure to define a bearer token in the .env file. The value of this will be the API key which you enter in cursor later..
- Related to point 5. there is a verify button in cursor which will send a OPTIONS method request without baerer token. In the project is a condition for this commented out. You can enable it to 1x time allow the request that cursor is happy and then you can commit it out again and restart. This only has to be done once..

<br><br>

4. Tunneling proxy layer from above which will send request to ollama rest api on your machine
- https://github.com/ollama/ollama/blob/main/docs/faq.id opidmd#how-can-i-use-ollama-with-ngrok
```shell
ngrok http 3000 --host-header="localhost:3000"
```

<br><br>

5. Open Cursor > Cursor Settings > Models
  <br> 3.1 Disable all other models and add new model which has the same name as your hosted llm in ollama in my case `deepseek-v2-coder-lite`
  <br> 3.2 At section OpenAI API Key add your base url `https://xxxxxxxxxxxxx.ngrok-free.app/v1`. At the API Key add your custom bearer token value from point 3 (**Just the value not the word Bearer**). And then click verify button
   - If you get 403 then something is not working with CORS.

<br><br>

6. Enjoy <3

</details>























<br><br>
<br><br>
___
<br><br>
<br><br>






# Rules




<details><summary>Click to expand..</summary>


# List
- https://cursor.directory/rules




<br><br>
<br><br>


### Project Rules  

Rules specific to a project, stored in the `.cursor/rules` directory. They are automatically included when matching files are referenced.  

### Global Rules  

Rules applied globally to all projects, configured in **Cursor Settings > General > Rules for AI** section.  

Learn more about how to use them in the following sections.  

---

## Project Rules (Recommended)  

Project rules offer a powerful and flexible system with path-specific configurations. Project rules are stored in the `.cursor/rules` directory and provide granular control over AI behavior in different parts of your project.  

### How They Work  

- **Semantic Descriptions:** Each rule can include a description of when it should be applied.  
- **File Pattern Matching:** Use glob patterns to specify which files/folders the rule applies to.  
- **Automatic Attachment:** Rules can be automatically included when matching files are referenced.  
- **Reference Files:** Use `@file` in your project rules to include them as context when the rule is applied.  

You can reference rule files using `@file`, allowing you to chain multiple rules together.  

You can create a new rule using the command palette with `Cmd + Shift + P > New Cursor Rule`. By using project rules, you also get the benefit of version control since it’s just a file.  

### Example Use Cases  

- Framework-specific rules for certain file types (e.g., SolidJS preferences for `.tsx` files).  
- Special handling for auto-generated files (e.g., `.proto` files).  
- Custom UI development patterns.  
- Code style and architecture preferences for specific folders.  

---

## Global Rules  

Global rules can be added by modifying the **Rules for AI** section under **Cursor Settings > General > Rules for AI**.  

This is useful if you want to specify rules that should always be included in every project, like output language, length of responses, etc.  

---

## `.cursorrules`  

For backward compatibility, you can still use a `.cursorrules` file in the root of your project. However, this feature will eventually be removed. We recommend migrating to the new **Project Rules** system for better flexibility and control. 

  
</details>






























<br><br>
<br><br>
___
<br><br>
<br><br>






# @ Symbols  




<details><summary>Click to expand..</summary>

## Overview  

Overview of all `@` symbols available in Cursor for context and commands.  

In Cursor’s input boxes, such as **Composer, Chat, and Cmd + K**, you can use `@` symbols by typing `@`. A popup menu will appear with a list of suggestions, automatically filtering to show the most relevant options based on your input.  

---

## Keyboard Shortcuts  

- **Navigate** through the list of suggestions using the **up/down arrow keys**.  
- **Select** a suggestion by pressing **Enter**.  
- If the suggestion is a **category** (e.g., `@Files`), the list will refine to show only relevant items within that category.  

---

## List of All `@` Symbols  

- **`@Files`** - Reference specific files in your project.  
- **`@Folders`** - Reference entire folders for broader context.  
- **`@Code`** - Reference specific code snippets or symbols from your codebase.  
- **`@Docs`** - Access documentation and guides.  
- **`@Git`** - Access Git history and changes.  
- **`@Notepads`** - Access notepads.  
- **`@Summarized Composers`** - Work with summarized composer sessions.  
- **`@Cursor Rules`** - Work with cursor rules.  
- **`@Web`** - Reference external web resources and documentation.  
- **`@Link (paste)`** - Create links to specific code or documentation.  
- **`@Recent Changes`** - Reference recent changes in your code.  
- **`@Codebase`** - Reference your entire codebase as context (**Chat only**).  
- **`@Lint Errors`** - Reference lint errors (**Chat only**).  
- **`@Definitions`** - Look up symbol definitions (**Cmd + K only**).  

---

## Additional Symbols  

- **`# Files`** - Add files to the context without referencing.  
- **`/ Commands`** - Add open and active files to the context.  
  
</details>































<br><br>
<br><br>
___
<br><br>
<br><br>








# Ignore Files  




<details><summary>Click to expand..</summary>



Learn how to use `.cursorignore` and `.cursorindexingignore` to control file access and indexing in Cursor.  

---

## Overview  

Cursor provides two different ignore files to control how files are handled:  

- **`.cursorignore`**: Makes a best-effort attempt to exclude files from both AI features and indexing.  
- **`.cursorindexingignore`**: Controls only which files are indexed for search and context (same as the old `.cursorignore`).  

As of version **0.46**, `.cursorignore` attempts to exclude files from both **AI access and indexing** (similar to the previously unreleased `.cursorban`). For **indexing-only control**, like the old `.cursorignore`, use `.cursorindexingignore`.  

---

## `.cursorignore`  

The `.cursorignore` is **best-effort**, meaning **we do not guarantee that ignored files will never be sent up**. Bugs may allow ignored files to be accessed in certain cases. If you find any such issues, report them.  

**Use cases:**  
- Excluding **sensitive files** from AI access and indexing.  
- Ignoring **configuration files** that contain secrets.  
- Restricting access to **proprietary code**.  

**Effects:**  
Files listed in `.cursorignore` will be excluded from Cursor’s AI features:  
- Not included in **tab and chat requests**.  
- Not included in **AI context features**.  
- Not **indexed** for search or context.  
- Not **accessible** via `@`-symbols or other context tools.  

---

## `.cursorindexingignore`  

The `.cursorindexingignore` file **automatically inherits all patterns from your `.gitignore`** files.  

It only controls **which files are indexed** for search and context. This provides the same indexing control as the old `.cursorignore`.  

**Use cases:**  
- Excluding **large generated files** from indexing.  
- Skipping indexing of **binary files**.  
- Controlling which parts of the codebase are **searchable**.  
- **Optimizing** indexing performance.  

**Important:**  
Files in `.cursorindexingignore` **can still be manually included** as context or accessed by AI features – they just **won’t be automatically indexed** or included in search results.  

---

## File Format  

Both `.cursorignore` and `.cursorindexingignore` use the same syntax as `.gitignore`.  

### **Basic Patterns**  

```gitignore
# Ignore all files in the `dist` directory  
dist/  

# Ignore all `.log` files  
*.log  

# Ignore specific file `config.json`  
config.json  
```

### **Advanced Patterns**  

Include only `*.py` files in the `app` directory:  

```gitignore
# Ignore everything  
*  

# Do not ignore app  
!app/  

# Do not ignore directories inside app  
!app/*/  
!app/**/*/  

# Do not ignore Python files  
!*.py  
```

---

## Troubleshooting  

The ignore file syntax follows `.gitignore` exactly. If you encounter issues:  

- Replace **"cursorignore"** with **"gitignore"** in search queries.  
- Check **Stack Overflow** for similar patterns.  
- Test patterns with:  
  ```bash
  git check-ignore -v [file]
  ```
  to understand how matching works.  

**Common Gotchas:**  
- Patterns are **matched relative** to the ignore file location.  
- **Later patterns override earlier ones**.  
- **Directory patterns require a trailing slash (`/`)**.  
- **Negation patterns (`!`) must negate a previous pattern**.  

</details>




























<br><br>
<br><br>
___
<br><br>
<br><br>









# Codebase Indexing  




<details><summary>Click to expand..</summary>

Learn how to index your codebase in Cursor for more accurate AI assistance and search results.  

---

## Index your Codebase  

For **better and more accurate** codebase answers, you can **index your codebase**. Cursor computes **embeddings** for each file in your project, using them to **improve search results and AI responses**.  

### **How It Works:**  
- When a **project is opened**, Cursor **initializes indexing** for that workspace.  
- After the initial setup, Cursor will **automatically index new files** added to your workspace.  
- The indexing **status** is available under:  
  **Cursor Settings > Features > Codebase Indexing**.  

---

## Advanced Settings  

By default, Cursor **indexes all files** in your codebase.  

### **Customization Options:**  
Expand the **Show Settings** section to:  
- Enable or disable **automatic indexing** for new repositories.  
- Configure **which files should be ignored** during indexing.  

### **File Ignore Behavior:**  
- Cursor respects **all `.gitignore` files**, including those in subdirectories.  
- You can create a **`.cursorignore` file** for user-specific ignore patterns.  
- To prevent committing `.cursorignore`, add it to your **global `.gitignore`**.  

### **Optimizing Accuracy:**  
If your project contains **large content files** that AI **doesn’t need**, excluding them **can improve answer quality**.  

---

## Working with Large Monorepos  

For **large monorepos** (hundreds of thousands of files), **strategic indexing** is key.  

### **Best Practices:**  
- Use `.cursorignore` to let developers configure **which folders and paths** are indexed.  
- Add `.cursorignore` to **your global `.gitignore`**.  

This helps developers optimize indexing for **their specific work areas**.  

---

## FAQ  

### **Where can I see all indexed codebases?**  
There’s **no centralized list** of indexed codebases. To check a project’s status:  
1. Open the project in Cursor.  
2. Navigate to **Codebase Indexing settings**.  

### **How do I delete all indexed codebases?**  
- **Option 1:** Delete your Cursor **account** from Settings (removes all indexed data).  
- **Option 2:** Manually delete **individual codebases** from Codebase Indexing settings.  

**Note:** There’s **no bulk delete option** without deleting your account.  

</details>





































<br><br>
<br><br>
___
<br><br>
<br><br>









# Model Context Protocol (MCP)  



<details><summary>Click to expand..</summary>


## Server
- https://glama.ai/mcp/servers
- https://smithery.ai/ **HOT**
- https://cursor.directory/
- https://www.lmsystems.ai/servers **PAID CLOUD**



<br><br>
<br><br>




## What is MCP?  

The **Model Context Protocol (MCP)** is an **open protocol** that standardizes how applications provide **context and tools** to LLMs.  

Think of **MCP as a plugin system for Cursor** – it extends the agent’s capabilities by allowing integrations with **external data sources and tools**.  

📖 **[Learn More About MCP](#)**  

---

## Uses  

MCP enables Cursor to connect directly to **external systems and data sources**. Instead of manually feeding in project structure details, MCP **automates and standardizes** these interactions.  

### **Examples:**  
✅ **Databases** → Query databases without manually defining schemas.  
✅ **Notion** → Fetch data for implementation guidance.  
✅ **GitHub** → Create PRs, manage branches, find code.  
✅ **Memory** → Allow Cursor to store and recall information.  
✅ **Stripe** → Manage customers, subscriptions, and payments.  

---

## Architecture  

MCP servers are **lightweight programs** that expose capabilities via a standardized protocol. They act as **bridges** between Cursor and external tools or data sources.  

### **Supported Transport Types**  

#### 💻 **Stdio Transport (Local Only)**  
- Runs **on your local machine**  
- Managed automatically by Cursor  
- Communicates via **stdout**  
- **Only accessible locally**  

✅ **Input:** A **shell command** executed by Cursor  

#### 🌐 **SSE Transport (Local or Remote)**  
- Can run **locally or remotely**  
- Managed and run **by you**  
- Communicates **over the network**  
- **Can be shared across multiple machines**  

✅ **Input:** A **URL** to the `/sse` endpoint of an external MCP server  

📌 **Choosing the Right Transport:**  
- **Use stdio** for quick local development.  
- **Use SSE** for team-wide, distributed MCP setups.  

---

## Configuring MCP Servers  

MCP uses a **JSON-based configuration file**.  

### **Example (Stdio MCP Server using Node.js)**  
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
📌 **Notes:**  
- `command`: Defines the executable (e.g., `npx`)  
- `args`: Arguments passed to the command  
- `env`: Environment variables (e.g., API keys)  

---

## Configuration Locations  

### **Project-Specific Configuration**  
📂 **`.cursor/mcp.json`** → Only applies to **that specific project**  

### **Global Configuration**  
🏠 **`~/.cursor/mcp.json`** → Available **across all projects**  

📌 **Tip:** Add `.cursor/mcp.json` to your global `.gitignore` to prevent committing sensitive configurations.  

---

## Using MCP Tools in Cursor  

### **Automatic Tool Usage**  
- The **Composer Agent** will automatically use relevant MCP tools listed under **Available Tools** in the MCP settings.  
- You can also **directly prompt** the agent to use a specific tool by name or description.  

### **Tool Approval**  
- By default, Cursor **asks for approval** before using an MCP tool.  
- You can review the tool call **arguments** before executing.  

### **Yolo Mode (Auto-Execute MCP Tools)**  
- **Enabling Yolo Mode** allows Cursor to **automatically run MCP tools** without approval, just like terminal commands.  
📖 **[Read more about Yolo Mode](#)**  

---

## Tool Responses  

When an MCP tool runs, Cursor will **display the response in chat**, along with:  
- **Tool call arguments**  
- **Expanded tool response details**  

---

## Limitations  

🔴 MCP is **still evolving** – some known limitations:  
- Cursor **only sends the first 40 tools** to the Agent.  
- MCP **may not work over SSH** or certain remote development setups.  
- **Resources (data storage/retrieval)** are **not yet supported** in Cursor (coming in future updates).  


</details>








































<br><br>
<br><br>
___
<br><br>
<br><br>




# Good 2 Know



<details><summary>Click to expand..</summary>


# Structure
- keep files small and create a new file for new components

  
</details>






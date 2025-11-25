# Tools
- https://docs.cursor.com/chat/tools  
- Vollständige Liste aller verfügbaren Tools mit aktualisierten RPC-Aufrufen:


---

## Orchestrierung

- **multi_tool_use.parallel** – Mehrere unabhängige Tool-Aufrufe parallel ausführen.


---

## Datei- und Code-Operationen

### **functions.read_file** – Lesen von Dateiinhalten (mit anpassbarem Bereich)

<details><summary>Click to expand..</summary>

```
Read the contents of a file within your codebase.
— Up to 750 lines in max mode
— Up to 250 lines in other modes
```

**Beispiel: iteratives Lesen einer großen Datei**

```markdown
Tool: functions.read_file
Parameter:
  target_file: "./.ai/rules/shared-rules/core/core-rules/base.md"
  start_line_one_indexed: 1
  end_line_one_indexed_inclusive: 250
  should_read_entire_file: false
  explanation: "Reading the first chunk (1-250) of base.md for iterative full content retrieval."
```

Antwort enthält die Gesamtanzahl der Zeilen → nächster Aufruf:

```markdown
Tool: functions.read_file
Parameter:
  target_file: "./.ai/rules/shared-rules/core/core-rules/base.md"
  start_line_one_indexed: 251
  end_line_one_indexed_inclusive: 389
  should_read_entire_file: false
  explanation: "Reading the final chunk (251-389) of base.md for iterative full content retrieval."
```

</details>

---

- **functions.edit_file** – Bestehende Datei partiell ändern oder neue Datei erstellen.  
- **functions.search_replace** – Einzigartig identifizierte Textstelle in einer Datei ersetzen.  
- **functions.delete_file** – Datei löschen.  
- **functions.reapply** – Letzte Edit-Anweisung erneut anwenden (falls fehlerhaft umgesetzt).  
- **functions.list_dir** – Verzeichnisinhalt auflisten.  
- **functions.grep** – Schnelle Code-/Textsuche (Regex, ripgrep).  
- **functions.edit_notebook** – Jupyter-Notebook-Zellen gezielt ändern oder erstellen.  

---

## Ausführungstools

- **functions.run_terminal_cmd** – Shell-Befehl ausführen (non-interaktiv empfohlen).  

---

## Linting

- **`read_lints`**:  
  - **`paths?: string[]`** – optional; Liste von Dateien/Ordnern, für die Linter-Errors abgefragt werden.  
    - Wenn gesetzt → nur diese Pfade.  
    - Wenn weggelassen → gesamter Workspace.

Ich habe es so aufgerufen:

```json
{
  "paths": [
    "c:\\git\\test\\eslint.config.ts"
  ]
}
```

Weitere Filter- oder Options-Parameter gibt es bei diesem Tool nicht.
---

## Web & Recherche

- **functions.web_search** – Websuche für aktuelle Informationen.  

---

## Chat / Composer

- **user_query** – Benutzertext in die Chatbox einfügen.  

---

## Regeln & Kontext

- **functions.fetch_rules** – Abrufen nutzerspezifischer Regeln.  

**Beispiel:**

```python
print(functions.fetch_rules(
    rule_names = [
        ".ai/rules/shared-rules/core/global-rules/emoji-communication.mdc",
        ".ai/rules/custom-rules/database-rules/evident-reference-documentation-always.mdc"
    ]
))
```

---

## Codebase-Suche

- **codebase_search** – Semantische Suche im Code nach relevanten Snippets.  

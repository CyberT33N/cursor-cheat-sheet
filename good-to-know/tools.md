# Tools
- https://docs.cursor.com/chat/tools
- Hier ist eine vollständige Liste aller Tools, die mir zur Verfügung stehen:


Cursor will call tools like this:
```
Tool Name: default_api.read_file
```






## Dateisystem & Codebase-Tools

### **codebase_search** - Semantische Suche im Code nach relevanten Snippets



<br><br>


### **read_file** - Lesen von Dateiinhalten mit anpassbarem Bereich

<details><summary>Click to expand..</summary>

```
Read the contents of a file within your codebase.
— Up to 750 lines in max mode
— Up to 250 lines in other modes
```


Absolut! Hier sind die detaillierten Aufrufe für das `read_file`-Tool, die ich gerade verwendet habe, um die Datei `./.ai/rules/shared-rules/core/core-rules/base.md` iterativ zu lesen, nachdem der erste Aufruf gezeigt hat, dass sie mehr als 250 Zeilen hat (insgesamt 389):

**1. Aufruf (Lesen des ersten Blocks):**


Die Information über die Gesamtanzahl der Zeilen war Teil der Antwort, die ich vom ersten read_file-Aufruf (dem für die Zeilen 1-250) erhalten habe.

```markdown
Tool: `read_file`
Parameter:
  target_file: "./.ai/rules/shared-rules/core/core-rules/base.md"
  start_line_one_indexed: 1
  end_line_one_indexed_inclusive: 250
  should_read_entire_file: false
  explanation: "Reading the first chunk (1-250) of base.md for iterative full content retrieval."
```
*(Die Antwort dieses Aufrufs enthielt die Information "total 389 lines", was den nächsten Schritt auslöste.)*

**2. Aufruf (Lesen des verbleibenden Blocks):**

```markdown
Tool: `read_file`
Parameter:
  target_file: "./.ai/rules/shared-rules/core/core-rules/base.md"
  start_line_one_indexed: 251
  end_line_one_indexed_inclusive: 389  # Ende auf die Gesamtzeilenzahl gesetzt
  should_read_entire_file: false
  explanation: "Reading the second and final chunk (251-389) of base.md for iterative full content retrieval."
```

Diese beiden Aufrufe ermöglichen es, den gesamten Inhalt auch von größeren Dateien zu erfassen, indem die Leseoperation in Blöcke aufgeteilt wird.






</details>











<br><br>


  
- **list_dir** - Auflisten des Inhalts eines Verzeichnisses
- **file_search** - Fuzzy-Suche nach Dateien anhand von Teilen des Pfades
- **edit_file** - Vorschlagen und Anwenden von Änderungen an Dateien
- **delete_file** - Löschen einer Datei
- **reapply** - Erneutes Anwenden der letzten Bearbeitung mit einem intelligenteren Modell
- **grep_search** - Textbasierte Regex-Suche in Dateien

## Ausführungstools
- **run_terminal_cmd** - Ausführen von Terminal-Befehlen

## Chat/Composer
- **user_query** - Benutzer Text in Chat Box

## Regeln & Kontext
- **fetch_rules** - Abrufen von nutzerspezifischen Regeln
```
print(default_api.fetch_rules(
    rule_names = [
        ".ai/rules/shared-rules/core/global-rules/emoji-communication.mdc",
        ".ai/rules/custom-rules/database-rules/evident-reference-documentation-always.mdc"
        # Füge hier weitere Regelpfade hinzu, falls benötigt
    ]
))
```

## Web & Recherche
- **web_search** - Suche im Web nach Echtzeit-Informationen

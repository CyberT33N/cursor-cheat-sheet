# Tools
- https://docs.cursor.com/chat/tools
- Hier ist eine vollständige Liste aller Tools, die mir zur Verfügung stehen:

## Dateisystem & Codebase-Tools
- **codebase_search** - Semantische Suche im Code nach relevanten Snippets

- **read_file** - Lesen von Dateiinhalten mit anpassbarem Bereich
```
Read the contents of a file within your codebase.
— Up to 750 lines in max mode
— Up to 250 lines in other modes
```
  
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

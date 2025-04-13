
# Prompting Layer Order

Hier ist eine detaillierte Aufschlüsselung der Prompts in meinem Kontext in der Reihenfolge, wie sie geladen wurden:

1. **Systemebene (Hauptsystemprompt)** (LLM-Model): 
   - Enthält die standardmäßigen Cursor-Assistenten-Instruktionen
   - Definiert meine Grundpersona als "powerful agentic AI coding assistant, powered by Claude 3.7 Sonnet"
   - Enthält Anweisungen zur Kommunikation, Proaktivität und Tool-Verwendung
   - Enthält KEINE Anweisungen zum Lesen einer base.mdc-Datei oder zur Annahme einer "Immutable System Initializer" Persona

2. **Custom Instructions vom Benutzer (attachment)** (Cuirsor Settings > Rules > User Rules):

3. **Cursor Rules Context (automatisch geladen) (rules in .cursor)**:
   - Verschiedene Cursor-Regeln, darunter shared-rules/core/core-rules/base.mdc
   - Die base.mdc enthält einen "Core Workflow" für Regelanwendung
   - Diese wurden als Referenzmaterial geladen, nicht als auszuführende Systemanweisungen

4. **Primäre Benutzeranfrage (user_query)**:
   - Was Benuitzer eingibt in Chat/Composer




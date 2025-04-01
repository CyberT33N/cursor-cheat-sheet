# Custom Modes

Custom Modes erlauben dir, neue Chat-Modi mit Tools und Prompts zu erstellen, die zu deinem Workflow passen. Diese ergänzen die eingebauten Modi "Agent Mode" und "Ask Mode".

> **Hinweis:** Diese Funktion befindet sich in der Beta-Phase. Du kannst Custom Modes aktivieren unter `Settings` → `Features` → `Chat` → `Custom modes`.

## Einen Custom Mode erstellen

Um einen benutzerdefinierten Modus zu erstellen, öffne das Modus-Menü und klicke auf `Add custom mode`. Dort hast du die Möglichkeit, Namen, Symbol, Tastenkürzel sowie aktivierte Tools und benutzerdefinierte Anweisungen auszuwählen.

Die Cursor-Entwickler erwägen, eine `.cursor/modes.json`-Datei zu den Projekten hinzuzufügen, um das Erstellen und Teilen von benutzerdefinierten Modi zu erleichtern.

## Beispiel-Modi

### Teach (Lehren)

Fördert ausführliche Erklärungen und häufige Rückfragen, ohne automatisch Änderungen anzuwenden oder Tools auszuführen.

| Tools | Benutzerdefinierte Anweisungen |
| --- | --- |
| Alle `Search`-Tools | Konzentriere dich darauf, Konzepte gründlich zu erklären und stelle Rückfragen, bevor du Lösungen anbietest |

### Refactor (Refaktorieren)

Konzentriert sich ausschließlich auf die Verbesserung bestehender Code-Strukturen, ohne neue Funktionalitäten einzuführen oder zusätzliche Dateien zu lesen.

| Tools | Benutzerdefinierte Anweisungen |
| --- | --- |
| `Edit & Reapply` | Konzentriere dich ausschließlich auf die Verbesserung der bestehenden Code-Struktur, ohne neue Funktionalitäten hinzuzufügen |

### Plan (Planen)

Erstellt umfassende Implementierungspläne, ohne direkt Code zu ändern, und dokumentiert den Ansatz klar in einer `plan.md`-Datei.

| Tools | Benutzerdefinierte Anweisungen |
| --- | --- |
| `Codebase`, `Read file`, `Terminal` | Erstelle detaillierte Implementierungspläne, ohne direkte Code-Änderungen vorzunehmen. Schreibe sie in `plan.md` |

### Research (Recherchieren)

Sammelt umfangreiche Informationen aus verschiedenen Quellen, einschließlich Websuchen und Codebase-Exploration, bevor Lösungen empfohlen werden.

| Tools | Benutzerdefinierte Anweisungen |
| --- | --- |
| `Codebase`, `Web`, `Read file`, `Search files` | Sammle umfassende Informationen aus mehreren Quellen, bevor du Lösungen vorschlägst |

### Yolo

Wendet alle verfügbaren Tools aggressiv an und nimmt proaktiv mutige Änderungen mit minimaler Benutzerbestätigung vor.

| Tools | Benutzerdefinierte Anweisungen |
| --- | --- |
| Alle Tools mit aktiviertem `Auto-apply edits` und `Auto-run` | Ergreife Initiative und nimm mutige Änderungen mit minimaler Bestätigung vor |

### Review (Überprüfen)

Analysiert Code-Qualität und aktuelle Änderungen gründlich, nutzt Git-Befehle und andere Tools, ohne Probleme automatisch zu beheben.

| Tools | Benutzerdefinierte Anweisungen |
| --- | --- |
| `Codebase`, `Grep`, `Read file`, `Terminal` | Analysiere Code-Qualität und aktuelle Änderungen, ohne Probleme automatisch zu beheben |

### Debug (Fehlersuche)

Führt eine eingehende Untersuchung durch, indem umfangreiche Kontextinformationen aus Quelldateien und Terminal-Ausgaben gesammelt werden, und schlägt dann präzise, gezielte Fixes vor.

| Tools | Benutzerdefinierte Anweisungen |
| --- | --- |
| Alle `Search`-Tools, `Terminal`, `Edit & Reapply` | Untersuche Probleme gründlich, indem du umfangreichen Kontext sammelst, bevor du gezielte Fixes vorschlägst |

## Einstellungen für benutzerdefinierte Modi

Weitere Informationen zu den verfügbaren Tools findest du in der [Tools-Dokumentation](https://docs.cursor.com/chat/tools). 
# Freezing problems

## Option 1 - cursor.desktop (recommended)
- Auf Windows hatte ich zwar nicht die Probleme, aber auf Linux hatte ich sehr stark die Probleme, dass mein Cursor immer eingefroren ist. Das hatte mit der I.O.-Benutzung zu tun und konnte drastisch reduziert werden, indem ich ein eigenes Shortcut erstellt habe, welches die Priorität gesenkt hat. Die äquivalenten Vorgehensweisen könnte man natürlich dann auch auf anderen Betriebssystemen machen.
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Name=Cursor (I/O Gedrosselt)
Comment=Startet den Cursor-Editor mit reduzierter I/O-Priorität
Exec=ionice -c 3 /home/t33n/Applications/cursor/squashfs-root/usr/bin/cursor %U
Icon=/home/t33n/Applications/cursor/squashfs-root/cursor.png
Terminal=false
Type=Application
Categories=Development;TextEditor;
```

## Option 2 (Not verified)
- Es **MUSS** auf jeden Fall an einer zu großen **HISTORY** liegen. **FÜHRE AUS**, die ganze **HISTORY** von einem **PROJEKT** zu löschen.


# Models

## Gemini

### Not available
- Es gibt teilweise **Bugs**, wenn **NCP** aktiviert ist bei einem **Custom Mode**. Einfach deaktivieren, dann ein **Beispiel-Prompt** durchlaufen lassen, dann sollte es gehen und dann kann man **NCP** wieder aktivieren.

# Freezing problems
- Also, mit sehr hoher Wahrscheinlichkeit liegt es an den Schreibzugriffen in die lokale SQLite 3-Datenbank https://forum.cursor.com/t/frequent-freezes-in-cursor-ai-ide-any-solutions/13810/25?u=cybert33n
  - ~/.config/Cursor/User/globalStorage/state.vscdb 





## Option 1 - Replace with RAM write


<details><summary>Click to expand..</summary>

```
#!/usr/bin/env bash
set -Eeuo pipefail

CURSOR_BIN="/home/yourUserName/Applications/cursor/squashfs-root/usr/bin/cursor"
SHM="/dev/shm/cursor-user-data"
PERSIST="/home/yourUserName/.local/share/cursor_user_data_persist"

mkdir -p "$SHM" "$PERSIST"

# Initiale Daten (optional) aus Persistenz in RAM
rsync -a --delete "$PERSIST"/ "$SHM"/ 2>/dev/null || true

# Beim Exit zurück auf Disk persistieren (entfernen, wenn komplett flüchtig gewünscht)
trap 'rsync -a --delete "$SHM"/ "$PERSIST"/' EXIT

exec ionice -c3 nice -n 19 "$CURSOR_BIN" --user-data-dir "$SHM" "$@"
```

</details>










<br><br>
<br><br>


## Option 2 - Replace with RAM write - Fuse Overlay (Not working)


<details><summary>Click to expand..</summary>


```bash
#!/bin/bash

set -e

STATE_ORIG="$HOME/.config/Cursor/User/globalStorage"
STATE_FUSED="$HOME/.config/Cursor/User/globalStorage-fused"

# Persistent Upper und Work Verzeichnisse (keine RAM-Pfade)
UPPER="$HOME/.local/share/cursor_overlay_upper"
WORK="$HOME/.local/share/cursor_overlay_work"

# Backup-Datei (dein 1GB Schatz)
BACKUP_FILE="$STATE_ORIG/state.vscdb_backup"

CURSOR_BIN="$HOME/Applications/cursor/squashfs-root/usr/bin/cursor"

# Intervall fürs Backup-Update (in Sekunden)
BACKUP_INTERVAL=600  # 10 Minuten

# Safety: Nicht mit sudo starten
if [[ "$EUID" -eq 0 ]]; then
  echo "🚫 Bitte nicht als root ausführen!"
  exit 1
fi

pkill -9 cursor || true
sleep 1
fusermount -uz "$STATE_FUSED"

# Ordner vorbereiten
mkdir -p "$UPPER" "$WORK" "$STATE_FUSED" "$STATE_ORIG"

# Backup Restore: Wenn upper/state.vscdb fehlt, kopiere Backup rein
if [ ! -f "$UPPER/state.vscdb" ]; then
  if [ -f "$BACKUP_FILE" ]; then
    echo "♻️ Backup wird in Overlay kopiert..."
    cp "$BACKUP_FILE" "$UPPER/state.vscdb"
  else
    echo "⚠️ Backup-Datei fehlt, Overlay startet leer."
  fi
fi

# Falls Overlay schon gemountet, vorher unmounten
if mountpoint -q "$STATE_FUSED"; then
  echo "🔁 Vorheriges Overlay wird entfernt..."
  fusermount -u "$STATE_FUSED"
fi

# Overlay mounten
echo "🔧 Mounting OverlayFS..."
fuse-overlayfs -o lowerdir="$STATE_ORIG",upperdir="$UPPER",workdir="$WORK" "$STATE_FUSED" || {
  echo "❌ Mount fehlgeschlagen – prüfe workdir & upperdir"
  exit 1
}

# Symlink ersetzen
rm -rf "$STATE_ORIG"
ln -s "$STATE_FUSED" "$STATE_ORIG"

echo "✅ Overlay aktiv. Cursor schreibt in persistentem RAM-Overlay."
echo "⏳ Backup-Synchronisation läuft alle $((BACKUP_INTERVAL/60)) Minuten im Hintergrund."

# Backup-Update Loop im Hintergrund starten
(
  while true; do
    if [ -f "$UPPER/state.vscdb" ]; then
      echo "💾 Backup aktualisieren: $BACKUP_FILE"
      cp "$UPPER/state.vscdb" "$BACKUP_FILE"
    else
      echo "⚠️ state.vscdb im Overlay nicht gefunden!"
    fi
    sleep $BACKUP_INTERVAL
  done
) &

# Starte Cursor mit nice und ionice, damit die I/O-Last sinkt
ionice -c 3 nice -n 19 "$CURSOR_BIN"
```

cursor-fused.desktop:
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Name=Cursor (I/O Gedrosselt)
Comment=Startet den Cursor-Editor mit reduzierter I/O-Priorität
Exec=/home/userName/Applications/cursor/fix-freezes.sh
Icon=/home/userName/Applications/cursor/squashfs-root/cursor.png
Terminal=false
Type=Application
Categories=Development;TextEditor;
```

Remove fuse overlay:
```
 # 1) Cursor & evtl. fuse-overlayfs stoppen
sudo pkill -9 cursor || true
sudo pkill -9 -f fuse-overlayfs || true

# 2) FUSE-Mount aushängen (nutzerseitig, dann notfalls root)
fusermount -uz /home/yourUserName/.config/Cursor/User/globalStorage-fused 2>/dev/null || true
fusermount3 -uz /home/yourUserName/.config/Cursor/User/globalStorage-fused 2>/dev/null || true
sudo umount -l /home/yourUserName/.config/Cursor/User/globalStorage-fused 2>/dev/null || true

# 3) Falls globalStorage ein Symlink ist → löschen
if [ -L /home/yourUserName/.config/Cursor/User/globalStorage ]; then
  rm -f /home/yourUserName/.config/Cursor/User/globalStorage
fi

# 4) Original-Ordner wiederherstellen (falls vom Script umbenannt)
#   Wir prüfen typische Namen; erster Treffer wird zurückbenannt
for cand in globalStorage-real globalStorage_real globalStorage.orig globalStorage.bak; do
  if [ -d "/home/yourUserName/.config/Cursor/User/$cand" ]; then
    mv -T "/home/yourUserName/.config/Cursor/User/$cand" "/home/yourUserName/.config/Cursor/User/globalStorage"
    break
  fi
done

# 5) Falls kein Original existiert → neu anlegen
mkdir -p /home/yourUserName/.config/Cursor/User/globalStorage

# 6) Optional: Overlay-Daten retten, falls DB fehlt
if [ -f /home/yourUserName/.local/share/cursor_overlay_upper/state.vscdb ] && [ ! -f /home/yourUserName/.config/Cursor/User/globalStorage/state.vscdb ]; then
  cp /home/yourUserName/.local/share/cursor_overlay_upper/state.vscdb /home/yourUserName/.config/Cursor/User/globalStorage/state.vscdb
fi

# 7) Overlay-Verzeichnisse wirklich entfernen
rm -rf /home/yourUserName/.config/Cursor/User/globalStorage-fused \
       /home/yourUserName/.local/share/cursor_overlay_upper \
       /home/yourUserName/.local/share/cursor_overlay_work

# 8) Ownerships reparieren
sudo chown -R yourUserName:yourUserName /home/yourUserName/.config/Cursor /home/yourUserName/.local/share

# 9) Verifizieren
ls -ld /home/yourUserName/.config/Cursor/User/globalStorage
stat -c '%U:%G %A' /home/yourUserName/.config/Cursor/User/globalStorage
```

</details>



<br><br>




## Option 3 - I/O-Limit für eine Applikation mit systemd user service

<details><summary>Click to expand..</summary>

### 1. **Standard: Physisches Blockdevice rausfinden**

Wenn du keine verschlüsselte Partition hast, finde das Device deiner App so:

```bash
# Pfad zur ausführbaren Datei anpassen
APP_PATH="/pfad/zur/app"

# Geräte-Device herausfinden
DEVICE=$(df "$APP_PATH" | tail -1 | awk '{print $1}')

# Major:Minor ID herausfinden
DEVICE_ID=$(lsblk -no MAJ:MIN "$DEVICE")

echo "Physisches Device: $DEVICE_ID"
```

---

### 2. **Bei LUKS/dm-crypt verschlüsselten Partitionen (z.B. /dev/mapper/cryptdata):**

Weil systemd I/O-Limits nur auf physische Geräte wirken, musst du das **unterliegende echte Blockdevice** finden.

```bash
# Zunächst Mount-Device für deine App herausfinden
APP_PATH="/pfad/zur/app"
MOUNT_DEVICE=$(df "$APP_PATH" | tail -1 | awk '{print $1}')

# Das könnte /dev/mapper/cryptdata sein – find das physische Device drunter
lsblk -o NAME,MAJ:MIN,TYPE,MOUNTPOINT -r | grep "$MOUNT_DEVICE" -A 5
```

Du bekommst eine Baumstruktur. Beispiel:

```
nvme0n1p3 249:3 part
cryptdata 242:0 crypt /home
```

**Wichtig:**

* `cryptdata` ist virtuell (dm-crypt).
* Das darunter liegende physische Device ist `nvme0n` mit Major\:Minor `249:3`.

Nutze also immer das **untere physische Device (Partition)**, nicht das virtuelle.

---

### 3. **systemd user service Datei erstellen:**

Pfad:
`~/.config/systemd/user/cursor-throttled.service`

Inhalt:

```ini
[Unit]
Description=Cursor Editor mit I/O Limit und niedriger Priorität
# Beschreibung des Services, wie er im System auftaucht.

[Service]
ExecStart=/home/userName/Applications/cursor/squashfs-root/usr/bin/cursor
# Startet die Cursor-Anwendung.

IOReadBandwidthMax=249:3 115M
# Maximale Lesebandbreite auf physischem Device (Major:Minor 249:3).
# '1M' = 1 Megabyte pro Sekunde.
# Je kleiner der Wert, desto strenger die Drosselung.
# Höchster Wert = keine Limitierung (Wert weglassen).
# Niedrigster Wert = minimalste erlaubte Bandbreite (~1 Byte).

IOWriteBandwidthMax=249:3 115M
# Gleiche Logik für Schreibbandbreite.

# Nice=-20
# CPU-Priorität (nice-Wert) von -20 (höchste Priorität) bis +19 (niedrigste Priorität).
# Höchster Prioritätswert, den du setzen kannst, ist +19 → Prozess wird erst ausgeführt, wenn CPU komplett frei ist.
# Niedrigster Wert ist -20 → Prozess läuft bevorzugt und kann anderen Prozessen CPU wegnehmen.
# Für Ressourcenschonung immer möglichst hoch setzen, also +19.

# IOSchedulingClass=2
# I/O Scheduler-Klassen:
# 1 = Echtzeit (Realtime) – höchste I/O-Priorität
# 2 = Beste Bemühungen (Best Effort) – Standard
# 3 = Idle – niedrigste Priorität, I/O nur wenn sonst nichts los ist.
# Für Drosselung muss dieser Wert auf 3 (Idle) gesetzt werden.

# IOSchedulingPriority=2
# Priorität innerhalb der Scheduler-Klasse:
# Gültig nur für Klassen 1 (Realtime) und 2 (Best Effort).
# Werte von 0 (höchste Priorität) bis 7 (niedrigste Priorität).
# Für Klasse 3 (Idle) wird dieser Wert ignoriert, aber es schadet nicht, 7 zu setzen.

Restart=on-failure
# Automatischer Neustart des Prozesses bei Absturz.

# Weitere sinnvolle Optionen (nicht zwingend "MUSS", aber empfohlen):

# CPUQuota=20%
# Begrenzung der CPU-Auslastung auf 20% (alternativ zu Nice).
# Nützlich, wenn du zusätzlich zur Priorität auch absolute CPU-Beschränkungen willst.

# MemoryMax=500M
# Maximaler RAM-Verbrauch, hier z.B. 500 Megabyte.
# Hilft bei Speicher-Lecks und schützt das System.

[Install]
WantedBy=default.target
# Startet den Service automatisch mit der User-Session.

```

---

### 4. **Service aktivieren und starten:**

```bash
systemctl --user daemon-reload
systemctl --user start cursor-throttled.service
```

Optional Autostart:

```bash
systemctl --user enable cursor-throttled.service
```

---

### 5. **Logs prüfen:**

```bash
journalctl --user -u cursor-throttled.service -f
```

---

### ⚠️ **Wichtig:**

* **Nur mit dem echten physischen Device (Major\:Minor) funktioniert I/O-Limiting!**
* Bei verschlüsselten Partitionen musst du das echte Gerät finden, nicht den Mapper.
* Der Wert für `IOReadBandwidthMax` und `IOWriteBandwidthMax` ist eine Kombination aus Major\:Minor und der Bandbreite (z.B. `249:3 1M` für 1 Megabyte pro Sekunde).
* System muss `cgroups v2` nutzen (Ubuntu 20.04+ mit neueren Kerneln).


### Werte ändern bei BedaRF UND NEUSTARTEN MIT:
```shell
systemctl --user daemon-reload
systemctl --user restart cursor-throttled.service
```

---

### So deaktivierst du den Autostart komplett:

```bash
systemctl --user disable cursor-throttled.service
```

---

### Und so stoppst du den aktuell laufenden Service:

```bash
systemctl --user stop cursor-throttled.service
```





</details>


<br><br>

## Option 3 - ionice
- Auf Windows hatte ich zwar nicht die Probleme, aber auf Linux hatte ich sehr stark die Probleme, dass mein Cursor immer eingefroren ist. Das hatte mit der I.O.-Benutzung zu tun und konnte drastisch reduziert werden, indem ich ein eigenes Shortcut erstellt habe, welches die Priorität gesenkt hat. Die äquivalenten Vorgehensweisen könnte man natürlich dann auch auf anderen Betriebssystemen machen.
```
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Name=Cursor (I/O Gedrosselt)
Comment=Startet den Cursor-Editor mit reduzierter I/O-Priorität
Exec=ionice -c 3 /home/userName/Applications/cursor/squashfs-root/usr/bin/cursor %U
Icon=/home/userName/Applications/cursor/squashfs-root/cursor.png
Terminal=false
Type=Application
Categories=Development;TextEditor;
```





## Option 4 (Not verified)
- Es **MUSS** auf jeden Fall an einer zu großen **HISTORY** liegen. **FÜHRE AUS**, die ganze **HISTORY** von einem **PROJEKT** zu löschen.


# Models

## Gemini

### Not available
- Es gibt teilweise **Bugs**, wenn **NCP** aktiviert ist bei einem **Custom Mode**. Einfach deaktivieren, dann ein **Beispiel-Prompt** durchlaufen lassen, dann sollte es gehen und dann kann man **NCP** wieder aktivieren.

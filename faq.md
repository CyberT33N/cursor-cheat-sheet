# Freezing problems


## Option 1 - I/O-Limit für eine Applikation mit systemd user service (recommended)

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
Description=Cursor Editor mit I/O Limit

[Service]
ExecStart=/pfad/zur/app
# Physisches Blockdevice hier setzen (z.B. 249:3)
IOReadBandwidthMax=249:3 1M
IOWriteBandwidthMax=249:3 1M
Restart=on-failure

[Install]
WantedBy=default.target
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


</details>

<br><br>

## Option 2 - ionice (recommended)
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





## Option 3 (Not verified)
- Es **MUSS** auf jeden Fall an einer zu großen **HISTORY** liegen. **FÜHRE AUS**, die ganze **HISTORY** von einem **PROJEKT** zu löschen.


# Models

## Gemini

### Not available
- Es gibt teilweise **Bugs**, wenn **NCP** aktiviert ist bei einem **Custom Mode**. Einfach deaktivieren, dann ein **Beispiel-Prompt** durchlaufen lassen, dann sollte es gehen und dann kann man **NCP** wieder aktivieren.

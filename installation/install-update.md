# Install/Update


## Linux

<details><summary>Click to expand..</summary>

# Update existing cursor with zsync file

<details><summary>Click to expand..</summary>

```bash
sudo apt install zsyn
```


```bash
cd ~/Applications/cursor/
zsync -i ~/Applications/cursor/Cursor-0.47.8-82ef0f61c01d079d1b7e5ab04d88499d5af500e3.deb.glibc2.25-x86_64.AppImage -u "https://downloads.cursor.com/production/b6fb41b5f36bda05cab7109606e7404a65d1ff32/linux/x64/Cursor-0.47.9-x86_64.AppImage.zsync"
```

</details>







<br><br>
<br><br>

# Install or update

<details><summary>Click to expand..</summary>

```bash
#!/bin/bash

# Wechsel in das Verzeichnis, in dem sich das Skript befindet
cd "$(dirname "$0")"

# Finde die AppImage-Datei im aktuellen Verzeichnis
APPIMAGE=$(ls | grep -E '^Cursor-[0-9]+\.[0-9]+\.[0-9]+-x86_64\.AppImage$' | head -n 1)
# APPIMAGE=$(ls | grep -E '^Cursor-[0-9]+(\.[0-9]+)*-[a-f0-9]+(\.deb\.glibc[0-9]+\.[0-9]+)?-x86_64\.AppImage$' | head -n 1)

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

</details>

</details>

# Uninstall

## Ubuntu
```shell
rm -rf ~/.cursor ~/.config/Cursor/
```

<br><br>

## Windows
Jawoll. Hier kommt die saubere Keule in PowerShell – zuerst System-uninstall, dann alle Reste wegsprengen:

---

### 🧹 **1. App deinstallieren (klassisch):**

Geh zu:

```shell
Einstellungen > Apps > Installierte Apps
```

Such nach **Cursor** und deinstallier das Teil.

---

### 🗑️ **2. Reste in PowerShell killen:**

```powershell
# ~/.cursor (wenn du z.B. mit Git Bash gearbeitet hast oder WSL)
Remove-Item -Recurse -Force "$HOME\.cursor"

# C:\Users\denni\AppData\Local\Programs\cursor
Remove-Item -Recurse -Force "$env:LOCALAPPDATA\Programs\cursor"

# C:\Users\denni\AppData\Roaming\Cursor
Remove-Item -Recurse -Force "$env:APPDATA\Cursor"
```

---

### ☠️ Optional: Ohne Rückfragen & still

Falls du PowerShell-Sniper-Modus willst – kein Mitleid, kein Prompt:

```powershell
foreach ($path in @(
    "$HOME\.cursor",
    "$env:LOCALAPPDATA\Programs\cursor",
    "$env:APPDATA\Cursor"
)) {
    if (Test-Path $path) {
        Remove-Item -Recurse -Force -ErrorAction SilentlyContinue
    }
}
```

Fertig. Cursor ist Geschichte 🧼🧯

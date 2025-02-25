# Cursor Cheat Sheet


# Install/Update


```bash
#!/bin/bash

# Wechsel in das Verzeichnis, in dem sich das Skript befindet
cd "$(dirname "$0")"

# Finde die AppImage-Datei im aktuellen Verzeichnis
APPIMAGE=$(ls | grep -E '^cursor-[0-9.]+(-build-[a-zA-Z0-9]+)?-?x86_64\.AppImage$' | head -n 1)

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

# Setze korrekte Rechte für chrome-sandbox
sudo chown root:root squashfs-root/chrome-sandbox
sudo chmod 4755 squashfs-root/chrome-sandbox

# Starte die extrahierte Anwendung
./squashfs-root/AppRun

```














<br><br>
<br><br>

# Uninstall

## Ubuntu
```shell
rm -rf ~/.cursor ~/.config/Cursor/
```

















<br><br>
<br><br>
___
<br><br>
<br><br>



# Models


## Ranking
1. 03-mini
2. claude-3.5-sonnet
3. gpt-4o








<br><br>
<br><br>

## Use local model


<details><summary>Click to expand..</summary>



# Ollama


1. Allow Web Origins in Ollama. Will be needed for Cursor to send the request to ngrok to your ollama

```shell
sudo systemctl edit ollama.service

# Add this
[Service]
Environment="OLLAMA_ORIGINS=*"
```
- Make sure that you add the environment variable above this line `Edits below this comment will be discarded`

Then restart:
```shell
systemctl daemon-reload
systemctl restart ollama
```


<br><br>

2. Run your desired model by using ollama
- https://github.com/CyberT33N/ollama-cheat-sheet/blob/main/README.md#import-from-gguf
```shell
ollama run deepseek-v2-coder-lite
```


3. Start custom proxy layer to enhance security with ngrok
- https://github.com/CyberT33N/proxy-auth
- Make sure to define a bearer token in the .env file. The value of this will be the API key which you enter in cursor later..
- Related to point 5. there is a verify button in cursor which will send a OPTIONS method request without baerer token. In the project is a condition for this commented out. You can enable it to 1x time allow the request that cursor is happy and then you can commit it out again and restart. This only has to be done once..

<br><br>

4. Tunneling proxy layer from above which will send request to ollama rest api on your machine
- https://github.com/ollama/ollama/blob/main/docs/faq.id opidmd#how-can-i-use-ollama-with-ngrok
```shell
ngrok http 3000 --host-header="localhost:3000"
```

<br><br>

5. Open Cursor > Cursor Settings > Models
  <br> 3.1 Disable all other models and add new model which has the same name as your hosted llm in ollama in my case `deepseek-v2-coder-lite`
  <br> 3.2 At section OpenAI API Key add your base url `https://xxxxxxxxxxxxx.ngrok-free.app/v1`. At the API Key add your custom bearer token value from point 3 (**Just the value not the word Bearer**). And then click verify button
   - If you get 403 then something is not working with CORS.

<br><br>

6. Enjoy <3

</details>


























# Good 2 Know



<br><br>
<br><br>
___
<br><br>
<br><br>




<details><summary>Click to expand..</summary>


# Structure
- keep files small and create a new file for new components

  
</details>






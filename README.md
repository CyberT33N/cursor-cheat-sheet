# Cursor Cheat Sheet


# Install
```shell
./cursor-0.44.11x86_64.AppImage --appimage-extract

sudo chown root:root squashfs-root/chrome-sandbox
sudo chmod 4755 squashfs-root/chrome-sandbox

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

<br><br>

## Use local model

<br><br>

### Ollama


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


<br><br>

3. Tunneling your ollama rest api to cloud with ngrok
- https://github.com/ollama/ollama/blob/main/docs/faq.id opidmd#how-can-i-use-ollama-with-ngrok
```shell
ngrok http 11434 --host-header="localhost:11434"
```



<br><br>

4. Open Cursor > Cursor Settings > Models
  3.1 Disable all other models and add new model which has the same name as your hosted llm in ollama in my case `deepseek-v2-coder-lite`
  3.2 At section OpenAI API Key add your base url `https://xxxxxxxxxxxxx.ngrok-free.app/v1`. Add any random API Key (Or maybe add valid OpenAI Key but do not think this is necessary) And then click verify button
   - If you get 403 then something is not working with CORS.

<br><br>

5. Enjoy <3

# Cursor Cheat Sheet


# Install
```shell
sudo chmod +x ./cursor-0.45.11x86_64.AppImage
./cursor-0.45.11x86_64.AppImage --appimage-extract

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


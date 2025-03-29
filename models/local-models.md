# Use Local Models

## Open Threads
- https://github.com/getcursor/cursor/issues/1380#issuecomment-2717102371

<br><br>

## Third party
- https://github.com/kcolemangt/llm-router

<br><br>

## Ollama Integration

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

2. Run your desired model by using ollama
- https://github.com/CyberT33N/ollama-cheat-sheet/blob/main/README.md#import-from-gguf
```shell
ollama run deepseek-v2-coder-lite
```

3. Start custom proxy layer to enhance security with ngrok
- https://github.com/CyberT33N/proxy-auth
- Make sure to define a bearer token in the .env file. The value of this will be the API key which you enter in cursor later..
- Related to point 5. there is a verify button in cursor which will send a OPTIONS method request without baerer token. In the project is a condition for this commented out. You can enable it to 1x time allow the request that cursor is happy and then you can commit it out again and restart. This only has to be done once..

4. Tunneling proxy layer from above which will send request to ollama rest api on your machine
- https://github.com/ollama/ollama/blob/main/docs/faq.id opidmd#how-can-i-use-ollama-with-ngrok
```shell
ngrok http 3000 --host-header="localhost:3000"
```

5. Open Cursor > Cursor Settings > Models
  3.1 Disable all other models and add new model which has the same name as your hosted llm in ollama in my case `deepseek-v2-coder-lite`
  3.2 At section OpenAI API Key add your base url `https://xxxxxxxxxxxxx.ngrok-free.app/v1`. At the API Key add your custom bearer token value from point 3 (**Just the value not the word Bearer**). And then click verify button
   - If you get 403 then something is not working with CORS.

6. Enjoy <3 

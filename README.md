# Cursor Cheat Sheet



# Models

<br><br>

## Use local model

<br><br>

### Ollama

1. Run your desired model by using ollama
- https://github.com/CyberT33N/ollama-cheat-sheet/blob/main/README.md#import-from-gguf

<br><br>

2. Tunneling your localhost llm rest api to cloud with ngrok
- https://github.com/ollama/ollama/blob/main/docs/faq.id opidmd#how-can-i-use-ollama-with-ngrok
```shell
ngrok http 11434 --host-header="localhost:11434"
```

<br><br>

3. Open Cursor > Cursor Settings > Models
  3.1 Disable all other models and add new model which has the same name as your hosted llm in ollama in my case
  3.2. At section OpenAI API Key add your base url `https://xxxxxxxxxxxxx.ngrok-free.app/v1`. And then click verify

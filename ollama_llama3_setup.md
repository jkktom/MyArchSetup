# Ollama and Llama 3 Setup Guide

## Installation History

### Installing Ollama
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

Installation output:
```
>>> Cleaning up old version at /usr/local/lib/ollama
>>> Installing ollama to /usr/local
>>> Downloading Linux amd64 bundle
######################################################################## 100.0%
>>> Adding ollama user to render group...
>>> Adding ollama user to video group...
>>> Adding current user to ollama group...
>>> Creating ollama systemd service...
>>> Enabling and starting ollama service...
>>> Downloading Linux ROCm amd64 bundle
######################################################################## 100.0%
>>> The Ollama API is now available at 127.0.0.1:11434.
>>> Install complete. Run "ollama" from the command line.
>>> AMD GPU ready.
```

### Pulling Llama 3.3 Model
```bash
ollama pull llama3
```

Pull output:
```
pulling manifest 
pulling 6a0746a1ec1a... 100% ▕███████████████████████████▏ 4.7 GB                         
pulling 4fa551d4f938... 100% ▕███████████████████████████▏  12 KB                         
pulling 8ab4849b038c... 100% ▕███████████████████████████▏  254 B                         
pulling 577073ffcc6c... 100% ▕███████████████████████████▏  110 B                         
pulling 3f8eb4da87fa... 100% ▕███████████████████████████▏  485 B                         
verifying sha256 digest 
writing manifest 
success
```

## Using Llama 3

### Basic Usage
Run a single prompt:
```bash
ollama run llama3 "Your prompt here"
```

Example:
```bash
ollama run llama3 "What can you do?"
```

### Interactive Chat Session
Start an interactive chat:
```bash
ollama run llama3
```

### Other Available Models
List all available models:
```bash
ollama list
```

Pull other models:
```bash
ollama pull mistral
ollama pull llama3:8b    # 8B parameter version
ollama pull llama3:70b   # 70B parameter version (requires more RAM)
```

## Important Information

- The Ollama API is available at 127.0.0.1:11434
- Models are stored in ~/.ollama/models
- Ollama runs as a service with systemd

To check service status:
```bash
systemctl status ollama
```

To restart the service:
```bash
sudo systemctl restart ollama
```

## Resources

- Official website: [https://ollama.com/](https://ollama.com/)
- GitHub repository: [https://github.com/ollama/ollama](https://github.com/ollama/ollama)
- Model library: [https://ollama.com/library](https://ollama.com/library) 
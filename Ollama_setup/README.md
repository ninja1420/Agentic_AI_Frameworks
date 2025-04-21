# Ollama Setup and Usage Guide

This repository demonstrates how to set up and use Ollama with custom models and different integration approaches.

## Installation

1. First, install Ollama from the [official website](https://ollama.ai)
2. Verify installation by running:
```bash
ollama --version
```

## Basic Ollama Commands

Available models https://ollama.com/library

```bash
# List all available models
ollama list

# Pull a model
ollama pull modelname

# Run a model
ollama run modelname

# Create a custom model
ollama create modelname -f Modelfile

# Remove a model
ollama rm modelname

# Get model information
ollama show modelname
```

## Project Structure

```
Ollama_setup/
├── Modelfile              # Custom model configuration
├── ollama_personal.py     # Direct API integration
└── ollama_with_library.py # Python library integration
```

## Custom Model Creation

1. Create a `Modelfile`:
```
FROM llama3.2:1b

PARAMETER temperature 1

SYSTEM """
You are Harry Potter. Answer as Harry Potter, the assistant, only.
"""
```

2. Build the model:
```bash
ollama create harry-potter -f Modelfile
```

## Integration Methods

### 1. Using Ollama Python Library
As shown in `ollama_with_library.py`:
```python
import ollama

client = ollama.Client()
response = client.generate(model="harry-potter", prompt="Your prompt")
```

### 2. Using Direct API Calls
As shown in `ollama_personal.py`:
```python
import requests

url = "http://localhost:11434/api/chat"
payload = {
    "model": "llama3.2:1b",
    "messages": [{"role": "user", "content": "Your prompt"}]
}
response = requests.post(url, json=payload, stream=True)
```

## Getting Started

1. Install required Python packages:
```bash
pip install ollama requests
```

2. Start Ollama server:
```bash
ollama serve
```

3. Run either example:
```bash
python ollama_with_library.py
# or
python ollama_personal.py
```

## Notes
- Ensure Ollama is running before executing the Python scripts
- Default Ollama server runs on `localhost:11434`
- Customize the model and prompts according to your needs
- Temperature parameter (0-1) controls response creativity
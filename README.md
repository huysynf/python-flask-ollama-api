# ollama-api

How to launch your own Private ChatGPT with API access using Ollama and Llama3.2 and FastAPI(Python)



## Installation

Follow next steps in order to install Ollama with llama3.2 on Ubuntu Server

### Install Ollama on Ubuntu

#### Step 1 - Update Ubuntu server

```sh
sudo apt update
```

```sh
sudo apt upgrade
```

```sh
apt install python3.12-venv
```

#### Step 1 - Install Ollama service

Install Ollama
```sh
curl -fsSL https://ollama.com/install.sh | sh
```

Pull llama3.2 LLM. You can [checkout here](https://github.com/ollama/ollama?tab=readme-ov-file#model-library) full list of LLM's

```sh
ollama run llama3.2
```

Check that Ollama is working

```sh
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt":"Who are you?"
}'
```

#### Step 2 - Install Ollama API 

Download Ollama API files

```sh
git clone https://github.com/saasscaleup/ollama-api.git
```

```sh
cd ollama-api
```

Install required packages.

```sh
python3 -m venv venv
```

```sh
source venv/bin/activate  # On Windows, use: venv\Scripts\activate
```

```sh
pip install fastapi uvicorn requests httpx
```

Run ollama-api app


```sh
uvicorn main:app --host 0.0.0.0 --port 3000
```

## API requests example


| Endpoint                   | `curl` Command                                                                                               | Description                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------|----------------------------------|
| `/generate` (streaming)    | ``` curl -N -X POST http://localhost:3000/api/generate -H "Content-Type: application/json" -d '{ "model": "llama3.2", "prompt": "What is your name?" }' ``` | Request streamed generation      |
| `/generate` (non-streaming)| ``` curl -X POST http://localhost:3000/api/generate -H "Content-Type: application/json" -d '{ "model": "llama3.2", "prompt": "What is your name?", "stream": false }' ``` | Request non-streamed generation  |
| `/models/download`         | ``` curl -X POST http://localhost:3000/api/models/download -H "Content-Type: application/json" -d '{ "llm_name": "llama3.2" }' ``` | Download specified model         |
| `/models`                  | ``` curl -X GET http://localhost:3000/api/models ```                                                          | List available models            |




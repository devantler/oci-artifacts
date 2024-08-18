# Ollama

An AI model serving platform to help you get up and running with Llama 3.1, Mistral, Gemma 2, and other large language models.

- [Docs](https://github.com/ollama/ollama/tree/main/docs)
- [Helm Chart](https://github.com/otwld/ollama-helm)

## Post-build variables

| Variable                   | Description                   | Default | Required |
| -------------------------- | ----------------------------- | ------- | -------- |
| ollama_ingress_enabled     | Enable ingress for Ollama     | true    | ✕        |
| ollama_persistence_enabled | Enable persistence for Ollama | false   | ✕        |
| ollama_memory_request      | Memory request for Ollama     | 4Gi     | ✕        |
| ollama_memory_limit        | Memory limit for Ollama       | 8Gi     | ✕        |
| ollama_cpu_request         | CPU request for Ollama        | 2       | ✕        |
| ollama_cpu_limit           | CPU limit for Ollama          | 4       | ✕        |

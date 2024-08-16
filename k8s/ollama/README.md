# Ollama

An AI model serving platform to help you get up and running with Llama 3.1, Mistral, Gemma 2, and other large language models.

- [Docs - Ollama](https://github.com/ollama/ollama/tree/main/docs)
- [Docs - Open WebUI](https://docs.openwebui.com)
- [Helm Chart - Ollama](https://github.com/otwld/ollama-helm)
- [Helm Chart - Open WebUI](https://github.com/open-webui/helm-charts)

## Post-build variables

| Variable                           | Description                      | Default | Required |
| ---------------------------------- | -------------------------------- | ------- | -------- |
| ollama_ingress_enabled             | Enable ingress for Ollama        | true    | ✕        |
| ollama_persistence_enabled         | Enable persistence for Ollama    | false   | ✕        |
| ollama_open_web_ui_ingress_enabled | Enable ingress for Ollama web UI | true    | ✕        |

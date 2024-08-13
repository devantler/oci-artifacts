# K8sGPT Operator

A Kubernetes operator to enable SRE superpowers within a Kubernetes cluster. It allows creating custom resources to define the behaviour and scope of a managed K8sGPT workload. Analysis and outputs will also be configurable to enable integration into existing workflows.

## Usage

1. Install the operator
2. Create and apply a K8sGPT custom resource

```yaml
apiVersion: core.k8sgpt.ai/v1alpha1
kind: K8sGPT
metadata:
  name: k8sgpt-sample
  namespace: k8sgpt-operator-system
spec:
  ai:
    enabled: true
    model: gpt-3.5-turbo
    backend: openai
    secret:
      name: k8sgpt-sample-secret
      key: openai-api-key
    # anonymized: false
    # language: english
  noCache: false
  repository: ghcr.io/k8sgpt-ai/k8sgpt
  version: v0.3.8
  #integrations:
  # trivy:
  #  enabled: true
  #  namespace: trivy-system
  # filters:
  #   - Ingress
  # sink:
  #   type: slack
  #   webhook: <webhook-url> # use the sink secret if you want to keep your webhook url private
  #   secret:
  #     name: slack-webhook
  #     key: url
  #extraOptions:
  #   backstage:
  #     enabled: true
```

> [!INFO]
> You might need to add a secret to contain your API Key for the chosen AI backend.

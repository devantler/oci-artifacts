# Welcome to Devantler's OCI Artifacts 🚀

> [!WARN]
> This repo will soon be deprecated. It became a big maintenance overhead, when I only use the artifacts in my [homelab](https://github.com/devantler/homelab). Furthermore I have learned this is not such a great approach, as it is to dependent on tooling (FluxCD). If someone else thinks of this, I would suggest to do it with either Helm Umbrella Charts or Timoni. These solutions will provide much better templating, and be more open for consumption. Both solutions could still be distributed as OCI artifacts.


<details>
  <summary>Show/hide folder structure</summary>

<!-- readme-tree start -->
```
.
├── .github
│   └── workflows
├── .vscode
└── k8s
    ├── capi-operator
    ├── cert-manager
    │   └── cluster-issuers
    │       ├── cloudflare-letsencrypt
    │       └── selfsigned
    ├── cloudflared
    ├── clusters
    │   └── oci-artifacts
    │       ├── flux-system
    │       ├── releases
    │       │   ├── capi-operator
    │       │   ├── cert-manager
    │       │   ├── cloudflared
    │       │   ├── gha-runner-scale-set-controller
    │       │   ├── goldilocks
    │       │   ├── harbor
    │       │   ├── helm-charts-oci-proxy
    │       │   ├── homepage
    │       │   ├── k8sgpt-operator
    │       │   ├── kyverno
    │       │   ├── metrics-server
    │       │   ├── oauth2-proxy
    │       │   ├── ollama
    │       │   ├── open-webui
    │       │   ├── plantuml
    │       │   ├── pulumi-operator
    │       │   ├── reloader
    │       │   ├── traefik
    │       │   └── trivy-operator
    │       └── variables
    ├── gha-runner-scale-set-controller
    ├── goldilocks
    ├── harbor
    ├── helm-charts-oci-proxy
    ├── homepage
    ├── k8sgpt-operator
    ├── kubelet-serving-cert-approver
    ├── kyverno
    ├── longhorn
    ├── metrics-server
    ├── oauth2-proxy
    ├── ollama
    ├── open-webui
    ├── plantuml
    ├── pulumi-operator
    │   └── programs
    │       └── harbor-proxy-program
    ├── reloader
    ├── traefik
    │   └── middlewares
    │       ├── basic-auth
    │       └── forward-auth
    └── trivy-operator

57 directories
```
<!-- readme-tree end -->

</details>

OCI Artifacts are a great way to distribute ready-to-use K8s manifests. It requires almost no lines of code to get services deployed, and together with Flux and Flux post-build variables it can be a great addition to Helm charts. In most cases deploying a service, will require a single line + setting some post-build variables. In more advanced scenarios it might require patching the OCI Artifact with Kustomize patches.

This repository contains the following OCI Artifacts:

- [Cluster API Operator](k8s/capi-operator/README.md)
- [Cert Manager](k8s/cert-manager/README.md)
  - [Cluster Issuer - Cloudflare LetsEncrypt](k8s/cert-manager/cluster-issuers/cloudflare-letsencrypt/README.md)
  - [Cluster Issuer - Self-Signed](k8s/cert-manager/cluster-issuers/selfsigned/README.md)
- [Cloudflared](k8s/cloudflared/README.md)
- [GitHub Actions Runner Scale Set](k8s/gha-runner-scale-set/README.md)
- [Goldilocks](k8s/goldilocks/README.md)
- [Harbor](k8s/harbor/README.md)
- [Helm Charts OCI Proxy](k8s/helm-charts-oci-proxy/README.md)
- [Homepage](k8s/homepage/README.md)
- [K8sGPT Operator](k8s/k8sgpt-operator/README.md)
- [Kubelet Serving Cert Approver](k8s/kubelet-serving-cert-approver/README.md)
- [Kyverno](k8s/kyverno/README.md)
- [Longhorn](k8s/longhorn/README.md)
- [Metrics Server](k8s/metrics-server/README.md)
- [OAuth2 Proxy](k8s/oauth2-proxy/README.md)
- [Ollama](k8s/ollama/README.md)
- [PlantUML](k8s/plantuml/README.md)
- [Pulumi Operator](k8s/pulumi-operator/README.md)
  - [Program - Harbor Proxy Program](k8s/pulumi-operator/programs/harbor-proxy-program/README.md)
- [Reloader](k8s/reloader/README.md)
- [Traefik](k8s/traefik/README.md)
  - [Middleware - Basic Auth](k8s/traefik/middlewares/basic-auth/README.md)
  - [Middleware - Forward Auth](k8s/traefik/middlewares/forward-auth/README.md)
- [Trivy Operator](k8s/trivy-operator/README.md)

## Requirements

For testing locally:

- [KSail](https://github.com/devantler/ksail)
- [Docker](https://www.docker.com/)
- Linux or MacOS

For deploying the OCI Artifacts to a Kubernetes cluster:

- A running Kubernetes cluster
- Flux GitOps installed in the cluster

## Usage

### Deploying an OCI Artifact with Flux Kustomization (Recommended)

First you have to create an `OCIRepository` to be able to deploy OCI Artifacts.

```yaml
apiVersion: source.toolkit.fluxcd.io/v1beta2
kind: OCIRepository
metadata:
  name: oci-artifacts
  namespace: flux-system
spec:
  interval: 1m0s
  url: oci://ghcr.io/devantler/oci-artifacts/manifests
  ref:
    tag: latest
```

Applying this resource to your cluster will enable you to reference and deploy OCI Artifacts with Flux Kustomizations:

```yaml
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: traefik
  namespace: flux-system
spec:
  interval: 1m
  targetNamespace: traefik
  sourceRef:
    kind: OCIRepository
    name: oci-artifacts
  path: traefik
  prune: true
  wait: true
  # If the OCI Artifact requires setting post-build variables,
  # you might need decryption and substitutes configured.
  decryption:
    provider: sops
    secretRef:
      name: sops-age
  postBuild:
    substituteFrom:
      - kind: ConfigMap
        name: variables
      - kind: Secret
        name: variables-sensitive
  # If you further want to customize the deployment,
  # you can freely change it up with regular Kustomize patches.
  patches:
    - target:
        kind: HelmRelease
        name: traefik
      patch: |-
        apiVersion: helm.toolkit.fluxcd.io/v2
        kind: HelmRelease
        metadata:
          name: traefik
        spec:
          values:
            ports:
              websecure:
                middlewares:
                  - traefik-traefik-auth-headers@kubernetescrd
            ingressRoute:
              dashboard:
                middlewares:
                  - name: traefik-forward-auth
                    namespace: traefik
```

For a real life example, take a look at my [homelab](https://github.com/devantler/homelab).

### Deploying an OCI Artifact with Kustomize

> [!NOTE]
> Pulling K8s manifest over OCI is not supported by Kustomize yet. There is [an active Pull Request](https://github.com/kubernetes-sigs/kustomize/pull/5147) that will add support for this.

### Setting variables for OCI Artifacts

Some of the OCI Artifacts require you to provide some variables to configure the service. You can do this by adding the variables to your variables files in the `k8s/clusters/[clusterName]/variables` folder in your own clusters repo. You can find the variables in the `k8s/<oci-artifact>/README.md` files in this repository.

## Contributing

The OCI Artifacts repo is open source, and I welcome contributions from anyone. If you want to contribute, please create issues or pull requests in this repository and I will take a look at it.

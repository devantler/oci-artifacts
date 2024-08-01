# Welcome to Devantler's OCI Artifacts 🚀

<details>
  <summary>Show/Hide Folder Structure</summary>

<!-- readme-tree start -->

```
.
├── .github
│   └── workflows
├── .vscode
└── k8s
    ├── cert-manager
    │   └── cluster-issuers
    │       ├── cloudflare-letsencrypt
    │       └── selfsigned
    ├── cloudflared
    ├── clusters
    │   └── oci-artifacts
    │       ├── apps
    │       │   └── homepage
    │       ├── flux-system
    │       ├── releases
    │       │   ├── cert-manager
    │       │   ├── cloudflared
    │       │   ├── gha-runner-scale-set-controller
    │       │   ├── goldilocks
    │       │   ├── harbor
    │       │   ├── helm-charts-oci-proxy
    │       │   ├── homepage
    │       │   ├── metrics-server
    │       │   ├── oauth2-proxy
    │       │   ├── plantuml
    │       │   ├── pulumi-operator
    │       │   ├── reloader
    │       │   └── traefik
    │       └── variables
    ├── gha-runner-scale-set-controller
    ├── goldilocks
    ├── harbor
    ├── helm-charts-oci-proxy
    ├── homepage
    ├── kubelet-serving-cert-approver
    ├── longhorn
    ├── metrics-server
    ├── oauth2-proxy
    ├── plantuml
    ├── pulumi-operator
    │   └── programs
    │       └── harbor-program
    ├── reloader
    └── traefik
        └── middlewares
            └── forward-auth

46 directories
```

<!-- readme-tree end -->

</details>

OCI Artifacts is a collection of pre-configured K8s manifests that can be deployed to a Kubernetes cluster in a GitOps-friendly manner. The manifests are distributed through OCI andrely on FluxCD and Kustomize.

---
Where Helm Charts primarily packages applications with a focus on flexibility, configurability and being unopinionated, OCI Artifacts provide simple and opinionated configurations on top of e.g. Helm Charts, with a focus on implementing best practices with sane defaults.

This makes it easier to get started with deploying services to a Kubernetes cluster, and saves you from spending valuable time digging through the documentation and issues for each service you want to deploy.

So this is for you if you are looking for a simple GitOps-friendly way to deploy popular services that are configured as intended by the maintainers.

Below is a list of the available OCI Artifacts and their stage of development:

- [Traefik](k8s/stable/traefik/README.md) ![Stable](https://img.shields.io/badge/Stable-blue)
  - Middlewares
    - [Basic Auth](k8s/stable/traefik/middlewares/basic-auth/README.md)
    - [Forward Auth](k8s/stable/traefik/middlewares/forward-auth/README.md)
- [Cert Manager](k8s/beta/cert-manager/README.md) ![Beta](https://img.shields.io/badge/Beta-yellow)
- [Cloudflared](k8s/beta/cloudflared/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [GitHub Actions Runner Scale Set](k8s/gha-runner-scale-set/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Goldilocks](k8s/beta/goldilocks/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Harbor](k8s/beta/harbor/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Helm Charts OCI Proxy](k8s/beta/helm-charts-oci-proxy/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Homepage](k8s/beta/homepage/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Kubelet Serving Cert Approver](k8s/beta/kubelet-serving-cert-approver/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Longhorn](k8s/beta/longhorn/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Metrics Server](k8s/beta/metrics-server/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [OAuth2 Proxy](k8s/beta/oauth2-proxy/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [PlantUML](k8s/beta/plantuml/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Pulumi Operator](k8s/beta/pulumi-operator/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)
- [Reloader](k8s/beta/reloader/README.md) ![Alpha](https://img.shields.io/badge/Alpha-orange)

The stages of development are defined as follows:

![Stable](https://img.shields.io/badge/Stable-blue) - Expected to work, with sane defaults and best practices implemented.

![Beta](https://img.shields.io/badge/Beta-yellow) - Expected to work, but without sane defaults and best practices fully implemented.

![Alpha](https://img.shields.io/badge/Alpha-orange) - New and experimental, with no guarantees of working as intended. Primarily used as a sandbox for testing and learning new services.

> [!NOTE]
> The stages of development is a metric of stability and not a metric of feature completeness. Stable services are still under active development and might not have all features implemented, but for those that are implemented, they are expected to work as intended. For example, the Traefik service is stable, but it does not provide OCI Artifacts for all of its Middlewares yet.

## Prerequisites

For testing locally:

- [KSail](https://github.com/devantler/ksail)
- [Docker](https://www.docker.com/)
- Linux or MacOS

For deploying the OCI Artifacts to a Kubernetes cluster:

- A running Kubernetes cluster
- Flux GitOps installed in the cluster

## Usage

OCI Artifacts assumes the use of [FluxCD Post-build variables](https://fluxcd.io/flux/components/kustomize/kustomizations/#post-build-variable-substitution) for setting most configurations. This is a design choice as it is a very non-verbose way to configure services. However, it is not perfect, and in some cases, you might need to configure the services in other ways, for example by creating resources, or by using Kustomize patches.

> [!NOTE]
> The current approach works well (assuming you are using FluxCD as your primary deployment tool), but it is not perfect. I am open to suggestions on how to improve this, and I am actively looking for a more standardized way to deploy and configure services independently of the deployment tool used.

### Setting Common Post-build Variables

Most of the OCI Artifacts provide configurations that affect multiple services. These configurations should be set as post-build variables for your cluster. You can set these variables in a ConfigMap and a Secret (depending on the sensitivity of the data).

Below is a list of common post-build variables that you should set for your cluster:

| Variable                  | Description                                                   |              Default              | Required |
| ------------------------- | ------------------------------------------------------------- | :-------------------------------: | :------: |
| cluster_domain            | The domain of the cluster (will be `<service-name>.<domain>`) |                ""                 |    ✓     |
| helm_repository_proxy_url | The URL of the Helm repository proxy                          | chartproxy.container-registry.com |    ✕     |

### Deploying an OCI Artifact

There are two ways to deploy an OCI Artifact, either with Flux Kustomizations or with Kustomize. The currently recommended way is to use Flux Kustomizations, as these provide powerful features to enhance the deployment process.

#### Deploying with Flux Kustomizations (Recommended)

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

#### Deploying With Kustomize

> [!WARNING]
> Pulling K8s manifest over OCI is not supported by Kustomize yet. There is [an active Pull Request](https://github.com/kubernetes-sigs/kustomize/pull/5147) that will add support for this.

## Contributing

The OCI Artifacts repo is open source, and I welcome contributions from anyone. If you want to contribute, please create issues or pull requests in this repository and I will take a look at it.

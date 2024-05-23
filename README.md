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
    │   ├── certificates
    │   ├── cluster-issuers
    │   └── secrets
    ├── cloudflared
    ├── clusters
    │   └── oci-artifacts
    │       ├── crds
    │       ├── flux-system
    │       ├── infrastructure
    │       │   └── configmaps
    │       └── variables
    ├── crossplane
    ├── dex
    ├── gha-runner-scale-set
    ├── goldilocks
    ├── harbor
    ├── helm-charts-oci-proxy
    ├── homepage
    ├── kubelet-serving-cert-approver
    ├── longhorn
    ├── metrics-server
    ├── oauth2-proxy
    ├── openebs
    ├── pulumi-operator
    ├── rook-ceph
    └── traefik

31 directories
```
<!-- readme-tree end -->

</details>

This repository contains Kubernetes (K8s) manifests distributed as OCI Artifacts.

- [Cert Manager](k8s/cert-manager/README.md)
- [Cloudflared](k8s/cloudflared/README.md)
- [Crossplane](k8s/crossplane/README.md)
- [Dex](k8s/dex/README.md)
- [GitHub Actions Runner Scale Set](k8s/gha-runner-scale-set/README.md)
- [Goldilocks](k8s/goldilocks/README.md)
- [Harbor](k8s/harbor/README.md)
- [Helm Charts OCI Proxy](k8s/helm-charts-oci-proxy/README.md)
- [Homepage](k8s/homepage/README.md)
- [Kubelet Serving Cert Approver](k8s/kubelet-serving-cert-approver/README.md)
- [Metrics Server](k8s/metrics-server/README.md)
- [MinIO](k8s/minio/README.md)
- [OAuth2 Proxy](k8s/oauth2-proxy/README.md)
- [Pulumi Operator](k8s/pulumi-operator/README.md)
- [Rook-Ceph](k8s/rook-ceph/README.md)
- [Traefik](k8s/traefik/README.md)

OCI Artifacts are a great way to distribute ready-to-use K8s manifests. It requires almost no lines of code to get services deployed, and together with Flux and Flux post-build variables it can be a great addition to Helm charts. In most cases deploying a service, will require a single line + setting some post-build variables. In more advanced scenarios it might require patching the OCI Artifact with Kustomize patches.

## Requirements

For testing locally:

- [KSail](https://github.com/devantler/ksail)
- [Docker](https://www.docker.com/)
- Linux or MacOS

For deploying the OCI Artifacts to a Kubernetes cluster:

- A running Kubernetes cluster
- Flux GitOps installed in the cluster

## Usage

### Reference an OCI Artifact with Kustomize

> [!NOTE]
> Pulling K8s manifest over OCI is not supported by Kustomize yet. There is [an active Pull Request](https://github.com/kubernetes-sigs/kustomize/pull/5147) that will add support for this. Until then, we can use Git over HTTP to reference the OCI Artifact.

To reference an OCI Artifact with Kustomize, you need to add the following to your `kustomization.yaml` files that you want to reference the OCI Artifact and its configurations from:

```yaml
# Deploying folders
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
  # To reference a folder you use the following syntax:
  - https://github.com/devantler/oci-artifacts//k8s/[serviceName]?ref=[refName]

---
# Deploying single files
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
  # To reference a single file you use the following syntax:
  - https://raw.githubusercontent.com/devantler/oci-artifacts/[refName]/k8s/[serviceName]/[pathToYamlFile]
```

Where `[serviceName]` is the name of the OCI Artifact you want to reference, and `[refName]` is the name of the branch or tag you want to pull the OCI Artifact from. If you want to reference a single file, you also need to specify the [pathToYamlFile] which is the path to the yaml file relative to the OCI Artifact folder. For example `cert-manager/certificates/cluster-issuer-certificate.yaml`, if you want to pull the cluster issuer certificate provided by the cert-manager OCI Artifact

### Setting variables for OCI Artifacts

Some of the OCI Artifacts require you to provide some variables to configure the service. You can do this by adding the variables to your variables files in the `k8s/clusters/[clusterName]/variables` folder in your own clusters repo. As the references are http, you can fairly easily decode where to look for the possible variables. For example, if you want to reference the `traefik` service, you can find the variables in the `k8s/traefik/*.yaml` files in this repository.

### Patching OCI Artifacts

Some OCI Artifacts might not meet your expectations out-of-the-box. In this case, you can patch the OCI Artifact by adding patches to your `kustomization.yaml` file that references the OCI Artifact. For example, if you want to patch the `traefik` service, you would add the following to your `kustomization.yaml` file:

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
  # To reference a service you use the following syntax:
  - https://[token]@github.com/devantler/oci-artifacts//k8s/traefik?ref=v0.0.3

patches:
  # To patch a service with a patch file you use the following syntax:
  - path: traefik-patch.yaml
    target:
      kind: HelmRelease
      name: traefik
      namespace: traefik
  # To inline patch a service you use the following syntax:
  - patch: |-
      - op: replace
        path: /some/existing/path
        value: new value
    target:
      kind: HelmRelease
      name: traefik
      namespace: traefik
```

This allows you full control over the OCI Artifacts, but if you require a lot of patches, you might want to consider contributing to the OCI Artifact to make it more flexible, or copying the OCI Artifact into your own clusters repo and configure it there.

## Contributing

The OCI Artifacts repo is open source, and I welcome contributions from anyone. If you want to contribute, please create issues or pull requests in this repository and I will take a look at it.

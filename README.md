# Welcome to Devantler's OCI Registry 🚀

<details>
  <summary>Show/Hide Folder Structure</summary>

<!-- readme-tree start -->
```
.
├── .github
│   ├── scripts
│   └── workflows
├── .vscode
├── k8s
│   ├── apps
│   ├── clusters
│   │   └── docker
│   │       ├── .flux
│   │       ├── infrastructure
│   │       │   ├── configs
│   │       │   └── services
│   │       └── variables
│   └── infrastructure
│       ├── cert-manager
│       │   ├── certificates
│       │   └── cluster-issuers
│       ├── cloudflared
│       ├── flux-github-status-updater
│       ├── flux-webhook-receiver
│       │   ├── ingress-routes
│       │   └── secrets
│       ├── gha-runner-scale-set
│       ├── gha-runner-scale-set-controller
│       ├── harbor
│       ├── kube-prometheus-stack
│       ├── kubelet-serving-cert-approver
│       ├── local-storage
│       ├── metrics-server
│       ├── openebs
│       ├── pulumi-operator
│       │   └── programs
│       ├── redis
│       ├── reloader
│       ├── strapi
│       ├── testkube
│       ├── traefik
│       └── vertical-pod-autoscaler
├── pulumi
├── scripts
└── talos
    ├── cluster
    ├── controlplane
    └── worker

44 directories
```
<!-- readme-tree end -->

</details>

This is an [OCI registry](https://opencontainers.org) with various different components for building and managing kubernetes clusters. It uses [kustomize bases](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/#bases-and-overlays) for services and provides templating with [flux post-build variables](https://fluxcd.io/flux/components/kustomize/kustomizations/#post-build-variable-substitution), or full control with [kustomize patches](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/#customizing). As such, it provides a simple way to deploy services without the overhead of [Helm charts](https://helm.sh/docs/topics/charts/), and the complexity of writing your own Kubernetes manifests. However, it comes with the tradeoff of being less flexible than the helm charts in its templated setup, and as such it might not be suitable for all use cases in its current state. Feel free to open an issue or a PR if you require more helm values to be exposed, or if you have any other suggestions.

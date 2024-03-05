# Cert Manager

Cert Manager is a Kubernetes add-on to automate the management and issuance of TLS certificates from various issuing sources.

- [Documentation](https://cert-manager.io/docs/)
- [Helm Chart](https://github.com/cert-manager/cert-manager/tree/master/deploy/charts/cert-manager)

## Post-build variables

This OCI Artifact currently has no post-build variables to configure.

## CRDs

This OCI Artifact provides CRDs. They must be deployed separately.

### Cluster Issuers

#### Self-Signed Cluster Issuer

- `k8s/cert-manager/cluster-issuers/self-signed-cluster-issuer.yaml`

This cluster issuer can be used to issue self-signed certificates. It is only recommended to use this issuer for local and dev clusters.

### Cluster Issuer Certificate

- `k8s/cert-manager/certificates/cluster-issuer-certificate.yaml`

This certificate is used to issue certificates for any cluster issuer. It must be configured with the correct issuer.

| Variable            | Description                    | Default | Required |
| ------------------- | ------------------------------ | :-----: | :------: |
| cluster_domain      | The domain of the cluster      |         |    ✓     |
| cluster_issuer_name | The name of the cluster issuer |         |    ✓     |

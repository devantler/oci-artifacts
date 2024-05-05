# Cert Manager

Cert Manager is a Kubernetes add-on to automate the management and issuance of TLS certificates from various issuing sources.

- [Documentation](https://cert-manager.io/docs/)
- [Helm Chart](https://github.com/cert-manager/cert-manager/tree/master/deploy/charts/cert-manager)

## Post-build variables

This OCI Artifact currently has no post-build variables to configure.

## CRDs

This OCI Artifact provides CRDs. They must be deployed separately.

### Cluster Issuers

### Cluster Issuer Certificate

- `k8s/cert-manager/certificates/cluster-issuer-certificate.yaml`

This certificate is used to issue certificates for any cluster issuer. It must be configured with the correct issuer.

| Variable            | Description                    | Default | Required |
| ------------------- | ------------------------------ | :-----: | :------: |
| cluster_domain      | The domain of the cluster      |         |    ✓     |
| cluster_issuer_name | The name of the cluster issuer |         |    ✓     |

#### Self-Signed Cluster Issuer

- `k8s/cert-manager/cluster-issuers/self-signed-cluster-issuer.yaml`

This cluster issuer can be used to issue self-signed certificates. It is only recommended to use this issuer for local clusters.

#### Cloudflare LetsEncrypt Cluster Issuer

- `k8s/cert-manager/cluster-issuers/cloudflare-letsencrypt-cluster-issuer.yaml`

This cluster issuer can be used to issue certificates using the Cloudflare DNS API. It is recommended to use this issuer for dev/test and production clusters.

| Variable                                     | Description                                           |                         Default                          | Required |
| -------------------------------------------- | ----------------------------------------------------- | :------------------------------------------------------: | :------: |
| cloudflare_letsencrypt_cluster_issuer_server | The cluster issuer server to use for letsencrypt ACME | <https://acme-staging-v02.api.letsencrypt.org/directory> |    ✕     |
| cloudflare_letsencrypt_cluster_issuer_email  | The email to use when issuing new certificates issuer |                                                          |    ✓     |

For this issuer to work, you must also add the `k8s/cert-manager/certificates/cloudflare-dns-api-key.yaml` secret to your cert-manager namespace.

| Variable               | Description                                | Default | Required |
| ---------------------- | ------------------------------------------ | :-----: | :------: |
| cloudflare_dns_api_key | The API Key needed for ACME DNS challenges |         |    ✓     |

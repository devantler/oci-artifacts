# Cert Manager

Cert Manager is a Kubernetes add-on to automate the management and issuance of TLS certificates from various issuing sources.

- [Documentation](https://cert-manager.io/docs/)
- [Helm Chart](https://github.com/cert-manager/cert-manager/tree/master/deploy/charts/cert-manager)

## Post-build variables

| Variable       | Description               | Default | Required |
| -------------- | ------------------------- | :-----: | :------: |
| cluster_domain | The domain of the cluster |         |    ✓     |

## Custom Resources

- [Cluster Issuer - Self-Signed](cluster-issuers/selfsigned/README.md)
- [Cluster Issuer - Cloudflare LetsEncrypt](cluster-issuers/cloudflare-letsencrypt/README.md)

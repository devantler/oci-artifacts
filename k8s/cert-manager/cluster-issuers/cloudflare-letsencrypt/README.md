# Cert Manager - Cloudflare LetsEncrypt Cluster Issuer

This cluster issuer can be used to issue certificates using the Cloudflare DNS API. It is recommended to use this issuer for dev/test and production clusters.

## Dependencies

- [Cert Manager](../../README.md)

## Post-build variables

| Variable                                     | Description                                           |                         Default                          | Required |
| -------------------------------------------- | ----------------------------------------------------- | :------------------------------------------------------: | :------: |
| cloudflare_letsencrypt_cluster_issuer_server | The cluster issuer server to use for letsencrypt ACME | <https://acme-staging-v02.api.letsencrypt.org/directory> |    ✕     |
| cloudflare_letsencrypt_cluster_issuer_email  | The email to use when issuing new certificates issuer |                                                          |    ✓     |

For this issuer to work, you must also add the `k8s/cert-manager/certificates/cloudflare-dns-api-key.yaml` secret to your cert-manager namespace.

| Variable               | Description                                | Default | Required |
| ---------------------- | ------------------------------------------ | :-----: | :------: |
| cloudflare_dns_api_key | The API Key needed for ACME DNS challenges |         |    ✓     |

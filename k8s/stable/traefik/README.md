# Traefik

Traefik is a reverse proxy and load balancer that routes incoming requests to the correct backend service. It is used as an ingress controller in Kubernetes clusters.

- [Documentation](https://doc.traefik.io/traefik/)
- [Helm Chart](https://github.com/traefik/traefik-helm-chart)

## Prerequisites

- [Cert Manager](../../cert-manager/README.md) with a Cluster Issuer

## Usage

1. Deploy the Traefik OCI Artifact as instructed in [README > Usage](../../../README.md#deploying-an-oci-artifact), where its path is `stable/traefik`.
2. Set the following post-build variables (if necessary):
   | Variable | Description | Default | Required |
   | -------------------------------- | ----------------------------------------------------------------- | :-------: | :------: |
   | traefik_ingress_load_balancer_ip | The IP address of the load balancer | "" | ✕ |
   | traefik_service_type | The service to provide ingressing for (LoadBalancer or ClusterIP) | ClusterIP | ✕ |
3. Consider deploying Traefik Custom Resources (CRs):
   - Middlewares
     - [Basic Auth](middlewares/basic-auth/README.md)
     - [Forward Auth](middlewares/forward-auth/README.md)
4. Voilà! You have successfully deployed Traefik in your Kubernetes cluster, and you can now use it to create ingress or gateway routes to your services, with the ability to use middlewares to enhance routing capabilities.

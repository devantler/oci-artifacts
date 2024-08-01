# Traefik Forward Auth Middleware

This middleware adds forward authentication to a service.

- [Documentation](https://doc.traefik.io/traefik/middlewares/http/forwardauth/)

## Prerequisites

- [Traefik](./../README.md)

## Usage

1. Deploy the Traefik Forward Auth Middleware as instructed in [README > Usage](../../../../../README.md#usage), where its path is `stable/traefik/middlewares/forward-auth`.
   | Variable | Description | Default | Required |
   | ------------------------- | ------------------------------------------------------------ | :-----: | :------: |
   | traefik_forward_auth_address | The address of the forward authentication service | "" | ✓ |
   | traefik_forward_auth_tls_insecure_skip_verify | Skip verification of the certificate chain and host name | false | ✕ |
2. Add the middleware to your routes that need forward authentication.
3. Voilà! Your services are now protected by forward authentication.

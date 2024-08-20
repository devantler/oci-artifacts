# Traefik Middleware - Forward Auth

This middleware adds forward authentication to requests.

- [Documentation](https://doc.traefik.io/traefik/middlewares/http/forwardauth/)

## Dependencies

- [Traefik](../../README.md)

## Post-build variables

| Variable                                      | Description                                     | Default | Required |
| --------------------------------------------- | ----------------------------------------------- | :-----: | :------: |
| traefik_forward_auth_address                  | The address of the forward auth service         |   -    |    ✓     |
| traefik_forward_auth_ssl_host                 | The host of the forward auth service            |   -    |    ✓     |
| traefik_forward_auth_tls_insecure_skip_verify | Whether to skip verification of the certificate |  true   |    ✕     |

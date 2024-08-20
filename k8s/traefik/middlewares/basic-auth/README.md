# Traefik Middleware - Basic Auth

This middleware adds basic authentication to requests.

- [Documentation](https://doc.traefik.io/traefik/middlewares/http/basicauth/)

## Dependencies

- [Traefik](../../README.md)

## Post-build variables

| Variable                | Description                                    | Default | Required |
| ----------------------- | ---------------------------------------------- | :-----: | :------: |
| traefik_basic_auth_user | `htpasswd -nb user password \| openssl base64` |   -    |    ✓     |

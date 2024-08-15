# Programs - Harbor Proxy Program

This program is a Pulumi program and stack that configures a Harbor instance to be able to act as a pull-through cache and proxy for bothe docker images and Helm charts.

It proxies the following registries:

- `docker.io`
- `ghcr.io`
- `gcr.io`
- `registry.k8s.io`
- `quay.io`
- `mcr.microsoft.com`

To learn more about configuring the program and stack, visit the following:

- [Documentation](https://www.pulumi.com/registry/packages/harbor/)

## Dependencies

- [Pulumi Operator](../../README.md)
- [Harbor](../../../harbor/README.md)

## Post-build variables

| Variable                        | Description                                | Default                        | Required |
| ------------------------------- | ------------------------------------------ | ------------------------------ | -------- |
| harbor_docker_proxy_endpoint    | The endpoint of the Harbor Docker proxy    | <https://registry-1.docker.io> | ✕        |
| harbor_github_proxy_endpoint    | The endpoint of the Harbor GitHub proxy    | <https://ghcr.io>              | ✕        |
| harbor_google_proxy_endpoint    | The endpoint of the Harbor Google proxy    | <https://gcr.io>               | ✕        |
| harbor_k8s_proxy_endpoint       | The endpoint of the Harbor K8s proxy       | <https://registry.k8s.io>      | ✕        |
| harbor_quay_proxy_endpoint      | The endpoint of the Harbor Quay proxy      | <https://quay.io>              | ✕        |
| harbor_microsoft_proxy_endpoint | The endpoint of the Harbor Microsoft proxy | <https://mcr.microsoft.com>    | ✕        |
| pulumi_backend                  | The Pulumi backend to use                  | file:///pulumi-backend         | ✕        |
| harbor_url                      | The URL of the Harbor instance             | <http://harbor-core.harbor>    | ✕        |
| harbor_username                 | The username of the Harbor instance        | admin                          | ✕        |
| harbor_password                 | The password of the Harbor instance        | Harbor12345                    | ✕        |
| harbor_insecure                 | Whether to skip TLS verification           | false                          | ✕        |

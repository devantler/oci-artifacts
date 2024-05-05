# OAuth2 Proxy

A reverse proxy that provides authentication with OpenID Connect and many more identity providers.

- [Documentation](https://oauth2-proxy.github.io/oauth2-proxy/)
- [Helm Chart](https://github.com/oauth2-proxy/manifests)

## Post-build variables

| Variable                     | Description                                                    | Default | Required |
| ---------------------------- | -------------------------------------------------------------- | :-----: | :------: |
| cluster_domain               | The domain of the cluster                                      |   ""    |    ✓     |
| oauth2_proxy_ingress_enabled | Whether to enable an ingress route to the OAuth2 Proxy service |  true   |    ✕     |
| oauth2_proxy_client_id       | The OAuth2 client ID                                           |   ""    |    ✓     |
| oauth2_proxy_client_secret   | The OAuth2 client secret                                       |   ""    |    ✓     |
| oauth2_proxy_cookie_secret   | The secret used to encrypt the cookie                          |   ""    |    ✓     |
| oauth2_proxy_cookie_name     | The name of the cookie                                         |   ""    |    ✕     |

To further configure OAuth2 Proxy, you must create a ConfigMap with the desired configuration, and deploy it in the oauth2-proxy namespace with the name `oauth2-proxy-configmap`.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: oauth2-proxy-configmap
  namespace: oauth2-proxy
data:
  # https://oauth2-proxy.github.io/oauth2-proxy/configuration/overview
  oauth2_proxy.cfg: |-
    provider="github" # the OAuth2 provider to use
    email_domains = [ "*" ] # restrict logins to users with an email address in a specific domain
    github_org="my-org" # restrict logins to members of an organization
    github_team="my-team1,my-team2" # restrict logins to members of a team
    github_repo="my-repo" # restrict logins to collaborators in a repository (formatted as "owner/repo")
    github_user="my-user1,my-user2" # restrict logins to specific users
```

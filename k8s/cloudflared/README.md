# Cloudflared

Cloudflared is a tunneling daemon based on Wireguard that can proxy a local webserver through the Cloudflare network. It is used to make the local Kubernetes cluster available on the internet.

## Post-build variables

| Variable                 | Description                                 | Default | Required |
| ------------------------ | ------------------------------------------- | :-----: | :------: |
| cloudflared_tunnel_token | The token for an existing Cloudflare tunnel |   -    |    ✓     |

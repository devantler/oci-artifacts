# Chartproxy

Transparently proxy and transform Chart Repository styled Helm Charts as OCI artifacts. The service allows you to address any public Chart Repository styled Helm Chart as an OCI styled artifact.

- [Documentation](https://doc.traefik.io/traefik/)
- [Helm Chart](https://github.com/traefik/traefik-helm-chart)

## Post-build variables

| Variable                             | Description                                | Default                       | Required |
| ------------------------------------ | ------------------------------------------ | ----------------------------- | -------- |
| chartsproxy_image_registry | The OCI registry where the image is stored | 8gears.container-registry.com | ✕        |

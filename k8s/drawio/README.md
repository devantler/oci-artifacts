# Draw.io

A free, popular, and open source diagramming app.

- [Documentation](https://www.drawio.com/doc/)
- [Helm Chart](https://github.com/truecharts/charts/tree/master/charts/stable/drawio)

## Post-build variables

| Variable                 | Description                                               | Default | Required |
| ------------------------ | --------------------------------------------------------- | :-----: | :------: |
| cluster_domain           | The domain of the cluster                                 |   ""    |    ✓     |
| plantuml_ingress_enabled | Whether to enable an ingress route to the Draw.io service |  true   |    ✕     |

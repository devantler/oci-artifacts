# Harbor

Harbor is an open-source cloud native registry that stores, signs, and scans container images for vulnerabilities.

- [Documentation](https://goharbor.io/docs/)
- [Helm Chart](https://github.com/goharbor/harbor-helm)

## Post-build variables

| Variable                   | Description                           |     Default     | Required |
| -------------------------- | ------------------------------------- | :-------------: | :------: |
| cluster_domain             | The domain of the cluster             |       ""        |    ✓     |
| cluster_ingress_port       | The port of the ingress               |       ""        |    ✕     |
| harbor_storage_class       | The storage class to use for Harbor   |       ""        |    ✕     |
| harbor_storage_access_mode | The access mode for the storage class | "ReadWriteOnce" |    ✕     |
| harbor_image_registry      | The registry of the Harbor images     |    docker.io    |    ✕     |

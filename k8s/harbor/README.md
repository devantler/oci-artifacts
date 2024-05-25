# Harbor

Harbor is an open-source cloud native registry that stores, signs, and scans container images for vulnerabilities.

- [Documentation](https://goharbor.io/docs/)
- [Helm Chart](https://github.com/goharbor/harbor-helm)

## Post-build variables

| Variable                             | Description                               |     Default     | Required |
| ------------------------------------ | ----------------------------------------- | :-------------: | :------: |
| cluster_domain                       | The domain of the cluster                 |       ""        |    ✓     |
| harbor_storage_class                 | The storage class to use for Harbor       |       ""        |    ✕     |
| harbor_persistent_volume_access_mode | The access mode for the persistent volume | "ReadWriteMany" |    ✕     |

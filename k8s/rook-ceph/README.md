# Rook-Ceph

Rook is an open-source cloud-native storage orchestrator for Kubernetes, providing the platform, framework, and support for a diverse set of storage solutions to natively integrate with cloud-native environments.

## Post-build variables

| Variable                                         | Description                                        | Default | Required |
| ------------------------------------------------ | -------------------------------------------------- | :-----: | :------: |
| rook_ceph_cluster_ceph_blockpool_replicated_size | The number of replicas required for the block pool |    1    |    ✕     |
| rook_ceph_cluster_enable_discovery_daemon        | Whether to enable the Ceph discovery daemon        |  true   |    ✕     |
| rook_ceph_cluster_mgr_allow_multiple_per_node    | Whether to allow multiple Ceph managers per node   |  true   |    ✕     |
| rook_ceph_cluster_mon_allow_multiple_per_node    | Whether to allow multiple Ceph monitors per node   |  true   |    ✕     |

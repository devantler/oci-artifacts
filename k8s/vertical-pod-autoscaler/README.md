# Vertical Pod Autoscaler

A service that automatically adjusts the CPU and memory reservations for your pods to help them run more efficiently.

## Dependencies

- [Metrics Server](../infrastructure/metrics-server/README.md)

## Post-build variables

| Variable         | Description                                              | Default | Required |
| ---------------- | -------------------------------------------------------- | :-----: | :------: |
| vpa_min_replicas | The minimum number of live replicas required for updates |    1    |    ✕     |

## CRDs

### VerticalPodAutoscaler

This `VerticalPodAutoscaler` resource is used to enable Vertical Pod Autoscaling for a specific resource (e.g. `Deployment`, `StatefulSet`, `DaemonSet`).

```yaml
apiVersion: autoscaling.k8s.io/v1beta2
kind: VerticalPodAutoscaler
metadata:
  name: <vpa-name>
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment | StatefulSet | DaemonSet
    name: <target>
```

It is recommended that you deploy it alongside the component you want to autoscale.

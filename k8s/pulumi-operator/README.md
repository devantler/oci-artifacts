# Pulumi Operator

Pulumi Operator is a Kubernetes operator that manages and runs Pulumi programs and stacks.

- [Documentation](https://www.pulumi.com/docs/using-pulumi/continuous-delivery/pulumi-kubernetes-operator/) -[Helm Chart](https://github.com/pulumi/pulumi-kubernetes-operator/tree/master/deploy/helm/pulumi-operator)

## Post-build variables

| Variable                       | Description                                | Default   | Required |
| ------------------------------ | ------------------------------------------ | --------- | -------- |
| pulumi_operator_image_registry | The registry of the pulumi-operator images | docker.io | ✕        |

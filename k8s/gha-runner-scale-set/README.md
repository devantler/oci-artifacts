# GitHub Actions Runner Scale Set

GitHub Actions Runner Scale Set enables running self-hosted GitHub Actions runners in Kubernetes.

## Post-build variables

| Variable                                       | Description                                                                        | Default | Required |
| ---------------------------------------------- | ---------------------------------------------------------------------------------- | :-----: | :------: |
| gha_runner_scale_set_controller_image_registry | The container registry for the GitHub Runner Scale Set Controller image.           |         |    ✕     |
| gha_runner_scale_set_name                      | The name of the GitHub Actions Runner Scale set.                                   |         |    ✓     |
| github_config_url                              | The URL to the GitHub org or repo to scope the GitHub Actions Runner Scale set to. |         |    ✓     |
| github_token                                   | The GitHub Token required to authenticate with your GitHub org or repo.            |         |    ✓     |

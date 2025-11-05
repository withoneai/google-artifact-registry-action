# google-artifact-registry-action

A GitHub action that authenticates to [Google Artifact Registry](https://cloud.google.com/artifact-registry), builds a Docker image and pushes it to an Artifact Registry repository.


## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    # permissions required by google-github-actions/auth@v1, a dependency of picahq/google-artifact-registry-action@v2
    permissions:
      contents: read
      id-token: write

    steps:
      - uses: actions/checkout@v3
      - uses: picahq/google-artifact-registry-action@v2
        with:
          image: us-docker.pkg.dev/integrationos/docker-oss/my-service:v1
          service_account: github-actions@integrationos.iam.gserviceaccount.com
          workload_identity_provider: projects/356173785332/locations/global/workloadIdentityPools/github-actions/providers/github-actions
```


### Inputs

| Input  | Required? | Default | Description |
| ------ | --------- | ------- |------------ |
| `image`  | yes | | Full Docker image name to build and push, including the registry, repository and tag |
| `service_account` | yes | | GCP service account used to authenticate to Google Cloud |
| `workload_identity_provider` | yes | | GCP workload identity provider used to authenticate to Google Cloud |
| `context` | no | [Git context](https://github.com/docker/build-push-action/tree/master#git-context)| Build's context is the set of files located in the specified PATH or URL |
| `file` | no | `Dockerfile` | Path to the `Dockerfile` to build |
| `build-args` | no | `""` | The `build-args` to pass to `docker/build-push-action` |
| `secrets` | no | `""` | The `secrets` to pass to `docker/build-push-action` |

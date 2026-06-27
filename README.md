# common

Shared configuration and reusable GitHub Actions workflows for my repositories.

## Reusable workflows

### Prek (`.github/workflows/prek.yaml`)

Runs the `.pre-commit-config.yaml` pipeline via `prek`.

```yaml
jobs:
  lint:
    uses: ardubev16/common/.github/workflows/prek.yaml@master
```

### Python tests (`.github/workflows/python-test.yaml`)

Sets up `uv`, installs dev dependencies, and runs `pytest`.

```yaml
jobs:
  test:
    uses: ardubev16/common/.github/workflows/python-test.yaml@master
```

### Docker build (`.github/workflows/docker-build.yaml`)

Builds and pushes a Docker image to GHCR. Include
`type=ref,event=pr` in `tags` (the default) to also build and push
`pr-<number>` tagged images for pull requests.

```yaml
on:
  push:
    branches: [master]
    tags: ["v*"]
  pull_request:

jobs:
  docker:
    uses: ardubev16/common/.github/workflows/docker-build.yaml@master
    permissions:
      contents: read
      packages: write
```

### Docker clean PR image (`.github/workflows/docker-clean-pr.yaml`)

Deletes the `pr-<number>` tagged image for a closed pull request, so
PR images don't accumulate on GHCR indefinitely. Call it on
`pull_request: closed`.

```yaml
on:
  pull_request:
    types: [closed]

jobs:
  clean:
    uses: ardubev16/common/.github/workflows/docker-clean-pr.yaml@master
    permissions:
      packages: write
    with:
      pr-number: ${{ github.event.pull_request.number }}
    # optional, only needed for personal-account (non-org) packages
    secrets:
      package-token: ${{ secrets.PACKAGE_TOKEN }}
```

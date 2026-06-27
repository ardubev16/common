# common

Shared configuration and reusable GitHub Actions workflows for my repositories.

## Reusable workflows

### Prek (`.github/workflows/prek.yaml`)

Runs the `.pre-commit-config.yaml` pipeline via `prek`.

```yaml
jobs:
  lint:
    uses: ardubev16/common/.github/workflows/prek.yaml@main
```

### Python tests (`.github/workflows/python-test.yaml`)

Sets up `uv`, installs dev dependencies, and runs `pytest`.

```yaml
jobs:
  test:
    uses: ardubev16/common/.github/workflows/python-test.yaml@main
```

### Docker build and clean (`.github/workflows/docker-build-clean.yaml`)

Builds and pushes a Docker image to GHCR, then deletes old/untagged
package versions, keeping the most recent ones.

```yaml
jobs:
  docker:
    uses: ardubev16/common/.github/workflows/docker-build-clean.yaml@main
    permissions:
      contents: read
      packages: write
    # optional, only needed for personal-account (non-org) packages
    secrets:
      package-token: ${{ secrets.PACKAGE_TOKEN }}
```

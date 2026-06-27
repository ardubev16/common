# common

Shared configuration and reusable GitHub Actions workflows for my repositories.

- `renovate.json` / `default.json` — shared Renovate config.
- `.github/workflows/prek.yaml` — runs the prek (pre-commit) pipeline.
- `.github/workflows/python-test.yaml` — runs Python tests with uv/pytest.
- `.github/workflows/docker-build.yaml` — builds and pushes a Docker image to GHCR.
- `.github/workflows/docker-clean-pr.yaml` — deletes a PR's `pr-<number>` image from GHCR.

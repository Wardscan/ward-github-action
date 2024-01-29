# Mitigate GitHub Action

This GitHub Action generates Software Bill of Materials (SBOMs) using Syft and uploads them to [Mitigate](https://dev.mitigate.maggioli-research.gr), syncing them with your chosen asset.

## Features

- Generates SBOMs for Docker images or repositories.
- Uploads SBOMs directly to [Mitigate](https://dev.mitigate.maggioli-research.gr) and syncs them with your chosen asset.

## Inputs

- `assetid`: The ID of your asset that you want to get synced.
- `type`: Specifies where the SBOM will be generated from (`image`, `repo`).
- `registry`: The Docker registry of the image that you want to scan.
- `imagename`: The name of the Docker image that you want to scan.

## Usage

### Snippet of Image Scan

```yaml
name: Mitigate-github-action

on:
  - push
  - pull_request
  - workflow_dispatch

jobs:
  generate_sbom:
    runs-on: ubuntu-latest
    name: "Mitigate SBOM generator"
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4
            
      - name: Login to Container Registry
        uses: docker/login-action@v3
        with:
          registry: <my_registry_name>
          username: ${{ secrets.REGISTRY_USER }}
          password: ${{ secrets.REGISTRY_PASSWORD }}

      - name: Mitigate SBOM Asset Sync
        uses: Mitigate-new/mitigate-github-action@main
        with:
          assetid: ${{ secrets.ASSETID}}
          type: image
          imagename: <my_image_name>
```
### Snippet of Repo Scan

```yaml
name: Mitigate-github-action

on:
  - push
  - pull_request
  - workflow_dispatch

jobs:
  generate_sbom:
    runs-on: ubuntu-latest
    name: "Mitigate SBOM generator"
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Mitigate SBOM Asset Sync
        uses: Mitigate-new/mitigate-github-action@main
        with:
          assetid: ${{ secrets.ASSETID}}
          type: repo
```
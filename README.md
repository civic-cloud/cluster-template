# civic-cloud

This repository provides a complete toolkit for deploying and managing public-interest Kubernetes clusters for communities.

## Contents

- `.github/workflows/`
  - `publish-docs.yml`: Publishes `docs/` content to <http://civic-cloud.phl.io/> on push/merge into the `main` branch
  - `update-tag-projections.yml`: Updates the `docs/blueprint`, `k8s/blueprint`, and `k8s/manifests` holobranch projections
- `.holo/branches/`
  - `docs-site`: Builds static website via `mkdocs` from `mkdocs.yml` and `docs/**`
  - `gh-pages`: Combines `docs-site` content with `CNAME` configuration for the main civic-cloud website
  - `github-workflows`: Provides `.github/workflows` content to automate deployment of cluster releases
  - `k8s-manifests`: Canonical manifest tree for local and sourced Kubernetes content
  - `docs-blueprint`: Ready-to-build blueprint for `docs-site` that can be used as a foundation by extending projects
  - `k8s-blueprint`: Ready-to-build blueprint for `k8s-manifests` that can be used as a foundation by extending projects
- `.holo/lenses/`
  - `mkdocs`: Builds `docs-blueprint` into `docs-site`
- `.holo/sources/`
  - `cluster-template`: The repository, branch, and tag version for the upstream cluster template
- `docs/`: Documentation content in mkdocs format
- `script/`: Developer workflow commands

## Getting started

### Documentation

Check system dependencies and launch container providing live editing of docs content:

```bash
script/studio
```

### Kubernetes Manifests

A basic process for iterating on manifest content:

1. Copy/reset local `k8s/manifests` branch from latest on GitHub:

    ```bash
    git fetch origin +refs/heads/k8s/manifests:refs/heads/k8s/manifests
    ```

2. Commit new projection from working tree content to `k8s/manifests` branch:

    ```bash
    git holo project k8s-manifests \
        --working \
        --commit-to=k8s/manifests
    ```

### Kubernetes Blueprint

A basic process for iterating on manifest content in its pre-built (blueprint) form:

1. Copy/reset local `k8s/blueprint` branch from latest on GitHub:

    ```bash
    git fetch origin +refs/heads/k8s/blueprint:refs/heads/k8s/blueprint
    ```

2. Commit new projection from working tree content to `k8s/blueprint` branch:

    ```bash
    git holo project k8s-blueprint \
        --working \
        --commit-to=k8s/blueprint
    ```

# setup-artifactory-repo-tool

GitHub Action to install `artifactory-repo-tool`.

## Usage

```yaml
jobs:
  Setup artifactory-repo-tool:
    runs-on: ubuntu-latest
    steps:
      # ... potentially other steps ...
      - uses: hashicorp/artifactory-repo-tool@v1
        with:
          github-token: ${{ secrets.ART_GITHUB_TOKEN }}
```

### Inputs

| Input          | Description                                                        | Default        |
| -------------- | ------------------------------------------------------------------ | -------------- |
| `github-token` | GitHub token with release asset access to `artifactory-repo-tool`. |                |
| `version`      | Version of `artifactory-repo-tool` to install.                     | Latest release |

### Outputs

| Output    | Description                         |
| --------- | ----------------------------------- |
| `version` | Version of `artifactory-repo-tool` installed. |

## Development

Test locally with [act](https://github.com/nektos/act). You'll need a GitHub
token authorized to download release assets from the
[artifactory-repo-tool](https://github.com/hashicorp/artifactory-repo-tool) repository.

```bash
act --container-architecture=linux/amd64 --input github-token=$(gh auth token) workflow_dispatch
```

### Creating a Release

After your PR is merged to the default branch, `main`:

1. Update locally: `git checkout main && git pull`
1. Create a new tag for the release, e.g. `v1.0.0` with `git tag v1.0.0 && git push origin v1.0.0`.
1. Update the major version tag locally, e.g. `git tag -d v1 && git tag v1`
1. Update the tag upstream, e.g. `git push origin :refs/tags/v1 && git push origin v1`

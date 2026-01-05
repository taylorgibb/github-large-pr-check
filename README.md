# Github Action Large Pull Request Checker

A Github Action that checks if your Pull Requests exceed a given limit of number of lines of code changes (additions + deletions).

## Usage

```yaml
on: [pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: developerhut/github-large-pr-check@v1.0.0
        with:
          target_branch: ${{ github.event.pull_request.base.ref }}
          max_lines_changed: 500
          exclude_paths: |
            *package-lock.json
            *yarn.lock
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `max_lines_changed` | Maximum number of lines changed allowed | Yes | `400` |
| `target_branch` | The branch to compare against | Yes | `main` |
| `exclude_paths` | Newline-separated list of pathspec patterns to exclude | No | `""` |

## Outputs

| Output | Description |
|--------|-------------|
| `total_lines_changed` | Total lines changed in this PR (after exclusions) |

## Common Exclusion Patterns

The `exclude_paths` input uses git pathspec patterns. Here are common patterns you might want to exclude:

### Exclusion Examples

```yaml
exclude_paths: |
  *package-lock.json
  *yarn.lock
  *pnpm-lock.yaml
  *Gemfile.lock
  *poetry.lock
  *Pipfile.lock
  *composer.lock
  *Cargo.lock
```

## License

This is software is licensed under the MIT license. See [LICENSE](./LICENSE) for details.

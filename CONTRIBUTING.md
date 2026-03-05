# Contributing

## PR Title Convention

This project uses [Conventional Commits](https://www.conventionalcommits.org/) for **PR titles**. Since we squash-merge, the PR title becomes the final commit message.

### Format

```text
type: description
```

### Allowed Types

| Type | Purpose |
|------|---------|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation only |
| `style` | Code style (formatting, semicolons, etc.) |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `perf` | Performance improvement |
| `test` | Adding or updating tests |
| `build` | Build system or external dependencies |
| `ci` | CI configuration |
| `chore` | Other changes that don't modify src or test files |
| `revert` | Reverts a previous commit |

### Examples

- `feat: add skip-checkout input`
- `fix: handle empty trigger-tag-prefix`
- `docs: update installation instructions`

### Individual Commits

Individual commit messages within a PR are free-form. Only the PR title is enforced.

## Testing

CI runs two workflow files on push to `main` and on pull requests:

- **Unit tests** (`.github/workflows/unit-test.yml`) — test the derive logic with various prefix combinations using `skip-checkout: true` so no real tags are needed.
- **Integration tests** (`.github/workflows/integration-test.yml`) — exercise the full action including the checkout step against real tags on the remote.

To run tests locally with [act](https://github.com/nektos/act):

```bash
act push --container-architecture linux/amd64
```

## Releasing

1. Tag the release and push:

   ```bash
   git tag v1.x.x
   git push origin v1.x.x
   ```

2. Create a GitHub Release from the tag and check **"Publish this Action to the GitHub Marketplace"** in the release form.

3. Update the floating major-version tag so users who pin to `v1` get the latest:

   ```bash
   git tag -f v1 v1.x.x
   git push -f origin v1
   ```

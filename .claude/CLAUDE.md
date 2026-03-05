# CLAUDE.md

## Project

This is a **GitHub Actions composite action** (`checkout-version-tag`) published to the GitHub Actions Marketplace.

It derives a release tag from a trigger tag and checks out the corresponding ref. For example, given trigger tag `u1.2.3`, it checks out `v1.2.3`.

Extracted from [`TaiSakuma/legendary-octo-happiness`](https://github.com/TaiSakuma/legendary-octo-happiness) (`.github/actions/checkout-version-tag/`).

## Structure

- `action.yml` — the composite action definition (the only required file for a composite action)

## Testing

CI runs two workflow files on push to `main` and on pull requests:

- **Unit tests** (`.github/workflows/unit-test.yml`) — test the derive logic with `skip-checkout: true`.
- **Integration tests** (`.github/workflows/integration-test.yml`) — exercise the full action including checkout against real tags.

Run locally with [act](https://github.com/nektos/act):

```bash
act push --container-architecture linux/amd64
```

## PR Convention

Squash-merge with [Conventional Commits](https://www.conventionalcommits.org/) PR titles (e.g., `feat: ...`, `fix: ...`). See `CONTRIBUTING.md` for details.

## Releases

Two-tag flow automated by CI:

1. Push a `u<version>` tag (e.g., `git tag u1.0.0 && git push origin u1.0.0`).
2. The **Generate changelog** workflow (`changelog.yml`) updates `CHANGELOG.md` and creates the `v<version>` tag.
3. The **Release** workflow (`release.yml`) creates a GitHub Release with auto-generated notes and moves the floating major-version tag (e.g., `v1`, `v2`).

## Marketplace

- Branding: icon `tag`, color `blue`.
- The `name` and `description` fields in `action.yml` appear on the Marketplace listing.

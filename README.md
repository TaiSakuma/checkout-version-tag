# checkout-version-tag

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Checkout%20Version%20Tag-blue?logo=github)](https://github.com/marketplace/actions/checkout-version-tag)

A GitHub Action that derives a release tag from a trigger tag and checks out the corresponding ref.

This is useful in release workflows where a "trigger" tag (e.g., `u1.2.3`) is pushed to kick off the release process, and the workflow needs to check out the matching release tag (e.g., `v1.2.3`).

## Usage

```yaml
- uses: TaiSakuma/checkout-version-tag@v1
  with:
    trigger-tag: ${{ github.ref_name }}
```

### Full example

```yaml
on:
  push:
    tags:
      - "u[0-9]+.*"

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: TaiSakuma/checkout-version-tag@v1
        id: checkout
        with:
          trigger-tag: ${{ github.ref_name }}

      - run: echo "Release tag is ${{ steps.checkout.outputs.release-tag }}"
      - run: echo "Version is ${{ steps.checkout.outputs.version }}"
```

## Inputs

| Name                 | Description                                  | Required | Default |
| -------------------- | -------------------------------------------- | -------- | ------- |
| `trigger-tag`        | Tag/branch name to derive from (e.g., u1.2.3)| Yes      |         |
| `trigger-tag-prefix` | Prefix to strip from the trigger tag         | No       | `u`     |
| `release-tag-prefix` | Prefix for the release tag                   | No       | `v`     |
| `fetch-depth`        | Number of commits to fetch                   | No       | `1`     |

## Outputs

| Name          | Description                           |
| ------------- | ------------------------------------- |
| `release-tag` | Computed release tag (e.g., `v1.2.3`) |
| `version`     | Bare version number (e.g., `1.2.3`)   |

## How it works

1. Strips the `trigger-tag-prefix` (default: `u`) from the trigger tag to extract the version number.
2. Prepends the `release-tag-prefix` (default: `v`) to form the release tag.
3. Checks out the release tag using `actions/checkout`.

## License

[MIT](LICENSE)

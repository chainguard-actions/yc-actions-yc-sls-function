<!-- markdownlint-disable -->

# Hardening Report: yc-actions--yc-sls-function/v4.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **yc-actions--yc-sls-function/v4.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in the workflow files use mutable version tags (e.g. `@v4`) instead of full 40-character commit SHA hashes. This means a compromised or updated action tag could silently execute different code. Affected references: `actions/checkout@v4`, `actions/setup-node@v4`, `actions/upload-artifact@v4` in check-dist.yml, and `actions/checkout@v4` in test.yml.

Locations:

- `.github/workflows/check-dist.yml:21`
- `.github/workflows/check-dist.yml:24`
- `.github/workflows/check-dist.yml:43`
- `.github/workflows/test.yml:12`

### missing-permissions (severity: medium)

Neither `.github/workflows/check-dist.yml` nor `.github/workflows/test.yml` has a top-level `permissions:` key, and no individual job within either file defines a `permissions:` block. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/check-dist.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned all `uses:` references to full 40-char commit SHAs — actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262, actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020, actions/upload-artifact@v4 → @ea165f8d65b6e75b540449e92b4886f43607fa02 — with original tags preserved as inline comments. (2) Added top-level `permissions: contents: read` to both check-dist.yml and test.yml, which is the minimum needed for checkout and npm build operations.


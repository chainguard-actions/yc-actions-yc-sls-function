<!-- markdownlint-disable -->

# Hardening Report: yc-actions--yc-sls-function/v4.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **yc-actions--yc-sls-function/v4.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow files reference GitHub Actions using mutable version tags (@v4) instead of immutable full-length SHA commit hashes. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code. Affected references: actions/checkout@v4, actions/setup-node@v4, actions/upload-artifact@v4 (check-dist.yml); actions/checkout@v4 (test.yml). Each should be pinned to a full 40-character hex SHA, e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.

Locations:

- `.github/workflows/check-dist.yml:21`
- `.github/workflows/check-dist.yml:24`
- `.github/workflows/check-dist.yml:42`
- `.github/workflows/test.yml:13`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` key, and no individual job defines its own `permissions:` block. Without explicit permissions, GitHub Actions uses the repository's default token permissions, which may be overly broad (e.g. write access to contents, pull-requests, etc.). Both check-dist.yml and test.yml should declare minimal required permissions (e.g. `permissions: contents: read`) at the top level or per job.

Locations:

- `.github/workflows/check-dist.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned all action references to full SHA hashes — actions/checkout@11d5960a326750d5838078e36cf38b85af677262, actions/setup-node@49933ea5288caeca8642d1e84afbd3f7d6820020, actions/upload-artifact@ea165f8d65b6e75b540449e92b4886f43607fa02 — with original tags preserved as comments. (2) Added top-level `permissions: contents: read` to both check-dist.yml and test.yml, restricting the GITHUB_TOKEN to the minimum needed for checkout and build operations.


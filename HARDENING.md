<!-- markdownlint-disable -->

# Hardening Report: yc-actions--yc-sls-function/v3.3.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **yc-actions--yc-sls-function/v3.3.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow files reference actions using mutable version tags instead of pinned full-length SHA commits. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Failing references: `actions/checkout@v4`, `actions/setup-node@v4`, `actions/upload-artifact@v4` in check-dist.yml; `actions/checkout@v4` in test.yml.

Locations:

- `.github/workflows/check-dist.yml:22`
- `.github/workflows/check-dist.yml:25`
- `.github/workflows/check-dist.yml:43`
- `.github/workflows/test.yml:13`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and no job within them defines job-level permissions. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/check-dist.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files:
1. check-dist.yml: Pinned actions/checkout@v4 to SHA 34e114876b0b11c390a56381ad16ebd13914f8d5, actions/setup-node@v4 to SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, and actions/upload-artifact@v4 to SHA ea165f8d65b6e75b540449e92b4886f43607fa02. Added top-level `permissions: contents: read`.
2. test.yml: Pinned actions/checkout@v4 to SHA 34e114876b0b11c390a56381ad16ebd13914f8d5. Added top-level `permissions: contents: read`.
All original tags are preserved as inline comments for readability.


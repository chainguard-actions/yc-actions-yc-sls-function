<!-- markdownlint-disable -->

# Hardening Report: yc-actions--yc-sls-function/v5.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **yc-actions--yc-sls-function/v5.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references in the workflow files use mutable version tags instead of immutable 40-character SHA commit hashes, making the workflows vulnerable to supply-chain attacks if the referenced action tags are moved or compromised. Failing references:
- `actions/checkout@v7`
- `actions/setup-node@v7`
- `actions/upload-artifact@v7`

Locations:

- `.github/workflows/check-dist.yml:23`
- `.github/workflows/check-dist.yml:29`
- `.github/workflows/check-dist.yml:56`
- `.github/workflows/ci.yml:21`
- `.github/workflows/ci.yml:27`
- `.github/workflows/ci.yml:47`
- `.github/workflows/ci.yml:53`
- `.github/workflows/linter.yml:24`
- `.github/workflows/linter.yml:31`
- `.github/workflows/linter.yml:40`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all mutable action tag references to full 40-character commit SHAs across three workflow files:
- check-dist.yml: actions/checkout@v7 → @3d3c42e5aac5ba805825da76410c181273ba90b1, actions/setup-node@v7 → @820762786026740c76f36085b0efc47a31fe5020, actions/upload-artifact@v7 → @043fb46d1a93c77aae656e7c1c64a875d1fc6a0a
- ci.yml: actions/checkout@v7 (×2) → @3d3c42e5aac5ba805825da76410c181273ba90b1, actions/setup-node@v7 (×2) → @820762786026740c76f36085b0efc47a31fe5020
- linter.yml: actions/checkout@v7 → @3d3c42e5aac5ba805825da76410c181273ba90b1, actions/setup-node@v7 → @820762786026740c76f36085b0efc47a31fe5020, super-linter/super-linter/slim@v8 → @4ce20838b8ab83717e78138c5b3a1407148e0918
Original tags preserved as inline comments for readability.


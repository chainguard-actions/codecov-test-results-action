<!-- markdownlint-disable -->

# Hardening Report: codecov--test-results-action/v1.0.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **codecov--test-results-action/v1.0.3** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v4.1.1`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. It should be replaced with the full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.1.1`.

Locations:

- `.github/workflows/main.yml:11`

### broad-permissions (severity: medium)

The job `run` in main.yml sets `permissions: read-all`, which grants read access to all repository scopes. This is overly broad and should be replaced with the minimal specific permissions actually required by the job (e.g. `contents: read`).

Locations:

- `.github/workflows/main.yml:6`

### missing-permissions (severity: medium)

The workflow `enforce-license-compliance.yml` has no top-level `permissions:` key and the single job `enforce-license-compliance` also has no `permissions:` key. Without an explicit permissions block, the job inherits the repository's default token permissions, which may be broader than necessary. A minimal permissions block (e.g. `permissions: {}` or `contents: read`) should be added.

Locations:

- `.github/workflows/enforce-license-compliance.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, broad-permissions, missing-permissions

**Notes:**

1. main.yml line 11: Pinned actions/checkout@v4.1.1 to full SHA b4ffde65f46336ab88eb53be808477a3936bae11 with tag comment. 2. main.yml line 6: Replaced broad `permissions: read-all` with minimal `permissions: contents: read` (the job only checks out code, installs npm deps, lints, and uploads test results). 3. enforce-license-compliance.yml: Added `permissions: {}` at the workflow top level since the license compliance job requires no GitHub token permissions.


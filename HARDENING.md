<!-- markdownlint-disable -->

# Hardening Report: codecov--test-results-action/v1.2.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **codecov--test-results-action/v1.2.1** was hardened automatically. 2 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v4.1.1` which is pinned to a mutable tag rather than a full 40-character commit SHA. This is vulnerable to supply-chain attacks if the tag is moved. It should be replaced with a pinned SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.1.1`.

Locations:

- `.github/workflows/main.yml:14`

### missing-permissions (severity: medium)

The workflow file `enforce-license-compliance.yml` has no top-level `permissions:` key and its only job (`enforce-license-compliance`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default repository permissions (which may include `write` access to contents and other scopes), violating the principle of least privilege. A minimal permissions block such as `permissions: read-all` or specific scopes should be added.

Locations:

- `.github/workflows/enforce-license-compliance.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `actions/checkout@v4.1.1` to its full commit SHA `b4ffde65f46336ab88eb53be808477a3936bae11` in `.github/workflows/main.yml` (line 14), preserving the tag as a comment for readability. 2. Added `permissions: read-all` at the top level of `.github/workflows/enforce-license-compliance.yml` to satisfy the least-privilege requirement — the workflow only needs read access to check out code and run the license compliance action.

### Iteration 2

**Fixes applied:** broad-permissions

**Notes:**

Replaced `permissions: read-all` with `permissions: contents: read` in `.github/workflows/enforce-license-compliance.yml`. The workflow only requires reading repository contents to perform license compliance checks, so all other permission scopes are omitted.


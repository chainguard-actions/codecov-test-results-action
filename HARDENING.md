<!-- markdownlint-disable -->

# Hardening Report: codecov--test-results-action/v1.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **codecov--test-results-action/v1.1.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses actions/checkout@v4.1.1, which is pinned to a mutable version tag rather than an immutable full 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. It should be pinned to a full SHA, e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.1.1.

Locations:

- `.github/workflows/main.yml:14`

### missing-permissions (severity: medium)

The workflow file enforce-license-compliance.yml has no top-level permissions: key and the single job (enforce-license-compliance) also has no job-level permissions: key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents, pull-requests, etc.). A minimal permissions block should be added.

Locations:

- `.github/workflows/enforce-license-compliance.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned actions/checkout@v4.1.1 to full SHA b4ffde65f46336ab88eb53be808477a3936bae11 in .github/workflows/main.yml, preserving the tag as a comment. 2. Added top-level `permissions: {}` to .github/workflows/enforce-license-compliance.yml to explicitly deny all default token permissions, since the workflow only calls an external license compliance action using a FOSSA API key and requires no GitHub token access.


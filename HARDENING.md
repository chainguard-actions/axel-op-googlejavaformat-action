<!-- markdownlint-disable -->

# Hardening Report: axel-op--googlejavaformat-action/v4.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **axel-op--googlejavaformat-action/v4.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All workflow files reference external actions using mutable tag-based refs instead of full 40-character SHA commit hashes, making them vulnerable to supply-chain attacks if a tag is moved. Failing references include: actions/checkout@v4, github/codeql-action/init@v3, github/codeql-action/analyze@v3 (codeql-analysis.yml); actions/checkout@v4, actions/setup-node@v4 (compile.yml); actions/checkout@v4, actions/setup-node@v4, actions/setup-java@v1 (test.yml); actions/checkout@v4, krzema12/github-actions-typing@v2 (validate-action-typings.yml).

Locations:

- `.github/workflows/codeql-analysis.yml:30`
- `.github/workflows/codeql-analysis.yml:34`
- `.github/workflows/codeql-analysis.yml:43`
- `.github/workflows/compile.yml:9`
- `.github/workflows/compile.yml:11`
- `.github/workflows/compile.yml:14`
- `.github/workflows/test.yml:8`
- `.github/workflows/test.yml:9`
- `.github/workflows/test.yml:22`
- `.github/workflows/test.yml:24`
- `.github/workflows/test.yml:26`
- `.github/workflows/test.yml:43`
- `.github/workflows/test.yml:45`
- `.github/workflows/test.yml:47`
- `.github/workflows/validate-action-typings.yml:8`
- `.github/workflows/validate-action-typings.yml:9`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and no individual job within any of these files defines its own `permissions:` block. Without explicit permissions, workflows inherit the default repository permissions (which may be broad), violating the principle of least privilege.

Locations:

- `.github/workflows/codeql-analysis.yml:1`
- `.github/workflows/compile.yml:1`
- `.github/workflows/test.yml:1`
- `.github/workflows/validate-action-typings.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 workflow files: (1) Pinned all external action references to full 40-character SHA commit hashes with tag comments for readability: actions/checkout@v4→11d5960a, github/codeql-action/init@v3→b7351df, github/codeql-action/analyze@v3→b7351df, actions/setup-node@v4→49933ea, actions/setup-java@v1→b6e674f, krzema12/github-actions-typing@v2→9ddf35b. (2) Added top-level permissions blocks to all 4 workflows with least-privilege permissions: codeql-analysis.yml gets contents:read + security-events:write (required for CodeQL to upload SARIF results); compile.yml gets contents:write (required to push compiled dist files); test.yml gets contents:read; validate-action-typings.yml gets contents:read.


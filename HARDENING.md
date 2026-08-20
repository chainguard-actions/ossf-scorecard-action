<!-- markdownlint-disable -->

# Hardening Report: ossf--scorecard-action/v2.4.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ossf--scorecard-action/v2.4.3** was hardened automatically. 5 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses 'ossf/scorecard-action@main' — a mutable branch ref instead of a pinned 40-character commit SHA. This exposes the workflow to supply-chain attacks if the branch is compromised.

Locations:

- `.github/workflows/scorecards.yml:24`

### unpinned-uses (severity: high)

The action.yaml Docker action references 'docker://ghcr.io/ossf/scorecard-action:v2.4.3' — a mutable image tag instead of an immutable SHA digest (e.g. @sha256:<64-hex-char-digest>). A tag can be silently repointed to a different image.

Locations:

- `action.yaml:68`

### script-injection (severity: high)

Rule (a): A ${{ ... }} expression is interpolated directly inside a run: shell command. The offending line is: `run: GITHUB_AUTH_TOKEN=${{ secrets.GITHUB_TOKEN }} go test -covermode=atomic -coverprofile=unit-coverage.out ./...`. Any ${{ }} expression inside a run: block is a script-injection risk because the value is substituted into the shell command string before the shell parses it. The value should be passed via an env: block and referenced as an environment variable instead.

Locations:

- `.github/workflows/tests.yaml:28`

### broad-permissions (severity: medium)

The workflow sets top-level 'permissions: read-all', which grants overly broad read access across all scopes. Replace with specific minimal permissions (e.g. contents: read, security-events: write) scoped to what each job actually needs.

Locations:

- `.github/workflows/scorecards.yml:6`

### broad-permissions (severity: medium)

The workflow sets top-level 'permissions: read-all', which grants overly broad read access across all scopes. Replace with specific minimal permissions scoped to what each job actually needs.

Locations:

- `.github/workflows/tests.yaml:8`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, script-injection, broad-permissions

**Notes:**

Fixed all 5 findings across 3 files:
1. scorecards.yml: Replaced 'permissions: read-all' with 'permissions: contents: read' (minimal top-level), and pinned 'ossf/scorecard-action@main' to full SHA 'e8e61e86ea0a152be84d03729c02a7300065c17d # main'.
2. tests.yaml: Replaced 'permissions: read-all' with 'permissions: contents: read', and moved '${{ secrets.GITHUB_TOKEN }}' from the run: shell command into an env: block as 'GITHUB_AUTH_TOKEN', referencing it as a plain env var in the shell.
3. action.yaml: Pinned the Docker image 'docker://ghcr.io/ossf/scorecard-action:v2.4.3' with its immutable SHA digest, resulting in 'docker://ghcr.io/ossf/scorecard-action:v2.4.3@sha256:2dd6a6d60100f78ef24e14a47941d0087a524b4d3642041558239b1c6097c941', preserving the docker:// scheme and tag.


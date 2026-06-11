<!-- markdownlint-disable -->

# Hardening Report: ossf--scorecard-action/v2.4.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **ossf--scorecard-action/v2.4.3** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yaml uses a Docker image pinned to a mutable version tag (`v2.4.3`) rather than an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the action reference. The failing reference is: `image: "docker://ghcr.io/ossf/scorecard-action:v2.4.3"`. It should be changed to a SHA-digest form such as `image: "docker://ghcr.io/ossf/scorecard-action@sha256:<64-hex-char-digest> # v2.4.3"`.

Locations:

- `action.yaml:57`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://ghcr.io/ossf/scorecard-action:v2.4.3` with the immutable SHA digest form `docker://ghcr.io/ossf/scorecard-action@sha256:2dd6a6d60100f78ef24e14a47941d0087a524b4d3642041558239b1c6097c941 # v2.4.3` in action.yaml at line 57. The digest was resolved via the Docker Registry HTTP API v2.


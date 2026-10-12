<!-- markdownlint-disable -->

# Hardening Report: ossf--scorecard-action/v2.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ossf--scorecard-action/v2.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yaml uses a Docker image referenced by a mutable version tag (`v2.5.0`) instead of an immutable SHA digest. This means the image could be silently replaced with a different (potentially malicious) version without any change to the action file. The reference `docker://ghcr.io/ossf/scorecard-action:v2.5.0` should be replaced with a SHA-pinned form such as `docker://ghcr.io/ossf/scorecard-action@sha256:<64-hex-char-digest> # v2.5.0`.

Locations:

- `action.yaml:62`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yaml from `docker://ghcr.io/ossf/scorecard-action:v2.5.0` to `docker://ghcr.io/ossf/scorecard-action:v2.5.0@sha256:1e1481c65fc2407d3fd6ab18a23c741eb4d1c0d9359ebafc4b3ab13aa61d8627`, preserving the docker:// scheme and the version tag inline alongside the immutable digest.


<!-- markdownlint-disable -->

# Hardening Report: ossf--scorecard-action/v2.6.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ossf--scorecard-action/v2.6.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Docker action image uses a mutable tag instead of a SHA digest: `image: "docker://ghcr.io/ossf/scorecard-action:v2.6.0"`. Pin it to a digest, e.g. `docker://ghcr.io/ossf/scorecard-action@sha256:<digest> # v2.6.0`.

Locations:

- `action.yaml:74`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image in action.yaml to its digest. It now reads docker://ghcr.io/ossf/scorecard-action:v2.6.0@sha256:7f092e5a4a363af001cca6cdb04f111e212173ba602336104394e7febc2c6e48. The digest came from the registry lookup. The docker:// scheme and the tag are kept in the reference.


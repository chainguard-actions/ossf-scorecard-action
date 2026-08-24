<!-- markdownlint-disable -->

# Hardening Report: ossf--scorecard-action/v2.4.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ossf--scorecard-action/v2.4.4** was hardened automatically. 5 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `ossf/scorecard-action@main` — a mutable branch ref instead of a pinned 40-character commit SHA. This allows supply-chain attacks if the referenced branch is compromised.

Locations:

- `.github/workflows/scorecards.yml:24`

### unpinned-uses (severity: high)

The action's Docker image reference uses a mutable tag (`v2.4.4`) instead of a SHA digest: `image: "docker://ghcr.io/ossf/scorecard-action:v2.4.4"`. A tag can be silently repointed to a different image, enabling supply-chain attacks.

Locations:

- `action.yaml:62`

### broad-permissions (severity: medium)

The workflow sets top-level `permissions: read-all`, which grants overly broad read access to all scopes. It should be replaced with specific minimal permissions.

Locations:

- `.github/workflows/scorecards.yml:6`

### broad-permissions (severity: medium)

The workflow sets top-level `permissions: read-all`, which grants overly broad read access to all scopes. It should be replaced with specific minimal permissions.

Locations:

- `.github/workflows/tests.yaml:8`

### script-injection (severity: high)

Rule (a) violation: A `${{ }}` expression is interpolated directly inside a `run:` shell command. The offending line is: `run: GITHUB_AUTH_TOKEN=${{ secrets.GITHUB_TOKEN }} go test -covermode=atomic -coverprofile=unit-coverage.out ./...`. The expression is substituted by the YAML template engine before the shell processes the command, meaning any special characters in the value are interpreted by the shell. The value should be passed via an `env:` block and referenced as `$GITHUB_AUTH_TOKEN` in the shell command.

Locations:

- `.github/workflows/tests.yaml:27`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, broad-permissions, script-injection

**Notes:**

Fixed all 5 findings:
1. scorecards.yml: Pinned ossf/scorecard-action@main to full SHA e8e61e86ea0a152be84d03729c02a7300065c17d
2. action.yaml: Pinned Docker image docker://ghcr.io/ossf/scorecard-action:v2.4.4 with SHA digest sha256:ae5104dd3cc28466ebeb11144354be4cac4b7ff829654f9fab89021d71c46670 (preserving docker:// scheme and tag)
3. scorecards.yml: Replaced top-level 'permissions: read-all' with 'permissions: contents: read'
4. tests.yaml: Replaced top-level 'permissions: read-all' with 'permissions: contents: read'
5. tests.yaml: Moved ${{ secrets.GITHUB_TOKEN }} out of the run: shell command into an env: block (GITHUB_AUTH_TOKEN), eliminating the script injection risk


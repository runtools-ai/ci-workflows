# ci-workflows

Reusable GitHub Actions workflows for RunTools per-repo PR CI.

This repo is the authoritative source for the **droplet**, **consumer**, and **app-platform-preview** smoke patterns. Per-repo workflows under `runtools-ai/runtools-*/.github/workflows/ci.yml` call into the workflows here via `workflow_call`.

Linear project: [Layer 3 — Per-repo CI](https://linear.app/runtools/project/layer-3-per-repo-ci-6e1a15a8a23a).

## Patterns

| Pattern | When to use | Reusable workflow |
|---|---|---|
| **droplet** | Repo deploys to a DO droplet (orchestrator, storage, model-gateway, fc-agent, code-exec). Build PR code → start on localhost:N → smoke against localhost + prod-deps | `droplet-localhost-smoke.yml` |
| **consumer** | Repo ships a CLI/SDK/Mac binary, OR an App Platform service running only build/typecheck/lint. Generic: install deps + run arbitrary `smoke_commands` | `consumer-prod-smoke.yml` |
| **app-platform-preview** | Repo deploys to DO App Platform (auth, billing, tools, runtools.ai) AND needs a real PR preview app + functional smoke against it. Deploys preview via `digitalocean/app_action@v2` + waits for health + runs scoped smoke. See sharp-edge note below. | `app-platform-preview-smoke.yml` |

### App Platform preview pattern — current limitation

The committed `.do/app.yaml` contains `EV[1:...]` encrypted secret values from the PROD app's at-rest encryption key. When `digitalocean/app_action@v2` creates a fresh preview app, **those values will not decrypt** because the preview is a different app with its own encryption key.

For now, the `app-platform-preview-smoke.yml` workflow is usable in two scenarios:
1. **Health/route-shape smoke only** — preview boots in degraded mode where secret-dependent paths fail, but `/health` (or any route that doesn't read secrets) returns 200. Use this for PR-shape validation.
2. **Caller pre-populates preview secrets via doctl** — caller's workflow runs `doctl apps update <preview-id> --spec <overridden-spec>` between deploy and health-check to inject smoke-safe secret values.

For App Platform repos that just need build/typecheck/lint validation today (no preview app), use the **consumer** pattern instead — `consumer-prod-smoke.yml` is generic enough.

## How a consumer repo calls into this

`runtools-ai/<repo>/.github/workflows/ci.yml`:

```yaml
name: CI

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]
  push:
    branches: [master]

permissions:
  contents: read
  id-token: write   # Vault OIDC
  packages: read    # @runtools-ai npm scope on npm.pkg.github.com

jobs:
  smoke:
    uses: runtools-ai/ci-workflows/.github/workflows/droplet-localhost-smoke.yml@main
    secrets: inherit
    with:
      service_name: orchestrator
      vault_role: orchestrator
      port: 8080
      build_command: bun install --frozen-lockfile && bun run build
      start_command: bun run start
      smoke_script: scripts/smoke/pr-smoke.ts
      health_path: /health
```

**Permissions note**: the caller MUST grant at least the same permissions the reusable workflow declares. GitHub fails the workflow with `startup_failure` if the caller is narrower than the reusable.

Each repo declares its own probe set in `scripts/smoke/pr-smoke.ts` (or `.sh`).

## Common to all patterns

- **Vault OIDC** — `hashicorp/vault-action@v3` with the repo's role pulls `SMOKE_ORG_API_KEY` (from `secret/shared`) + any service-specific secrets.
- **Org-scoping is the isolation boundary** — every request the smoke makes carries the smoke-ci-only org's API key. The org has a $1000 credit cap, no Stripe customer, no auto-topup. Cannot accidentally touch other orgs' rows or rack up real bills.
- **Prod DB is safe** — `auth.orgId` filter on every query means the smoke can only see/write smoke-ci-only org's rows.
- **Fast** — target sub-2-minute total wall clock per PR.

## Repository layout

```
ci-workflows/
├── .github/workflows/
│   ├── droplet-localhost-smoke.yml      ← reusable (workflow_call)
│   ├── consumer-prod-smoke.yml          ← reusable (workflow_call)
│   └── app-platform-preview-smoke.yml   ← reusable (workflow_call)
└── examples/
    ├── orchestrator-ci.yml              ← starter for droplet repos
    └── sdk-ci.yml                       ← starter for consumer repos
```

## Branch protection

Per-repo `ci.yml` must be a required status check on `master` branch protection (Linear issue RUN-70). Branch protection is applied LAST — only after every repo has a green PR running through these workflows.

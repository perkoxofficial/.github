# Contributing

## CI is required — `ovh-ci`

Every repo in this org is built by **`ovh-ci`**, our self-hosted CI on OVH
(Dokploy + Mac Mini). There is **no GitHub Actions** — no hosted runners, no
budget for them, and job dispatch is blocked at the account level.

- Push to any branch → `ovh-ci` runs automatically (GitHub webhook).
- A **green `ovh-ci` check is required** before a PR can merge.
- To configure the build, drop a `ci.json` at the repo root. Without it the
  stack is auto-detected (Node, PHP, Gradle, Swift/Xcode, Flutter, etc.).
- Private repos: merge is not branch-protected (GitHub free plan), but
  **nothing deploys without a green `ovh-ci`** — production is gated at
  deploy, not merge.

## Rules

1. Never add `.github/workflows/` — GitHub Actions cannot run here.
2. Run the repo's local CI before you push. Never push a red local CI.
3. If `ovh-ci` fails, read the log and fix the code — don't push a guess.

CI source and operator docs: `perkoxofficial/infra-ci`.

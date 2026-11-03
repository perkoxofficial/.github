# Contributing — rules for every agent & developer

This org builds with **`ovh-ci`** (self-hosted CI) and tracks all work on
**GitHub Issues**. These rules keep every change traceable and stop people and
agents from colliding on the same work.

## The one rule that matters
**Every change traces to an Issue, and every Issue has exactly one owner.**

- No untracked work — if it isn't an Issue, it isn't being done.
- One Issue = one owner = one branch = one PR.
- Claim an Issue (assign yourself / comment "working on this") **before** you
  touch code. An already-owned Issue is off-limits — pick another.

## Board & Issues
1. Open an Issue using a template (bug / feature / task).
2. Claim it and keep its status honest: `todo → in progress → review → done`.
3. Move the card when you change state, not after the fact.
4. Keep discussion in the Issue — not in DMs — so the record lives on GitHub.

## Branches
- Trunk-based: short-lived branches off `main` (or `dev` where used).
- Name: `<type>/<issue>-<slug>` — e.g. `fix/123-offerwall-import`.
- Types: `feat` `fix` `docs` `chore` `refactor` `test` `ci`.
- Delete the branch after merge.

## Commits
- Conventional commits: `type(scope): subject` — imperative, ≤72 chars.
- One logical change per commit. No "wip" piles.

## Pull requests
- One PR = one Issue = one concern. Link it with `Closes #N`.
- Small and reviewable; a large PR needs a review plan in the description.
- **`ovh-ci` must be green** before merge (required on release repos; deploy-gated
  on private repos).
- **Review required** for non-trivial changes; authors never approve their own.

## CI (mandatory — no exceptions)
- The only CI is **`ovh-ci`** (self-hosted OVH + Mac Mini).
- **Never add GitHub Actions** (`.github/workflows/`) — dispatch is blocked at
  the account level and nothing will run.
- Run the repo's local CI before pushing. Never push a red local CI.
- Build config lives in `ci.json` at the repo root. **One owner per repo** edits it.

## Collision & coordination (how we avoid stepping on each other)
1. **One CI dispatcher.** Never deploy a second dispatcher or a second webhook
   for the same repo.
2. **One owner per Issue / repo / `ci.json`.** Claim first, then work.
3. **Never force-push a branch or edit a PR that isn't yours.**
4. **Deploys are serialized** — one deployer at a time through the deploy gate.
5. **Coordinate in the Issue**, not in chat — the record must live on GitHub.
6. Agents: don't edit another profile's files or work; route it through the board.

## Secrets
- All secrets live in **Infisical**. Never in a repo, never in an env var, never
  in chat history.
- Never commit a key/token — gitleaks scans every push.
- Reference secrets by name; rotate on exposure.

## Deploys
- `staging → green → prod → re-test → audit`. No direct prod merges.
- Roll back through the deploy gate — never by hand-editing production.

## Review standards
- Review for correctness, security, and collision risk — not just style.
- Approve only after `ovh-ci` is green and tests pass.

# Repository Handoff Configuration

Project-local handoff/closeout configuration. Fill in only real, confirmed values — never
placeholder paths or commands presented as facts. For any section that does not apply given this
repository's `PROJECT_CLASSIFICATION.md` entry, write `N/A — <reason>` instead of deleting the
section or inventing a value.

Store operational coordinates here, never credentials. If this repository already has equivalent
configuration in `AGENTS.md`, deployment docs, or another canonical file, reference it rather than
duplicate it.

## Repository Identity

- Project name: Summit Learning Center
- Repository root: `/Users/ant/Projects/GitHub/Summit-Learning-Center`
- Canonical remote: `https://github.com/rmz9dkfy5f-pixel/Summit-Learning-Center.git`
- Default branch: main
- Canonical handoff file: none — this repo has no `AGENT_HANDOFF.md`. Nearest equivalents:
  `docs/project/STATUS.md` (current truth), `docs/project/CONTEXT.md` (durable facts/constraints),
  `docs/project/DECISION_LOG.md` (decisions).

## Validation Contract

Discover these from the real toolchain (`package.json`, `pyproject.toml`, `Makefile`, CI config,
etc.) — do not invent commands that were not actually found.

- Install command: N/A — pure static HTML/CSS, no dependencies, no package manifest
- Focused test commands: N/A — no test suite
- Full test command: N/A — no test suite
- Lint/type-check commands: N/A — no toolchain configured
- Production build command: N/A — no build step; `docs/` is served as-is by GitHub Pages
- Runtime smoke test: manual — open the relevant `docs/vX.Y.Z/index.html` (or `docs/index.html`)
  in a browser and check it renders correctly before committing
- Manual or device checks: manual visual/responsive check in a browser; no automated device farm

## Snapshot Contract

Applies to Git-backed classifications (see `PROJECT_CLASSIFICATION.md`). Write `N/A — not
Git-backed` if this repository is Vault-only or Local non-Git.

- Snapshot required: yes
- Naming rule: named after the git tag it was created from (e.g. `v0.3.0`), from the exact tagged
  commit
- Exclusions: none — full working-tree copy, including `.git/`
- Verification method: file-count comparison between source working tree and snapshot copy
- Checksum requirement: no — file-count comparison is sufficient for this small static-site repo;
  revisit if the repo grows large or gains sensitive/binary assets
- Retention policy: keep all snapshots — repo is small (static HTML/CSS), negligible storage cost
- Restore/rollback procedure: prefer `git checkout <tag>` from `origin` (the tag is pushed and
  independently verified); the local snapshot copy is the fallback if git history itself becomes
  unavailable — copy the snapshot directory back over the repository root

### Snapshot Destination by Machine

Only relevant if snapshots are machine-path-dependent (e.g. an external backup drive). Detect the
current machine before resolving a destination:

```bash
scutil --get ComputerName 2>/dev/null || hostname
```

| Machine | Detection | Snapshot destination | Notes |
|---|---|---|---|
| Anthony's MacBook Pro | `scutil --get ComputerName` → `Anthony's MacBook Pro` | `/Users/ant/WorkSync/Projects/RepoBackups/Summit-Learning-Center/` | Confirmed by user 2026-09-10. Note: `/Users/ant/WorkSync/Projects/RepoBackups/Summit Learning Center/` (space, not hyphen) already exists as a stale, unrelated artifact — frozen at the repo's very first commit, predates the `docs/` restructuring, has its own uncommitted local edits. Do not use it; do not merge into it. |

If the current machine does not match any row above, or more than one row could plausibly match,
stop and ask before picking a destination — do not guess or infer a path pattern.

## Deployment Contract

Applies only to the "Git-backed with deployment" classification. Write `N/A — no deployment
target` otherwise.

- Deployment in scope: yes — automatic, via GitHub Pages (no manual deploy step)
- VPS/server alias: N/A — GitHub-managed static hosting, no server this project administers
- Deployment root: `docs/` directory, `main` branch
- Deployment branch or artifact: `main` branch, served from `docs/` (GitHub Pages "Deploy from a
  branch" model)
- Service/container names: N/A — GitHub-managed, no service/container under this project's control
- Read-only health checks: GitHub Pages build status (repo Settings → Pages); HTTP GET on the
  published Pages URL once confirmed (URL not yet confirmed — pre-existing open item, see
  `docs/project/STATUS.md`)
- Log locations: N/A — not accessible; GitHub Pages build logs are the only ones and are
  GitHub-managed
- Rollback target: `git revert` the offending commit on `main` and push — GitHub Pages serves
  whatever `docs/` contains at the current `main` HEAD, so no separate deploy rollback exists
- Actions requiring approval: any push to `main` (GitHub Pages redeploys automatically on push)

## Safety Boundaries

- Protected paths: `docs/v0.0.1/`, `docs/v0.1.4/` (prior versioned site releases — frozen, never
  edit in place; see `docs/project/CONTEXT.md`)
- Secret-bearing files: none known — pure static site, no credentials or API keys in this repo
- Prohibited actions: force-push, rewriting git history, editing/deleting a prior versioned
  `docs/vX.Y.Z/` directory
- Commit/push authorization rule: explicit user approval before every commit/push (matches this
  session's actual practice — plan reviewed and approved before each write)
- Tag/release authorization rule: user decides the exact tag name explicitly each time; never
  inferred from convention alone (this repo's tag history is not strictly sequential — see
  `docs/project/CONTEXT.md`)
- Deploy/merge authorization rule: no separate manual deploy step exists (GitHub Pages deploys
  automatically on push to `main`); merges to `main` require the same explicit approval as any
  other push

# moaiy-com/.github verification map

This directory is the maintained source for verifying the organization overview and governance surfaces in `moaiy-com/.github`. Read this index before driving, then use the matching feature file as the recipe.

## Baseline preconditions

- Checkout root is the `.github` repository (contains `profile/README.md` and `OVERVIEW_HEALTHCHECK.md`).
- `curl` and authenticated `gh` can read `orgs/moaiy-com`.
- Put `control-moaiy-github` on `PATH` and set a unique `MOAIY_VERIFY_EVIDENCE_DIR` for the run.
- Run `control-moaiy-github doctor` and require `doctor: PASS`.
- Do not change organization settings, pinned repos, or live profile metadata during a verification run.

## Driving conventions

- Start every recipe from the baseline state unless its preconditions say otherwise.
- Prefer exact public URLs and file paths over GitHub UI clicks.
- Treat every command as literal. Keep quoted names and flags unchanged.
- Run checks through `control-moaiy-github`.
- Keep proof artifacts; cleanup must not remove them.

## Proof and skip reporting

- Capture the command output and the written proof file, not only a pass line.
- Link proof includes per-URL status codes in `profile-links.proof.tsv`.
- Metadata proof includes the live JSON dump under `org-metadata.json`.
- Record the feature ID used with every artifact.
- Report an unreachable path with the attempted command and the unmet precondition.
- Do not report a skipped entry point as verified through a different path.

## Feature entry contract

Each feature file starts with an H1 title and one paragraph describing the user-visible behavior. It then uses exactly four H2 sections in this order.

1. `Sub-features` lists short IDs with one line for each behavior.
2. `How to get to it (user POV)` lists every user entry point.
3. `Driving it with control-moaiy-github` starts with `Preconditions:` and uses labeled bullets that pair each user action with an exact command and observable result.
4. `Gotchas` lists traps that can waste or invalidate a verification run.

## Features

- [Profile quick links](./profile-quick-links.md) covers public URLs and messaging anchors in `profile/README.md`.
- [Org metadata](./org-metadata.md) covers live description, website, and X/Twitter handle.
- [Security surface](./security-surface.md) covers `SECURITY.md` and the private security contact path from issue templates.
- [Governance templates](./governance-templates.md) covers PR/issue templates, CODEOWNERS, and community files.
- [Profile assets](./profile-assets.md) covers banner and avatar SVG assets referenced by the overview.

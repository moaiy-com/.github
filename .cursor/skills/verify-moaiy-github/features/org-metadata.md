# Org metadata

Org metadata is the live GitHub organization profile fields visitors see beside the overview: description, website, and X/Twitter username. The monthly health check expects them to match product messaging.

## Sub-features

- `meta-description` matches the expected OpenPGP/macOS positioning string.
- `meta-website` points at `https://moaiy.com`.
- `meta-twitter` is `moaiycom`.
- `meta-pins-dump` records current pinned repositories for human review against the preferred order in `OVERVIEW_HEALTHCHECK.md`.

## How to get to it (user POV)

- Visit https://github.com/moaiy-com and read the organization header (description, website, social).
- View pinned repositories on the organization overview.
- Compare against `OVERVIEW_HEALTHCHECK.md`.

## Driving it with control-moaiy-github

Preconditions:

- `control-moaiy-github doctor` reports `doctor: PASS`.
- `gh` can call `GET /orgs/moaiy-com` and organization GraphQL pinnedItems.
- Expected values match the current health-check baseline:
  - description: `Open-source tools for practical OpenPGP workflows on macOS.`
  - blog: `https://moaiy.com`
  - twitter_username: `moaiycom`

- **Read live metadata.** Run `control-moaiy-github check-org-metadata`. Exit code `0` and stdout include `check-org-metadata: PASS`.
- **Inspect JSON.** Open `$MOAIY_VERIFY_EVIDENCE_DIR/org-metadata.json` and confirm description, blog, and twitter_username.
- **Record pins.** Open `$MOAIY_VERIFY_EVIDENCE_DIR/org-pinned.json`. Preferred discoverability order from the health check is `moaiy`, `moaiy-com`, `.github`. If the live order differs, report a failure with the dumped names; do not rewrite the expectation quietly.

## Gotchas

- Changing expected strings in the helper without updating `OVERVIEW_HEALTHCHECK.md` (and usually `profile/README.md`) creates false greens.
- Pin order is product policy, not an API schema guarantee; treat mismatches as verification failures for the monthly checklist. An empty pin list fails the recipe.
- This recipe is read-only. Do not call org update APIs to make the check pass.

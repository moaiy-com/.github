---
name: verify-moaiy-github
description: "Prove the moaiy-com/.github org profile and governance surfaces: profile README links, live org metadata, security contact paths, issue/PR templates, and banner assets. Use when verifying org overview health, link breakage, SECURITY/template regressions, or monthly OVERVIEW_HEALTHCHECK work."
---

# verify-moaiy-github

This skill drives the **moaiy-com/.github** repository the way a maintainer and a GitHub visitor experience it. There is no local app server. The user-facing surface is the organization overview (`profile/README.md` + assets), live org metadata on GitHub, and the governance files GitHub serves to contributors.

Put the helper on `PATH` for the run:

```bash
export PATH="$PWD/.cursor/skills/verify-moaiy-github/scripts:$PATH"
export MOAIY_VERIFY_EVIDENCE_DIR="$PWD/.cursor/skills/verify-moaiy-github/artifacts/latest"
mkdir -p "$MOAIY_VERIFY_EVIDENCE_DIR"
```

## Launch

No daemon. Launch means: work from a clean checkout of this repo, ensure `curl` and `gh` are available, and point evidence at a run directory.

```bash
cd /path/to/moaiy-com/.github
export PATH="$PWD/.cursor/skills/verify-moaiy-github/scripts:$PATH"
export MOAIY_ORG_LOGIN=moaiy-com
export MOAIY_VERIFY_EVIDENCE_DIR="$PWD/.cursor/skills/verify-moaiy-github/artifacts/run-$(date -u +%Y%m%dT%H%M%SZ)"
mkdir -p "$MOAIY_VERIFY_EVIDENCE_DIR"
# optional mirror for the helper default:
ln -sfn "$MOAIY_VERIFY_EVIDENCE_DIR" .cursor/skills/verify-moaiy-github/artifacts/latest
```

Ready when `control-moaiy-github doctor` prints `doctor: PASS`.

Teardown is `control-moaiy-github cleanup` (removes only `MOAIY_VERIFY_SCRATCH` if set). Evidence under `MOAIY_VERIFY_EVIDENCE_DIR` must survive cleanup.

Isolation: this surface is mostly read-only HTTP/`gh` API. Do not mutate org settings during verification. Concurrent runs may share the public org API; they must not write shared local evidence dirs — give each run its own `MOAIY_VERIFY_EVIDENCE_DIR`.

## Doctor

```bash
control-moaiy-github doctor
```

Requires: `profile/README.md`, `SECURITY.md`, `OVERVIEW_HEALTHCHECK.md`, `profile/assets/`, `curl`, `gh`, and a successful `gh api orgs/moaiy-com` read. If anything looks off, run doctor before continuing.

## Drive

Prefer the helper over ad-hoc curls. Feature recipes live in `features/`. Common commands:

```bash
control-moaiy-github check-links
control-moaiy-github check-org-metadata
control-moaiy-github check-security-surface
control-moaiy-github check-templates
control-moaiy-github check-assets
```

Stable handles: exact URLs from `profile/README.md`, org login `moaiy-com`, file paths under `profile/`, `.github/`, and root governance markdown. Do not verify by editing GitHub settings UIs.

## Evidence

Proof files land in `$MOAIY_VERIFY_EVIDENCE_DIR` (also linked as `artifacts/latest` when you create that symlink):

| Command | Artifact |
| --- | --- |
| `check-links` | `link-checks.tsv`, `profile-links.proof.tsv` |
| `check-org-metadata` | `org-metadata.json`, `org-pinned.json` |
| `check-security-surface` | `security-surface.proof.txt` |
| `check-templates` | `templates.proof.txt` |
| `check-assets` | `assets.proof.txt` |

Proof standards:

- Exercise the real visitor path: public HTTPS URLs and the files GitHub renders, not private test stubs.
- Capture the check action and the resulting codes/bodies (TSV/JSON/text), not only a boolean.
- Side effects: this surface is read-only; prove absence of mutation by only using GET/`gh api` reads.
- Treat HTTP `200` and `301` as success for link health (matches `OVERVIEW_HEALTHCHECK.md`).

## Cleanup

```bash
control-moaiy-github cleanup
```

Never kill by process name (nothing is launched). Never delete the evidence directory. Only remove `MOAIY_VERIFY_SCRATCH` when set.

## Helpers

```bash
.cursor/skills/verify-moaiy-github/scripts/control-moaiy-github doctor
.cursor/skills/verify-moaiy-github/scripts/control-moaiy-github check-links
.cursor/skills/verify-moaiy-github/scripts/control-moaiy-github --help
```

The script is executable. Feature map: `features/README.md`. Keep the map honest with `/maintain-verification-skill` as the org overview changes.

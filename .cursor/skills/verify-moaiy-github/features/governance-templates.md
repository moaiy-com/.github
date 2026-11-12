# Governance templates

Governance templates are the default contributor paths shipped by this org standards repo: pull request template, issue forms, CODEOWNERS, code of conduct, and contributing guide.

## Sub-features

- `gov-pr-template` provides `.github/pull_request_template.md`.
- `gov-issue-forms` provides bug and feature issue forms plus `config.yml`.
- `gov-codeowners` provides `.github/CODEOWNERS`.
- `gov-community` provides root `CODE_OF_CONDUCT.md` and `CONTRIBUTING.md`.

## How to get to it (user POV)

- Open a pull request in a repository that inherits these org defaults and see the PR template body.
- Open a new issue and choose Bug report or Feature request (blank issues disabled).
- Read contributing / code of conduct links from the profile README details block.

## Driving it with control-moaiy-github

Preconditions:

- `control-moaiy-github doctor` reports `doctor: PASS`.
- Working tree includes the `.github/` directory from this repository.

- **Confirm required files.** Run `control-moaiy-github check-templates`. Exit code `0` and each required path prints `OK`.
- **Inspect proof.** Read `$MOAIY_VERIFY_EVIDENCE_DIR/templates.proof.txt` and confirm every required relative path is listed as present.

## Gotchas

- Presence proves the org standards files exist in this repo. It does not prove every product repository has inherited them; call that out if the task asked about a specific product repo.
- Do not create a real issue or PR solely to satisfy this recipe when file presence is enough for the mapped surface.

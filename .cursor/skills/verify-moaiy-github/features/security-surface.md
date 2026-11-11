# Security surface

The security surface tells reporters how to disclose vulnerabilities privately and what response targets to expect. Visitors reach it from `SECURITY.md`, the profile Security & Trust section, and the issue template contact link.

## Sub-features

- `sec-email` publishes `security@moaiy.com` as the private channel.
- `sec-targets` states 72-hour acknowledgement and 7-business-day triage targets.
- `sec-issue-contact` disables blank issues and routes security reports to the mailto contact.

## How to get to it (user POV)

- Open https://github.com/moaiy-com/.github/blob/main/SECURITY.md.
- From the org profile README, follow the Security & Trust / full policy link.
- On a repository using org issue templates, open the Security report contact link instead of filing a public issue.

## Driving it with control-moaiy-github

Preconditions:

- `control-moaiy-github doctor` reports `doctor: PASS`.
- Files `SECURITY.md` and `.github/ISSUE_TEMPLATE/config.yml` exist in the checkout.

- **Verify policy + contact config.** Run `control-moaiy-github check-security-surface`. Exit code `0`.
- **Inspect proof.** Read `$MOAIY_VERIFY_EVIDENCE_DIR/security-surface.proof.txt`. It must show the email and both response-target lines from `SECURITY.md`, plus `blank_issues_enabled: false` and the mailto contact from the issue template config.

## Gotchas

- A profile mention of `security@moaiy.com` alone is insufficient; the policy file and issue contact path must also agree.
- Do not open a real security email or public issue as part of verification.
- If a child repository overrides `SECURITY.md`, that override is out of scope for this org-standards recipe; note it and continue with the org file.

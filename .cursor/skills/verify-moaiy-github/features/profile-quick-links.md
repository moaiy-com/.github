# Profile quick links

Profile quick links let a GitHub visitor reach the website, product repo, docs, issues, related org repos, security policy, contributing guide, releases, and social account from the organization overview README.

## Sub-features

- `links-http` returns HTTP 200 or 301 for every public URL listed in the overview.
- `links-local-assets` confirms banner paths referenced by the README exist on disk.
- `links-messaging` confirms hero messaging anchors (site, product repo, security email) remain in the README.

## How to get to it (user POV)

- Open https://github.com/moaiy-com and read the organization profile README.
- Follow any Quick Links / Featured Projects / Security / Community hyperlink from that README.
- Open `profile/README.md` in this repository to edit the same content.

## Driving it with control-moaiy-github

Preconditions:

- `control-moaiy-github doctor` reports `doctor: PASS`.
- Network egress allows HTTPS to github.com, moaiy.com, x.com, and thenounproject.com.
- `MOAIY_VERIFY_EVIDENCE_DIR` points at this run's evidence directory.

- **Check public links.** Run `control-moaiy-github check-links`. Every listed URL prints `OK` and the command exits 0.
- **Inspect proof.** Read `$MOAIY_VERIFY_EVIDENCE_DIR/profile-links.proof.tsv`. Each remote row shows status `200` or `301`; local asset and messaging rows show `present`.
- **Confirm messaging.** The same command also greps `profile/README.md` for `https://moaiy.com`, `moaiy-com/moaiy`, and `security@moaiy.com`. Failure means the overview no longer matches monthly health-check expectations.

## Gotchas

- Some hosts return `301` before `200`. Both are accepted; other codes fail the recipe.
- `https://moaiy.com` sits behind Cloudflare bot challenge (`cf-mitigated: challenge`). Plain `curl` from many agent/CI egress IPs receives `403` even though a browser visitor passes. Capture the status in the TSV and report the unmet network precondition; do not lower the accepted status set to include `403`.
- X/Twitter and Noun Project may rate-limit or geo-block. Capture the status code in the TSV and report the unmet precondition instead of inventing a softer check.
- Do not treat a successful product-repo check as proof that docs or security links still work; the map lists separate URLs.

# GitHub Baseline Checklist

This checklist covers controls that cannot be enforced only by repository files.

## 1) Protect Default Branches

Apply to:

- `moaiy-com/moaiy` -> `main`
- `moaiy-com/moaiy-com` -> `master` (or `main` after migration)

Minimum settings:

- Require pull request before merge
- Require at least 1 approving review
- Require status checks to pass
- Require conversation resolution before merge
- Restrict force pushes
- Restrict branch deletion

## 2) Recommended Repository Security Toggles

- Enable Dependabot alerts
- Enable secret scanning and push protection
- Enable private vulnerability reporting
- Enable code scanning (CodeQL) where applicable

## 3) Default Branch Consistency

Normalize default branch naming:

- Migrate `moaiy-com/moaiy-com` from `master` to `main` when convenient
- Update workflow branch filters after migration

## 4) Enforce Review Ownership

- Keep `CODEOWNERS` up to date
- Require Code Owner review for critical paths when team size allows

## 5) Optional Hardening

- Require signed commits on default branches
- Enable linear history on high-risk repositories
- Restrict who can push to matching branches


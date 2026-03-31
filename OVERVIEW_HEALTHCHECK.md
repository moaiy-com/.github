# Organization Overview Health Check

Run this checklist once per month to keep the public organization overview accurate and useful.

## Monthly Checklist

- Confirm organization profile metadata is correct:
  - Description
  - Website
  - X/Twitter handle
  - Avatar
- Verify pinned repositories are ordered for product discovery:
  1. `moaiy`
  2. `moaiy-com`
  3. `.github`
- Validate all links in `profile/README.md` return HTTP 200 or 301.
- Confirm hero positioning in `profile/README.md` matches the latest website messaging.
- Confirm security contact and response targets are still accurate.

## Verification Commands

```bash
# Profile metadata
 gh api orgs/moaiy-com --jq '{description,blog,twitter_username,updated_at}'

# Pinned repositories count (query only)
 gh api graphql -f query='query { organization(login:"moaiy-com") { pinnedItems(first: 6, types: REPOSITORY) { nodes { ... on Repository { name } } } } }'

# Link checks
 curl -I -L https://moaiy.com
 curl -I -L https://github.com/moaiy-com/moaiy
 curl -I -L https://github.com/moaiy-com/moaiy/tree/main/doc
```

## Change Log

| Date (UTC) | Owner | Changes | Notes |
| --- | --- | --- | --- |
| 2026-03-31 | `@tau-gast` | Baseline created | Initial rollout |

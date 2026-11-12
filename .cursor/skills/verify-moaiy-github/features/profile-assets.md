# Profile assets

Profile assets are the SVG banner and avatar files the organization overview README embeds for light and dark color schemes.

## Sub-features

- `assets-banners` keeps `overview-banner-light.svg` and `overview-banner-dark.svg` as real SVG files.
- `assets-avatar` keeps `org-avatar.svg` as a real SVG file.
- `assets-readme-refs` keeps both banner filenames referenced from `profile/README.md`.

## How to get to it (user POV)

- Visit https://github.com/moaiy-com and see the overview banner image above the README heading.
- Toggle the GitHub UI color scheme to confirm the dark/light source selection.
- Open `profile/assets/` in this repository to edit the artwork.

## Driving it with control-moaiy-github

Preconditions:

- `control-moaiy-github doctor` reports `doctor: PASS`.
- `profile/assets/` contains the committed SVG files.

- **Validate assets.** Run `control-moaiy-github check-assets`. Exit code `0`.
- **Inspect proof.** Read `$MOAIY_VERIFY_EVIDENCE_DIR/assets.proof.txt`. Each asset line shows `OK` with a non-zero byte count. The command also requires both banner filenames to appear in `profile/README.md`.

## Gotchas

- A non-SVG file with the right name fails the `<svg` content check.
- Checking only the light banner is incomplete when the README picture element references dark mode too.
- Visual design QA (colors, crop) is outside this recipe; this map proves presence and reference integrity.

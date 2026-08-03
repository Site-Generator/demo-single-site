# Demo Single Club — site content

This repo holds **Demo Single Club's** website content only: `club.json` and
`images/`. Edit them via [Pages CMS](https://pagescms.org) (see `.pages.yml`)
or directly on GitHub.

Note: this club uses `"siteMode": "single"` (the classic long-scroll page).
The theme, "More tab" text, and quick-link icon fields still show up in the
Pages CMS editor, but the classic template ignores all of them — editing
those fields here has no visible effect on this club's site.

**Do not hand-edit anything under `generator/`.** That folder is a synced
copy of the shared [club-site-generator-core](../club-site-generator-core)
engine, pulled in via `git subtree`. Engine bugs/features are fixed there and
propagated here — a local edit under `generator/` risks a conflict the next
time that sync runs.

**Want a custom design for this club only?** Add a `custom-template/` folder
here at the repo root (sibling to `club.json`, not inside `generator/`),
mirroring `generator/template/`'s structure — for `single` mode that's
`custom-template/page.html`, `custom-template/style.css`, and/or
`custom-template/sections/*.html`. The build uses any file found there
instead of the built-in default, and falls back to the default for anything
you don't override. This is the supported way to diverge from the shared
design; it never conflicts with future engine syncs.

## Building locally

```bash
npm --prefix generator install
CLUB_DATA_DIR=.. CLUB_SLUG=demo-single node generator/build.js
npm --prefix generator run preview   # serves generator/dist/ via wrangler dev
```

## Deploying

This repo's Cloudflare Workers project is configured with:
- Root directory: `generator/`
- Build variables: `CLUB_SLUG=demo-single`, `CLUB_DATA_DIR=..`
- Build command: `node build.js`
- Deploy command: `npm run deploy`

<!-- Cloudflare deploy check: 2026-08-03 -->

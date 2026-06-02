# Onboarding — `legal`

> This repo is a tiny static website, published live via **GitHub Pages** at
> <https://shihabapp.github.io/legal/>, hosting ONE shared bilingual (English + Arabic) Privacy Policy
> and ONE shared Terms & Conditions for the entire `com.moaed.*` app fleet (27 Arabic, RTL, offline apps
> on Android + iOS). Because every app is offline and collects no data, one shared policy is accurate for
> each app, so all apps point at these same two URLs. For the deep reference read **AGENTS.md**; for the
> repo's role/layout map read **ARCHITECTURE.md**. This is not a buildable app — there is no build step.

## 1. What's in here

```
legal/
├── index.html          ← Privacy Policy (bilingual EN + AR), served at /legal/
├── terms/
│   └── index.html      ← Terms & Conditions (bilingual), served at /legal/terms/
├── README.md           ← short note (its terms.html URL is stale; see below)
├── AGENTS.md           ← authoritative agent guide
├── ARCHITECTURE.md     ← repo map / fleet role
├── onboarding.md       ← this file
└── CLAUDE.md           ← imports AGENTS.md for Claude Code
```

Each HTML page is self-contained: a top bar with two language-toggle buttons (English `#b-en`, العربية
`#b-ar`) plus a link to the sibling document, two `<section>`s (`id="en"` and `id="ar"`, the Arabic one
RTL and `hidden` by default), and a tiny inline `setLang(l)` script that swaps which section is shown.
Inline `<style>` only — no external CSS/JS, no framework, no build step. Brand color is green `#1c7a68`.
Each page carries a visible "Last updated" date and the contact email `moaead@gmail.com`.

## 2. How the fleet uses it

- **GitHub Pages** serves these files directly to the public from `main`, root (`/`) path. No custom domain.
- **Canonical live URLs** (referenced by every App Store / Play listing and by in-app Privacy/Terms links):
  - Privacy Policy: <https://shihabapp.github.io/legal/> (from `index.html`)
  - Terms & Conditions: <https://shihabapp.github.io/legal/terms/> (from `terms/index.html`)
- This is **live, legally-operative, user-facing content** — not internal docs. The text must stay TRUE to
  the apps: no data collection, no analytics, no ads, offline.

## 3. How to contribute safely

- Edit `index.html` and/or `terms/index.html`. GitHub Pages republishes automatically on push to `main`.
- Stage **only the file(s) you changed** — never `git add -A`.
- After pushing, wait for the Pages build, then reload both URLs and confirm each renders and both
  languages toggle.
- **Owner-sensitive:** do not change GitHub Pages source branch (`main`) / path (`/`) or disable Pages —
  that takes the published policies offline and can break store listings linking here.

## 4. Gotchas & house rules (each: see AGENTS.md)

- **Keep English and Arabic in sync.** Any wording change in one `<section>` must be mirrored in the other;
  preserve RTL on the Arabic section and the Arabic-Indic date numerals. See AGENTS.md.
- **Bump the "Last updated" date** on any page whose substance you change (both language copies). See AGENTS.md.
- **Never make a false claim** (e.g. "we collect analytics" when the apps don't). See AGENTS.md.
- **Preserve clean URLs:** keep `terms/index.html` so `/legal/terms/` works; don't reintroduce `terms.html`.
  Note `README.md` still references the old `terms.html` path and is slightly stale — trust the URLs above.
- Don't break the `setLang` toggle, the section `id`s (`en`/`ar`), or the privacy↔terms cross-links.

## 5. Getting help / related repos

- Org profile / app index: `shihabapp/.github-private`.
- iOS code-signing storage: `shihabapp/ios-certs` (fastlane `match`; default branch `master`).
- Contact: `moaead@gmail.com`.

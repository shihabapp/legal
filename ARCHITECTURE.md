# ARCHITECTURE — `legal`

A map of what this repo contains and its role in the `com.moaed.*` fleet. For the full agent guide see
**AGENTS.md**; for a contributor walkthrough see **onboarding.md**.

## Role in the fleet

`legal` is the single source of truth for the fleet's **public legal documents**. It is a static site,
published via **GitHub Pages** from `main` at root (`/`), serving one shared Privacy Policy and one shared
Terms & Conditions for all 27 apps. Every App Store / Play listing and every in-app Privacy/Terms link
points at the same two URLs here. Because all apps are offline and collect no data, one shared policy is
accurate for each app.

## Directory layout

```
legal/
├── index.html          # Privacy Policy — served at https://shihabapp.github.io/legal/
├── terms/
│   └── index.html      # Terms & Conditions — served at https://shihabapp.github.io/legal/terms/
├── README.md           # short note (stale terms.html URL; trust ARCHITECTURE/AGENTS instead)
├── AGENTS.md           # authoritative AI/agent guide
├── ARCHITECTURE.md     # this file
├── onboarding.md       # contributor guide
└── CLAUDE.md           # Claude Code entry point; imports AGENTS.md
```

## What each part is for

- **`index.html`** — the Privacy Policy. Bilingual: an English `<section id="en">` and an Arabic
  `<section id="ar">` (RTL, `lang="ar"`, hidden by default). Asserts no data collection, no analytics,
  no ads, offline, no unnecessary permissions; some apps keep simple local preferences on-device only.
- **`terms/index.html`** — the Terms & Conditions. Same bilingual shape. Apps are free; personal,
  non-exclusive, non-commercial license; content provided "as is"; terms may be updated at the same URL.
- Both pages share the same structure: a language toggle bar, two sections, and an inline `setLang(l)`
  script. Inline `<style>` only; brand green `#1c7a68`. Each page shows a "Last updated" date and the
  contact email `moaead@gmail.com`. The two pages cross-link to each other.

## Hosting / publishing model

- **GitHub Pages**, source = `main` branch, path = `/` (root). No custom domain / CNAME.
- Pushing to `main` triggers an automatic Pages rebuild; no build step or framework is involved.
- URLs use the clean directory form (`/legal/terms/` via `terms/index.html`); the old `terms.html` 404s.

## How other repos reference it

- **All 27 `com.moaed.*` apps** (`shihabapp/<slug>-android`, `shihabapp/<slug>-ios`) reference the Privacy
  and Terms URLs in their store listings and in-app links.
- **`shihabapp/.github-private`** — org profile / app index.
- **`shihabapp/ios-certs`** — iOS signing storage (fastlane `match`, branch `master`).

## Change discipline

Editing here changes live, public, legally-operative text. Keep English/Arabic in sync, bump the
"Last updated" date on substantive changes, keep claims true to the apps, and never disable Pages or
change its source. See AGENTS.md for the full guardrails.

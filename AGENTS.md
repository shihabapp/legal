# AGENTS.md — `shihabapp/legal`

> Guide for an AI/LLM agent working in this repo. Read it fully before editing.
> This is an **infra/support** repo, not an app. It holds the **public, user-facing legal documents** for the
> entire `com.moaed.*` app fleet (27 Arabic, RTL, offline apps on Android + iOS).

## What this repo is
A tiny static website, **published live via GitHub Pages**, hosting **one shared bilingual (English +
Arabic) Privacy Policy and one shared Terms & Conditions** that apply to ALL Shihab apps. Because every app
is offline and collects no data, a single shared policy is accurate for each app, so all apps point at these
same two URLs.

GitHub Pages is enabled and **built from the `main` branch, root (`/`) path**. The site is served at
`https://shihabapp.github.io/legal/` (no custom domain / CNAME).

## Live URLs (canonical — these are referenced by the App Store / Play listings)
- **Privacy Policy:** <https://shihabapp.github.io/legal/>  (served from `index.html`)
- **Terms & Conditions:** <https://shihabapp.github.io/legal/terms/>  (served from `terms/index.html`)

Both currently return HTTP 200. Note the terms URL is the **clean** form `/legal/terms/` (the most recent
change was "Clean URL: /terms/ instead of /terms.html"). The old `…/terms.html` now 404s. The repo's
`README.md` still references the old `terms.html` path and is therefore slightly stale — trust the URLs in
this section. The two pages cross-link to each other (privacy ↔ terms) via relative links.

## What lives where (file map)
```
legal/
├── index.html          ← Privacy Policy (bilingual: English + Arabic), served at /legal/
├── terms/
│   └── index.html      ← Terms & Conditions (bilingual), served at /legal/terms/
├── README.md           ← short note (its terms.html URL is stale; see above)
└── AGENTS.md           ← this file
```
How each HTML page is built (both pages share the same shape):
- A top bar with two language toggle buttons — **English** (`#b-en`) and **العربية** (`#b-ar`) — plus a link
  to the sibling document.
- Two `<section>`s: `id="en"` (`lang="en"`) and `id="ar"` (`class="ar"`, `lang="ar"`, RTL, starts `hidden`).
- A tiny inline `<script setLang(l)>` that shows one section and hides the other and flips the active button.
  English shows by default.
- Inline `<style>` only; no external CSS/JS, no build step, no framework. Brand color is green `#1c7a68`.
- Each page carries a visible **"Last updated"** date (currently **25 May 2026** / `٢٥ مايو ٢٠٢٦`) and a
  contact email **moaead@gmail.com**.

### Substance (so you don't contradict it)
- **Privacy:** apps collect **no** personal/device data, transmit/store nothing on a server, work offline,
  request no unnecessary permissions; some apps keep simple local preferences (favorites/display) on-device
  only; no ads, no analytics, no third-party data-collecting SDKs; suitable for all ages/children.
- **Terms:** apps are free; personal, non-exclusive, non-commercial license; no resale/modified redistribution;
  content is educational/devotional, provided "as is" without warranties; use at your own risk; terms may be
  updated at the same URL with a revised date.

## How it's used / who consumes it
- **GitHub Pages** serves these files directly to the public from `main`.
- **App Store and Google Play listings** for all 27 apps reference the Privacy URL (and Terms URL) above. The
  README directs: use the same privacy URL in every app's Play Console listing. In-app "Privacy"/"Terms"
  links also point here.
- This means the text here is **live, legally-operative, user-facing content** — not internal docs.

## How to change it safely
```
# default branch is main; GitHub Pages republishes automatically on push to main
git -C <dir> switch main
# edit index.html and/or terms/index.html
git -C <dir> add <changed file(s)>
git -C <dir> commit -m "legal: <what changed>"
git -C <dir> push origin HEAD:main
```
After pushing, wait for the Pages build, then reload <https://shihabapp.github.io/legal/> and
<https://shihabapp.github.io/legal/terms/> to confirm both render and both languages toggle.

When editing legal text:
- **Keep English and Arabic in sync.** Any wording change in one `<section>` must be mirrored in the other.
  Preserve RTL on the Arabic section (`class="ar"`, `dir`/`lang="ar"`) and the Arabic-Indic date numerals.
- **Bump the "Last updated" date** on any page whose substance you change (both language copies).
- Keep claims TRUE to the apps: the policy asserts no data collection / no analytics / no ads / offline. Do
  not weaken or contradict that unless the apps' actual behavior changed.
- Don't break the `setLang` toggle, the section `id`s (`en`/`ar`), or the privacy↔terms cross-links.
- Preserve the clean URLs: keep `terms/index.html` (so `/legal/terms/` works); don't reintroduce `terms.html`
  without updating every external reference.

## Guardrails — NEVER
- **NEVER** treat this as throwaway docs: editing here changes **live, public, legal** text shown to users and
  cited by App Store / Play listings. Change carefully.
- **NEVER** ship an English-only or Arabic-only change — the two languages must stay equivalent.
- **NEVER** make a privacy/terms claim that is false for the apps (e.g. "we collect analytics" when they don't,
  or vice-versa).
- **NEVER** commit unrelated files. For this task, commit **only** `AGENTS.md`; leave the HTML untouched.
- **NEVER** disable GitHub Pages or change its source branch (`main`)/path (`/`) without intent — that takes
  the published policies offline and can break store listings that link here.

## Glossary
- **GitHub Pages**: free static-site hosting that publishes a repo's files at a `*.github.io` URL; here it
  serves this repo from `main` at `https://shihabapp.github.io/legal/`.
- **Privacy Policy / Terms & Conditions**: the legally-required public documents an app store demands a link to.
- **bilingual / RTL**: pages contain both English (LTR) and Arabic (RTL, `dir="rtl"`) copies, toggled client-side.
- **clean URL**: directory-style URL (`/terms/`) served by an `index.html` inside that folder, instead of `/terms.html`.
- **"Last updated"**: the revision date shown on each page; bump it whenever the legal text changes.

## Cross-references to the fleet
- Referenced by every `com.moaed.*` app and its App Store / Play listing (privacy + terms links).
- Org profile / app index: `shihabapp/.github-private`.
- iOS code-signing storage: `shihabapp/ios-certs` (fastlane `match`; default branch `master`).

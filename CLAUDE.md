# CLAUDE.md

> Context for Claude Code. Read this before changing anything.

## What this is

Landing page for **Zurita Talent**, Diego Zurita's **international** boutique recruiting firm (San Francisco · Europe · Tokyo & Seoul). Global coverage is a core message: a "Live local time" row under the hero CTA and the region cards show SF (America/Los_Angeles), EU (Europe/Berlin) and JP/KR (Asia/Tokyo) with a Working hours / After hours status (Mon–Fri 9–18 local); the Where we hire section has a follow-the-sun chart drawn in the visitor's time zone. All driven by `data-tz`, `data-status-tz` and `data-lane-tz` attributes + the LIVE CLOCKS & COVERAGE JS block. Never claim someone is working "right now" — the status is computed. Since 2026-10-01 it's a firm site, not a CV page: Clients → Services (+ "How we engage": retainer / project / retained search, no prices) → Who we help → Where we hire (SF · EU · JP/KR with live clocks) → Approach (pipeline + stack) → Track record → Reviews → Founder → Contact. Primary CTA is email (`mailto:` with subject "Hiring with Zurita Talent").

Services: recruiting ops setup, sourcing as a service, embedded recruiting, executive search. Audience: startups (Seed–Series C) and scale-ups/enterprise. Diego's own background lives only in the Founder section (official title: Recruitment Lead at Need).

- Live: https://dzs97.github.io (GitHub Pages, repo `Dzs97/Dzs97.github.io`, public)
- Plain HTML + CSS + a little vanilla JS. No build step, no frameworks, no Tailwind.
- Content source of truth: Diego's CV (`diego-zurita-cv.pdf`) and LinkedIn (https://www.linkedin.com/in/diegozuritas/).

## Files

```
index.html          All content + JS (i18n, counters, pipeline tabs, spotlight)
styles.css          All styles, organized by /* ============ SECTION ============ */
img/                diego.jpg (portrait), diego-square.jpg (avatar)
img/tools/          64px tool icons (Ashby, Lever, Juicebox, Notion, Wrangle)
og.png              1200×630 link preview (LinkedIn/WhatsApp/Slack)
sitemap.xml, robots.txt  SEO; JSON-LD (ProfessionalService) lives in <head> — update it if services/regions change
_og/og.html         Template used to render og.png (underscore dir = not published)
diego-zurita-cv.pdf Source CV (content reference only — excluded from the published site via _config.yml)
```

## Conventions

1. **Bilingual EN/ES.** English lives in the HTML; every translatable element has `data-i18n="key"` and its Spanish text goes in the `ES` dictionary at the bottom of `index.html`. When adding or editing text, update both.
2. **Cache busting:** bump `styles.css?v=N` in `index.html` on every CSS change. Same idea for replaced images (e.g. `wrangle.png?v=2`).
3. **Theming:** colors are CSS variables on `:root`, with dark overrides under `@media (prefers-color-scheme: dark)` + `:root[data-theme="dark"]`. Add new colors the same way.
4. **Fonts:** Inter (body), Instrument Serif italic (accents in `<em>`), JetBrains Mono (labels).
5. **Logos:** company logos (Need, Atoms, BairesDev) are inline SVGs using `currentColor`, taken from each company's own site. Greenhouse/LinkedIn icons are inline SVGs from Simple Icons; the rest are PNGs in `img/tools/`.
6. **Testimonials are verbatim quotes** from LinkedIn recommendations — never reword them, never translate them.
7. **Job titles must match LinkedIn** (Founder section).
8. **Firm voice is "we"**; Founder section is first person. The hero strip ("Recruiting experience across") must list exactly the same companies, in the same order, as the Clients section.
10. **Clients section** ("Companies we've hired for" — wording chosen because Need is Diego's employer, not a paying client), in this order: Need (Series A · Venrock), Atoms (ex-CloudKitchens; $1.7B led by a16z, Jul 2026), Treeline (Series A · a16z), Nolla Health (Seed · General Catalyst), Zinq AI (Growth · Stockdale Capital), BairesDev (bootstrapped since 2009 — never raised VC). Logos are inline SVGs from each company's site. To add a client: new `.client` card + matching `.wm` in the hero strip + ES string.

## Workflow

- **Claude makes the commits and pushes** (don't hand Diego git commands). Commit messages in English, conventional style (`feat:`, `fix:`).
- Before pushing, preview locally: `python3 -m http.server 4173` in this folder, check desktop + mobile (375px) + light/dark + ES toggle.
- After pushing, confirm the Pages deploy succeeded:
  `curl -s "https://api.github.com/repos/Dzs97/Dzs97.github.io/actions/runs?per_page=1"`
  GitHub Pages occasionally fails the *deploy* step with a 500 — that's GitHub, not the code. Retrigger with an empty commit.
- `gh` CLI is not installed. Git credentials in the macOS Keychain work for Dzs97 repos.
- Regenerate `og.png` after changing name/role/headline:
  `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --disable-gpu --hide-scrollbars --allow-file-access-from-files --window-size=1200,630 --virtual-time-budget=5000 --screenshot=og.png "file://$PWD/_og/og.html"`

## Communication

Diego speaks Spanish primarily — reply in Spanish, concise, with brief technical reasoning when useful. He's comfortable with git/terminal but isn't a developer.

## Pending / backlog

- **Case study** section (`#case`) is scaffolded but `hidden`. Needs Diego's content: problem → what he did → result for "How I cut interview no-shows by 90%". Remove `hidden` and add ES strings when filled.
- **Sourcing Tracker is listed WITHOUT a link on purpose** — it holds work data and its deployment isn't access-protected. Never link it or name its URL here (this repo is public). Ask Diego whether he has locked it down yet.
- Ideas not done yet: custom domain (e.g. diegozurita.com), analytics (GoatCounter).
- The Need tenure ("3 yrs 2 mos") is hardcoded to match LinkedIn — update occasionally.

# CLAUDE.md — jeffcalvert.net Hugo Site

This file provides shared context for Claude Code and Claude Cowork sessions working on this project.
The canonical decisions log is at /Users/Jeff/Desktop/Migration/NEW_WEBSITE_PROJECT_REFERENCE-2.md.

---

## What This Site Is

**jeffcalvert.net** — author hub and digital legacy repository for Jeff Calvert.
Writer, ultramarathoner, veteran (two tours Iraq), photographer. State College, PA.

"The Rush of It All" (TROIA) is a named project/section within this site, not the top-level identity.
rushofitall.com will redirect to the writing section of this site.

---

## Stack

- **Generator:** Hugo (v0.159.0+)
- **Theme:** Hugo Classless (`themes/hugo-classless/`)
- **Hosting:** Netlify (free tier), auto-deploy from GitHub
- **Domain:** jeffcalvert.net (DNS on Cloudflare; registrar transfer from GoDaddy ~May 25, 2026)

---

## Content Folder Structure

```
content/
  writing/
    essays/          ← polished, finished writing
    roughs/          ← raw journal excerpts / unpolished free-writing
    reports/         ← race reports, expedition write-ups
    projects/
      pandemic-diary/
      desert-storm-dispatches/   ← placeholder, future
      trailrunner-ttp/           ← placeholder, future
  photography/       ← static page(s) linking to SmugMug gallery families
  about/             ← bios, now, colophon, favorites, tools, etc.
  legal/             ← copyright, privacy, accessibility, contact (footer-linked)
```

**Not yet built — slots held:**
- `content/books/` — add when ready
- `content/work/` — add for Nittany WordForge when ready
- `content/blog/` — if launched, most likely as a Substack Section

---

## Navigation

Main nav: Writing | Photography | About
Books and Work are commented out in hugo.toml — uncomment when sections are built.
Footer pages (legal/) are not in main nav.

---

## Front Matter Standard

```yaml
---
title: "Title Here"
date: YYYY-MM-DD          # publication date
written: YYYY-MM-DD       # Roughs only — original journal date
author: "Jeff Calvert"
type: "essay"             # essay | rough | adventure-report | project-entry
rough_number:             # Roughs only — sequence number
project: ""               # populated only for project-entry type
tags: []
draft: false
slug: "url-friendly-title"
source: "https://..."     # migration breadcrumb — original URL
excerpt: "..."            # brief description or opening line
---
```

- `written` and `rough_number` appear only in Rough entries
- `project` populated only for project-entry content
- Front matter does not need to be consistent across all posts — Hugo handles missing fields gracefully
- Obsidian-specific front matter fields pass through Hugo silently — no cleanup needed

---

## Content Migration Status

Source files (un-scrubbed Squarespace/Substack exports) live in:
- `/Users/Jeff/Desktop/Migration/rushofitall/` — Squarespace export (essays, roughs, reports, pandemic diary)
- `/Users/Jeff/Desktop/Migration/substack/posts/` — Substack export

**Known issues in source files (to scrub before migrating):**
- `section` field used instead of `type` (e.g., `section: "adventures"` → `type: "adventure-report"`)
- Missing blank line between front matter close `---` and first heading (appears as `---# Title`)
- Newsletter preamble in Substack files (subscriber welcome, references to previous posts) — remove
- "Written By [Jeff Calvert](url)" lines in body — remove
- Image paths: `../images/filename` won't resolve in Hugo — needs to be `/images/filename` or page bundle approach
- `date` field in Substack exports often missing — check body for date (e.g., "Jeff Calvert · Dec 10, 2023")
- Internal links pointing to old Squarespace/Substack URLs — update to relative Hugo paths eventually

**Test specimens loaded (representative cross-section):**
- `content/writing/essays/throughlines-part-1.md` — essay (from Substack)
- `content/writing/reports/utmb-2017.md` — adventure report (from Squarespace)
- `content/writing/projects/pandemic-diary/pandemic-diary-day-15.md` — rough / project entry (from Squarespace)

---

## Images

Source images live in `/Users/Jeff/Desktop/Migration/rushofitall/images/` (216 files).
Not yet copied to this project. When migrating, copy to `static/images/` and update image paths in content files.

---

## Active Writing Projects

| Project | Notes |
|---|---|
| A Runner's Guide to War (memoir) | War experience through the lens of running. Domain runnersguidetowar.com reserved. |
| Novel | In progress |

---

## Key Decisions

- Two-layer workflow: Obsidian (private drafting) → Hugo content/ (publication gate)
- Photography: static page linking to SmugMug gallery families (not a single SmugMug link)
- Blog: if launched, likely as a new Substack Section, not a Hugo section
- Roughs need a custom template: Chrysalis logo/icon, "Rough #N" label, two dates (Written / Published), visual disclaimer
- rushofitall.com → redirects to /writing/ (or equivalent) — Cloudflare redirect rule, set up after site has structure

---

## Styles

Source of truth: `/Users/Jeff/Desktop/Migration/Styles (draft) for JeffCalvert.md`

**Colors:**
- Headings: `#202060` (Penn/midnight blue)
- Body text: `#000000`
- Background: `#ffffff`
- Links, nav items, tags, breadcrumbs: `#610505` (blood red)
- Link hover: `#8a0707`

**Fonts:**
- Headings: Arial (weight 400, line-height 1.2, letter-spacing 0)
  - H1 2.2rem / H2 1.8rem / H3 1.4rem / H4 1.1rem
- Body: `"Palatino Linotype", Palatino, "Book Antiqua", serif` (weight 400, line-height 1.4)
- Misc/tags: Arial, 1rem, line-height 1, letter-spacing 0.01em
- Base font size: 20px (set on `html`)

**Spacing:** max-width 1800px, side margins 3vw

**CSS files (do not edit theme files directly — override in project):**
- `assets/css/light.css` — color CSS variables
- `layouts/partials/css-overwrite.html` — typography, layout, and other overrides
- `layouts/single.html` — local override of theme's single.html (tags spacing fix)

---

## Launch Strategy — Phased

### Phase 1 (before May 8 — cancel Squarespace)
Minimal placeholder site. Nearly all traffic is on Substack; this just establishes the domain.

- [x] Homepage (`content/_index.md`) — under-construction message, Substack link, signup embed ✅
- [x] About page — bare bio ✅
- [ ] Set up GitHub repo and push site
- [ ] Connect to Netlify (auto-deploy from GitHub)
- [ ] Confirm live at jeffcalvert.net
- [ ] Configure rushofitall.com → jeffcalvert.net redirect in Cloudflare
- [ ] Cancel Squarespace

### Phase 2 (no deadline — after Squarespace closed)
- [ ] Rationalize tags taxonomy (~6-8 canonical values) — required before content migration
- [ ] Restructure content/ to final target (rushofitall/, pandemic-diary/ as siblings under writing/)
- [ ] Migrate Squarespace and Substack content (scrub source files first)
- [ ] Build Roughs special template (Chrysalis logo, rough_number, dual dates, disclaimer)
- [ ] TROIA vs. general template differentiation
- [ ] Full about sub-pages (Now, Colophon, My Tens, etc.)
- [ ] Photography page with SmugMug family links
- [ ] Legal/footer pages (copyright, privacy, contact)
- [ ] Copy images to static/images/, update paths

### Phase 3 (future)
- [ ] Facebook backlog salvage (from JSON export)
- [ ] Strava pipeline decision
- [ ] Syndication (Notebook → Bluesky, etc.)

---

## Session Log

### 2026-04-23
- Added homepage (`content/_index.md`) — under-construction message, Substack link, subscribe embed
- Added bare about page bio
- Updated CLAUDE.md to reflect phased launch strategy (Phase 1 before May 8)
- Phase 1 remaining: GitHub repo → Netlify deploy → rushofitall.com redirect → cancel Squarespace

### 2026-04-01
- Confirmed Hugo site skeleton already in place at `/Users/Jeff/Desktop/jeffcalvert.net/`
- Established CSS strategy: override theme via `assets/css/light.css` and `layouts/partials/css-overwrite.html` (never edit theme files directly)
- Applied Jeff's color palette, fonts, and sizing from style reference doc
- Created `layouts/single.html` override to fix tags spacing (space between "Tags:" and first tag)
- Removed h2 decorative underline (theme default, not wanted)
- Centered content page title (h1) and date
- Fixed active nav item: removed bold (kept underline, increased offset to clear descenders)

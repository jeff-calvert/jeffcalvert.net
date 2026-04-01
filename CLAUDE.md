# CLAUDE.md — jeffcalvert.net Hugo Site

This file provides shared context for Claude Code and Claude Cowork sessions working on this project.
The canonical decisions log is at /Users/Jeff/Desktop/Migration/NEW_WEBSITE_PROJECT_REFERENCE.md.

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

## Open Tasks (site build)

- [ ] Build home page (content/_index.md)
- [ ] Build about section pages (bio, now, colophon, etc.)
- [ ] Build photography page with SmugMug links
- [ ] Build legal/footer pages (copyright, privacy, contact)
- [ ] Custom Roughs template (layout for rough_number, written/published dates, disclaimer)
- [ ] Copy images to static/images/ and update paths
- [ ] Set up Netlify deployment (requires GitHub account)
- [ ] Configure rushofitall.com redirect on Cloudflare
- [ ] Full content migration (scrub source files, then copy to content/)

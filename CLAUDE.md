# CLAUDE.md — jeffcalvert.net

Single canonical reference for this site. Replaces the prior split between `CLAUDE.md` and `NEW_WEBSITE_PROJECT_REFERENCE-2.md` (which is being archived).

Updated in place as decisions are made; changelog at bottom records significant shifts.

---

## The Person

**Jeff Calvert** — writer, runner, ultramarathoner, veteran (two tours Iraq), photographer, amateur philosopher. Lives in State College, PA (near Penn State / Mt. Nittany). Writing spans personal essays, adventure/race reports, war memoir, and fiction.

---

## What This Site Is

**jeffcalvert.net** — author hub and digital legacy repository. Contains everything Jeff publishes online; intended to outlive any specific platform.

"The Rush of It All" (TROIA) is a named project/section within this site, not the top-level identity. rushofitall.com redirects to jeffcalvert.net (target will be `/writing/rushofitall/` once that section exists).

**Hub model rationale:**
- Multiple active projects (memoir, novel) that don't fit cleanly under TROIA
- Digital-legacy ambition wants a person-named container, not a brand container
- Jeff Calvert identity (~1000 FB followers) ≈ TROIA identity (~200 Substack)
- Author name will appear on book covers; person-as-hub is professionally legible
- TROIA brand continues — it just gets a parent

**Content flow:** New content originates in Hugo and syndicates outward. Hugo is canonical. Existing content on Substack/Squarespace migrates in. SmugMug stays as photo repository.

---

## Stack & Infrastructure

- **Generator:** Hugo (v0.159.0+)
- **Theme:** Hugo Classless (`themes/hugo-classless/`) — chosen for simplicity, easy customization
- **Hosting:** Netlify (free tier). Currently manual deploy; auto-deploy from GitHub pending GitHub account-flag clearance.
- **Repo:** github.com/jeff-calvert/jeffcalvert.net (main branch)
- **Domain:** jeffcalvert.net — DNS on Cloudflare. Registrar transfer GoDaddy → Cloudflare ~May 25, 2026.
- **Email:** jeff@jeffcalvert.net and jeff@rushofitall.com both forward via Cloudflare Email Routing → jacalvsc@gmail.com. Gmail Send As configured for both. Google Workspace cancelled.
- **Other domains kept (all on Cloudflare):** rushofitall.com, runnersguidetowar.com (memoir), nittanywordforge.com, writingtherush.com (optional), lucascalvert.com / lucasorion.com / orionseye.com (held for son).
- **Domains let lapsed / for sale:** jacalvert.com, jcalvertonline.com, steadythere.com.

---

## Site Structure

### Top-level navigation
| Item | Status |
|---|---|
| Writing | Active |
| Photography | Static page (links to SmugMug families) |
| About | Active (bare for now) |
| Notebooks | Placeholder — off navbar until populated |
| Books | Placeholder — off navbar until populated |

Footer (not in main nav): Site pages (legal/utility), Contact.

### Target content folder structure (Phase 2)

```
content/
  writing/
    rushofitall/                   ← all TROIA content: essays, roughs, reports, WtR
    pandemic-diary/                ← PD entries; browsed via section index, no format taxonomy
    desert-storm-dispatches/       ← placeholder, future
    poetry/                        ← placeholder, future
    stories/                       ← placeholder, future
  notebooks/                       ← placeholder; off navbar until populated
    socials/
    field-notes/
    run-log/
    relics/
  photography/                     ← static page(s) linking to SmugMug families
  about/
    my-tens/                       ← subsection with own _index.md; no format taxonomy
    (bios, now, colophon, canon, identity, tools, blogroll, etc.)
  books/                           ← placeholder
  site/                            ← footer pages: copyright, privacy, accessibility, contact
```

**Notes:**
- `rushofitall/` is a sibling to `pandemic-diary/`, not a parent — each writing project gets its own URL space under `/writing/`
- Writing the Rush posts live in `rushofitall/` with `format: writing-the-rush` — no separate section
- Posts are page bundles: each post is a folder containing `index.md` plus that post's images (see Images section)
- Current `content/` still uses old structure (`essays/`, `roughs/`, `reports/`, `projects/pandemic-diary/`, `legal/`); restructure happens at content migration

### Photography
SmugMug (~$250/year) is justified for gallery volume. The site's photography section will be a small set of pages with direct links to SmugMug gallery families (Running, Nature, etc.) — not a single front-door link. Bringing SmugMug up to speed is a separate future project.

---

## Front Matter Standard

```yaml
---
# Identity
title: "Title Here"
subtitle: ""                             # optional — custom param
slug: "url-friendly-title"               # optional — only when URL should differ from filename

# Dates
date: YYYY-MM-DD                         # publication date
written: YYYY-MM-DD                      # optional — original date for backdated pieces

# Status & classification
draft: false
format: "essay"                          # essay | rough | adventure-report | writing-the-rush | review
                                         # OMIT for Pandemic Diary entries and My Tens pages
pd_day:                                  # only for Pandemic Diary entries — drives "Pandemic Diary - day N" subtitle
weight:                                  # optional — manual ordering; default is date-descending

# Discoverability
summary: "..."                           # 1-2 sentences; serves as both human teaser and SEO meta
tags: []                                 # rationalized canonical list

# Assets (page bundle — references resolve relative to the post folder)
featured_image: "hero.jpg"               # optional — present when post has a hero/thumbnail

# Migration
aliases:                                 # original URLs that should redirect to this post
  - /posts/original-slug
---
```

**Notes:**
- Field order doesn't affect Hugo behavior — grouped above for human readability
- `author` is set once in `hugo.toml` as a site default — not repeated in each file
- `subtitle`, `written`, `featured_image`, `pd_day` are custom params; Hugo treats any non-reserved field as a param automatically
- `summary` overrides Hugo's auto-generated summary (first ~70 words). Themes commonly use it for the SEO `<meta name="description">` tag too — so one well-written 1-2 sentence summary serves both purposes.
- Add an explicit `description:` field only on the rare post where SEO meta should differ materially from the human summary (otherwise leave it out)
- `aliases` drives the redirect map for old Squarespace/Substack URLs (Hugo emits redirects in the rendered site; Netlify handles them)
- Front matter does not need to be consistent across all posts — Hugo handles missing fields gracefully
- Obsidian-specific front matter fields pass through Hugo silently — no cleanup needed
- `type` field (Hugo reserved) controls template selection only — generally not needed; Hugo derives it from section. Set explicitly only if a piece needs a layout different from its section default.

### Roughs — additional display requirements
Roughs have a distinctive header that requires its own Hugo template:
- Chrysalis logo/icon
- Static label: **A Rough**
- Two dates displayed: *Written: YYYY-MM-DD* and *Published: YYYY-MM-DD*
- Visual disclaimer framing signaling unpolished content (footer block: "Rough (adj): not perfected; a disorderly, unrefined, or unfinished state" + "More about Roughs" link)

No sequence numbering. Roughs are published topically, not chronologically — numbering implied an order that didn't reflect anything meaningful. Ongoing content type — large backlog of journal excerpts to publish over time.

### Pandemic Diary — display requirements
Pandemic Diary entries get a standard subtitle directly under the post title: **(Pandemic Diary - day N)**, where the "Pandemic Diary" portion links to the section index. The day number comes from the `pd_day` front matter field. Implemented as a conditional in the section template (or a dedicated PD template), parallel to the Roughs special template.

---

## Taxonomy

Hugo's two taxonomies in use:

| Taxonomy | Purpose | Index pages |
|---|---|---|
| `format` | Genre/format of the piece | `/format/essay/`, `/format/rough/`, etc. |
| `tags` | Topical tags | `/tags/running/`, `/tags/war/`, etc. |

### Format values
| Value | Description |
|---|---|
| `essay` | Polished, finished writing |
| `rough` | Raw journal excerpts / unpolished free-writing |
| `adventure-report` | Race reports, expedition write-ups |
| `writing-the-rush` | Meta posts about writing process / project updates (lives in `rushofitall/`) |
| `review` | Book/gear/film reviews (placeholder, future) |

**No `format` value:** Pandemic Diary entries (browsed via section index), My Tens pages.

### Tags
~6-8 canonical topical tags. Rationalization happens *after* Squarespace migration but *before* Substack migration.

- Squarespace tags are ignored entirely — they were used for process tracking, not topical tagging. Squarespace posts migrate without `tags:`; we backfill from spreadsheet later.
- Substack tags are real topical tags and need a rationalized canonical list before Substack content migrates in.

### Tag scope note
Hugo tags are global by default — a `running` tag on a Pandemic Diary entry and on an essay both appear on `/tags/running/`. If project-internal organization is needed later, options are: custom taxonomy (e.g., `project_tags`), template filtering, or no internal tags. Likely sufficient to use main tags only for most projects.

---

## Content Migration Plan

**Source of truth per bucket:**

| Bucket | Authoritative source |
|---|---|
| Squarespace — all posts and pages (Essays, Roughs, Adventure Reports, Pandemic Diary, Strava Photos) | Full-site WXR XML export at `Migration/files to migrate/squarespace xml exports/` |
| Substack posts | Substack native export (Settings → Exports) — not yet run |

**Approach:**
- XML → Hugo Markdown via conversion script that reads each `<item>`, applies the front matter schema above, populates fields from XML and from a companion spreadsheet
- Each post becomes a **page bundle**: `content/writing/<section>/<slug>/index.md` with images colocated in the same folder
- Original Squarespace URL paths (XML `<link>` field) become `aliases:` entries to drive redirects
- Squarespace migration runs first, untagged. Tag taxonomy gets rationalized after. Then Substack migration adds tagged content. Squarespace tags backfilled at the end from spreadsheet.
- Dreamer-app exports (`Migration/files to migrate/squarespace vDreamer/` and `substack vDreamer/`) are reference/sanity-check only — XML is cleaner and more complete.

**Internal link normalization (script requirement):**

The XML export was run from `rushofitall.squarespace.com` (after the rushofitall.com domain was moved). Inline body links to other posts on Jeff's site appear in any of these forms across exports past and present:

- `https://rushofitall.com/...`
- `https://www.rushofitall.com/...`
- `https://rushofitall.squarespace.com/...`
- (and `http://` variants of each)

The conversion script must:
1. Detect any `<a href>` in body HTML matching any of these host prefixes
2. Strip the host, leaving the path (e.g., `/posts/another-post`)
3. Look up the path in the slug map (built during conversion as all items are processed) → rewrite to the new Hugo URL (e.g., `/writing/rushofitall/another-post/`)
4. If a referenced path isn't found in the map, leave it as-is and log a warning for manual review

This catches cross-references between Jeff's own posts so they survive the migration as working internal links, not as redirects-through-aliases (which would work but adds latency and is fragile if the alias map ever changes).

**Body content cleanups (script requirements):**
- Strip any inline "(Rough #N)" or "Rough #N" markers from body text and excerpts — the new template uses a static "A Rough" label, not a sequence number, so old inline references would dangle. Regex catches both parenthesized and bare forms.
- Strip the Squarespace footer block when present: the `<hr><div class="sqs-html-content">...Rough (adj): not perfected...More about Roughs...</div>` block is now rendered by the Hugo template, not embedded in body content.

**Spreadsheet columns (companion to XML):**
`slug | title | date | written | format | pd_day | tags | summary | has_hero (Y/N) | extra_aliases`

**File:** `Migration/Content Tracker - Squarespace for Hugo.csv`

**Precedence:** the spreadsheet is authoritative for `slug`, `title`, `summary`, and `format`. Jeff has edited these (cleaned up clumsy slugs, refined summaries, etc.) — they override the XML values. The XML is authoritative for body content, dates, image URLs, original URL paths (for primary alias), and `_thumbnail_id` → hero image lookup. Posts are matched between sources via the **original Squarespace slug** in the XML's `<wp:post_name>` field (recorded in the spreadsheet so the script can join the two).

The XML provides body content, dates, summary candidates, primary alias, and the hero image filename automatically. The spreadsheet supplies the authoritative editorial fields plus what XML can't give cleanly: rationalized tags (when ready), edited summary, written date for backdated pieces, pd_day, hero yes/no (sanity-check against XML extraction), any extra aliases.

**Substack migration:** deferred until Squarespace migration is complete and Substack-internal links pointing at old Squarespace URLs have been updated to new Hugo URLs.

---

## Images

**Layout: page bundles.** Each post is a folder containing `index.md` plus its images. This solves the Squarespace filename-chaos problem because every post has its own image namespace — no global filename collisions, so we can rename freely during conversion.

```
content/writing/rushofitall/boston-marathon-bombing/
  index.md
  hero.jpg
  image-01.jpg
  image-02.jpg
```

**Conversion-time naming:**
- Featured/thumbnail (from XML `_thumbnail_id`) → `hero.jpg`
- Inline images in order of appearance → `image-01.jpg`, `image-02.jpg`, ...
- Original Squarespace filenames discarded (they were inconsistent, often opaque)

**Markdown image references** (relative within the bundle):
```markdown
![](hero.jpg)
![](image-01.jpg)
```

**Source resolution:** XML carries full-resolution image URLs on `images.squarespace-cdn.com`. The conversion script downloads each image into the post's bundle folder during migration. The **hero image is identified automatically** from the XML `<wp:postmeta>` `_thumbnail_id` → matching `<wp:post_id>` attachment URL — no spreadsheet input needed beyond a Y/N sanity-check column.

**Image quality:** Squarespace images are 1500px medium-quality JPEGs (Photos.app exports). Adequate for a reading-focused site — not worth replacing with originals.

**Captions:** Squarespace caption markup is inconsistent in the XML. Conversion script will handle the common cases (figcaption tags); edge cases get cleaned up post-migration.

**Alt text:** XML has empty `alt=""` on virtually every image (Squarespace didn't capture alt). Default during migration:
- Hero image alt = post title (descriptive enough as a baseline)
- Inline images alt = empty for now

A future accessibility pass will backfill descriptive alt text on high-traffic posts. If you want to write hero alts up front, add an `alt` column to the spreadsheet.

**Existing Dreamer image folder:** 214 files in `Migration/files to migrate/squarespace vDreamer/images/`. Reference only; XML re-download is cleaner.

---

## Templates / Branding

- **TROIA template:** all content in `content/writing/rushofitall/` (essays, roughs, adventure-reports, writing-the-rush)
- **General template:** all other pages
- Within the TROIA template, Roughs get additional distinctive elements (Chrysalis logo, dual dates, disclaimer) via conditional on `format: rough`

---

## Styles

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

## Workflow

**Two-layer content pipeline:**
1. **Obsidian** — private drafting layer. All drafts and works-in-progress.
2. **Hugo project / GitHub** — public layer. Moving a file from Obsidian to `content/` is the publication gate.

Obsidian and Hugo project are kept as separate folders (deliberate — clean separation between private workspace and public site).

**Claude tool roles:**
- **Claude Chat:** strategy, content questions, longer-form planning conversations
- **Claude Code (this tool):** Hugo build, template editing, content migration, deployment
- **Claude Cowork:** file organization, batch tasks
- **MEMORY.md** (auto-generated): compressed working state, persists across sessions

---

## Active Writing Projects

| Project | Notes |
|---|---|
| **A Runner's Guide to War** (memoir) | War experience told through the lens of running as a lifetime throughline. Fits within TROIA conceptually. Domain runnersguidetowar.com reserved. See essay "Throughlines (Part 1)" on Substack for approach/angle. |
| **Novel** | In progress, details TBD |

---

## Strava — Separate Puzzle

Jeff posts to Strava daily with a required photo from each run as part of a pay-attention practice. This constitutes a meaningful body of work (field notes + photos). Distinct from other repatriation because it's ongoing, not just a backlog. Open questions: What content type does a Strava post become? (Notebook entry? `run-log` type? Adventure-report?) Ongoing pipeline (Strava API) or periodic salvage? Deferred — decide after Notebook section exists.

---

## Launch Phases

### Phase 1 — COMPLETE ✅ (2026-04-23)
- [x] Homepage — under-construction message, Substack link, signup embed
- [x] About page — bare bio
- [x] GitHub repo — github.com/jeff-calvert/jeffcalvert.net
- [x] Netlify deploy (manual) — magical-liger-a6891f.netlify.app
- [x] jeffcalvert.net live with HTTPS
- [x] rushofitall.com → jeffcalvert.net redirect (Cloudflare, 301)
- [x] Squarespace cancelled
- [x] Google Workspace cancelled
- [x] Email forwarding + Gmail Send As (jeffcalvert.net, rushofitall.com)
- [ ] Wire up GitHub → Netlify auto-deploy (pending GitHub support clearing account flag)

### Phase 2 — In Progress (no deadline — Squarespace closed)
**Migration order matters — this list is in dependency order:**
- [x] Restructure `content/` to target layout (`rushofitall/`, `pandemic-diary/` siblings under `writing/`; `legal/` → `site/`)
- [x] Build XML → Hugo conversion script (page bundles, alias generation, hero image extraction)
- [x] Migrate Squarespace content (untagged for now) — 131 posts, 221 images live
- [ ] Update rushofitall.com Cloudflare redirect to preserve path (`/posts/X` → `/writing/rushofitall/X`)
- [ ] Backfill 14 Strava activity URLs (see `Migration/Strava Links to Backfill.md`)
- [ ] Rationalize tags taxonomy (~6-8 canonical values)
- [ ] Backfill Squarespace `tags:` from spreadsheet
- [ ] Migrate Substack backlog (with tags; update Substack-internal links to new Hugo URLs first)
- [ ] Correct 3-4 Substack posts misclassified as essays (actually Writing the Rush)
- [ ] Build Roughs special template (Chrysalis logo, dual dates, disclaimer)
- [ ] Build Pandemic Diary subtitle treatment ("Pandemic Diary - day N" under post title)
- [ ] TROIA vs. general template differentiation
- [ ] Full about sub-pages (Now, Colophon, My Tens, etc.)
- [ ] Photography page with SmugMug family links
- [ ] Site footer pages (copyright, privacy, accessibility, contact)
- [ ] Update Substack reader account email (rushofitall.com → jeffcalvert.net) — handles ~90% of subscriber migration
- [ ] Accessibility pass: backfill image alt text on high-traffic posts

### Phase 3 — Future
- [ ] Facebook backlog salvage (from JSON export)
- [ ] Strava pipeline decision and implementation
- [ ] Syndication (Notebook → Bluesky via AT Protocol)
- [ ] NittanyWordForge page under About (services)
- [ ] Bring SmugMug up to speed

### Near-term Infrastructure
- [ ] Transfer jeffcalvert.net registrar GoDaddy → Cloudflare (~May 25)

---

## Key Principles

- Two-layer workflow: Obsidian (private) → Hugo content/ (publication gate)
- Hugo is canonical; everything else syndicates from it
- Photography: static page linking to SmugMug family galleries, not a single front-door link
- Blog (if launched): likely as a new Substack Section, not a Hugo section
- Front matter consistency across files is not required — Hugo handles missing fields gracefully
- Design principle: *broad and easy navigation at the top level, with clear pathways into the depths*

---

## Changelog

**2026-05-01 — Squarespace conversion working; ready to promote**
Built `scripts/migrate_dry_run.py`. Reads the WXR XML and the spreadsheet CSV, matches 131/131 rows by normalized title (5 intentional renames handled via `TITLE_OVERRIDES_RAW`; 2 deliberate skips: TTP test post and Strava Photos entry). Converts each post to a Hugo page bundle in `Migration/_dry_run_output/content/writing/{rushofitall,pandemic-diary}/<slug>/index.md`. Image dedup logic: when XML `_thumbnail_id` matches an inline image by filename root, the inline (full-resolution `?format=original`) URL is downloaded as `hero.jpg` and that body reference points at `hero.jpg` — one file serves both as featured image and inline embed at its original body position. Other inline images get sequential `image-NN.jpg` names. Body cleanups in script: strips `(Rough #N)` markers, Squarespace Roughs footer block, Pandemic Diary subtitle headings (now template-driven), `[caption ...]...[/caption]` shortcodes, leading/trailing decorative `<hr>` rules. Internal cross-references (`rushofitall.com`, `www.rushofitall.com`, `rushofitall.squarespace.com` host forms) rewritten to root-relative Hugo URLs via slug map. YouTube embedly iframes converted to Hugo's built-in `{{< youtube VIDEO_ID >}}` shortcode (one such embed in entire corpus). SSL handled via `certifi`. Image-download verified for sample post (christmas-letter-from-iraq-2003: hero + 3 inline). Identified 14 PD posts where original Squarespace text `[ Strava activity link ]` was never an actual `<a href>` in the export; checklist at `Migration/Strava Links to Backfill.md` for manual backfill against the live Squarespace site (Jeff will edit the live Hugo files directly post-promotion).

**2026-05-01 (continued) — Squarespace content promoted to live site**
Steps 1-5 completed: image gating removed, write mode run (131 posts, 221 images), old Phase 1 placeholder structure (`essays/`, `roughs/`, `reports/`, `projects/`) deleted, new `rushofitall/` and `pandemic-diary/` bundles copied into `content/writing/`, `static/_redirects` generated (131 Netlify 301 rules from front matter aliases), clean Hugo build verified (zero errors, 145 pages, 221 non-page files).

Pending (manual steps):
- Deploy: drag `public/` to Netlify
- Update rushofitall.com Cloudflare redirect to path-preserving (`/*` → `jeffcalvert.net/:splat`)
- Backfill 14 Strava activity URLs per `Migration/Strava Links to Backfill.md`

**2026-04-29 — Doc unification + migration plan refinements**
Merged `NEW_WEBSITE_PROJECT_REFERENCE-2.md` (438 lines, planning/strategy) into `CLAUDE.md` (was 207 lines, engineering). Single canonical source going forward. Decisions made in this session:
- **Front matter standard:** switch from `type` to `format`, `excerpt` → `summary`. Drop `author`, `source`, `project`, `description` (use `summary` only; add ad-hoc `description` per-post when SEO meta needs to differ materially). Add `aliases:` (drives redirect map from XML `<link>`), `featured_image:` (XML thumbnail extraction), and `pd_day:` (Pandemic Diary day number, drives standard "(Pandemic Diary - day N)" subtitle). Field order grouped for readability — doesn't affect Hugo behavior.
- **Image strategy:** page bundles (per-post folder) chosen over flat `static/images/`, because Squarespace filenames are inconsistent and bundles give per-post namespace for clean renames during conversion. Conventions: `hero.jpg` for the featured image, `image-01.jpg`, `image-02.jpg`, ... for inline. Hero identified automatically via XML `_thumbnail_id`. Alt text default = post title for hero, empty for inline; future accessibility pass to backfill.
- **Content migration approach:** XML-driven (replaces Dreamer exports as authoritative source). Squarespace migrates first, untagged. Tag taxonomy rationalized after. Substack migrates with tags. Squarespace tags backfilled from spreadsheet at end.
- **Folder rename:** `legal/` → `site/`.
- **Squarespace tags ignored entirely** — they were process tracking, not topical.
- **Image quality:** keep 1500px Squarespace exports — not worth replacing with Photos.app originals.
- **Internal link normalization:** conversion script must rewrite cross-references between Jeff's own posts (links from one post body to another). Recognize all host forms — `rushofitall.com`, `www.rushofitall.com`, `rushofitall.squarespace.com` — strip host, look up path in slug map, rewrite to new Hugo URL.
- **Roughs renumbering retired:** dropped `rough_number` from front matter and spreadsheet. Numbers implied a sequence that didn't reflect anything meaningful (Roughs are published topically, not chronologically). Template label changes from "Rough #N" to a static "A Rough." Conversion script strips inline "(Rough #N)" markers from body content.
- **Reference doc retired** to `Migration/_archive/`.

**2026-04-23 — Phase 1 complete**
Site live at jeffcalvert.net with HTTPS. Homepage and about page built. GitHub repo created. Netlify connected via manual deploy. rushofitall.com redirect live. Squarespace cancelled. Google Workspace cancelled. Email infrastructure complete (Cloudflare Email Routing + Gmail Send As).

**2026-04-09 — Front matter & site structure finalized**
Rushofitall is a sibling section to Pandemic Diary under `/writing/` (not a flat parent). Each writing project gets its own URL space. Writing the Rush is a `format` value within `rushofitall/` (Option A), not a separate section. Notebooks confirmed as top-level placeholder for micro-form content (Socials, Field Notes, Run Log, Relics). My Tens is a plain subsection under `/about/`. `format` taxonomy replaces `type` field. `author` moves to `hugo.toml`. Format values finalized: `essay`, `rough`, `adventure-report`, `writing-the-rush`, `review`. `project-entry` dropped. Pandemic Diary entries carry no `format` value.

**2026-04-08 — Repatriation framing**
jeffcalvert.net is canonical origin for new content; social platforms receive syndicated copies. Repatriation of existing content is a set of discrete one-time salvage operations. Facebook backlog identified as largest target. Strava flagged as ongoing puzzle (deferred).

**2026-04-01 — Hugo build started**
Hugo site skeleton in place. CSS strategy: override theme via `assets/css/light.css` and `layouts/partials/css-overwrite.html` (never edit theme files directly). Applied color palette, fonts, sizing. `layouts/single.html` override for tags spacing. Removed h2 decorative underline. Centered h1 and date.

**2026-03-31 — Architecture confirmed (Sessions 4-5)**
Content folder structure resolved. Two-layer Obsidian/Hugo workflow confirmed. Photography as static page linking to SmugMug families. Blog as cross-cutting (likely future Substack Section). Comprehensive terminology glossary built.

**2026-03-27 — Domains & email (Session 3)**
All kept domains transferred to Cloudflare (registrar + DNS) except jeffcalvert.net (DNS only; registrar transfer pending 60-day lock). Email infrastructure: jeff@jeffcalvert.net and jeff@rushofitall.com forward via Cloudflare Email Routing → Gmail.

**2026-03-25 — Foundation (Sessions 1-2)**
Initial strategic direction set: hub model (jeffcalvert.net), TROIA as named project within. Hugo + Netlify + Cloudflare stack. Hugo Classless theme.

---

## Reference Documents

- **Glossary:** `/Users/Jeff/Desktop/Migration/GLOSSARY_site_terminology.md` — Hugo, Substack, Netlify, Cloudflare, workflow terminology. Update in place as new terms arise.
- **Archived:** `/Users/Jeff/Desktop/Migration/_archive/REFERENCE-pre-2026-04-29.md` (was `NEW_WEBSITE_PROJECT_REFERENCE-2.md`)

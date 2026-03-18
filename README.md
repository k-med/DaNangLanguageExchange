# Da Nang Language Exchange

Official website source for the Da Nang Language Exchange community.

This repo contains a bilingual Hugo site for publishing meetup details, beginner resources, conversation topics, and general club information in English and Vietnamese.

## Stack

- Hugo
- PaperMod theme
- Markdown content
- Cloudflare Pages deployment

## Repository Layout

- `hugo.toml`: main site configuration, language settings, menus, and global params
- `content/`: site content in Markdown
- `content/events/`: meetup pages and event listings
- `content/resources/`: learning resources and starter materials
- `content/topics/`: weekly discussion topics and prompt pages
- `layouts/`: site-specific templates that override the theme
- `i18n/`: translation strings used by custom templates
- `assets/css/extended/custom.css`: custom styling
- `static/`: static files such as images
- `themes/PaperMod/`: theme submodule

## Local Development

Prerequisites:

- Git
- Hugo Extended, version `0.120.0` or newer recommended

Start the local dev server:

```bash
hugo server -D
```

The site will be available at `http://localhost:1313/`.

Production build:

```bash
hugo --gc --minify
```

Generated output is written to `public/`.

## How Content Works

The site is front-matter driven. Most homepage sections and detail pages pull directly from Markdown fields in `content/`.

Important behaviors:

- The site is bilingual. English pages usually have a matching Vietnamese file such as `page.md` and `page.vi.md`.
- `buildFuture = true` is enabled in `hugo.toml`, so future-dated events are included in builds.
- The homepage and event pages expect certain event fields to exist. If they are missing, the page may render with blank metadata.
- `recurring_weekly: true` causes an event’s display date to roll forward in 7-day increments from its original `date`.

## Editing Guide

### Update the weekly meetup

The main recurring event lives at `content/events/weekly-meetup.md` and `content/events/weekly-meetup.vi.md`.

Update these fields when the weekly session changes:

- `date`: anchor date and time for the recurring event
- `venue`: current venue instructions
- `time`: public event time
- `level_focus`: who the tables are for
- `venue_status`: short venue summary shown on cards
- `topic_of_week`: topic shown on homepage and event page
- `host_names`: organizer names
- `capacity_target`: internal-facing capacity summary
- `recap_highlight`: short recap text used in listings
- `summary`: short event description used across the site

If the meetup remains weekly, keep:

```yaml
recurring_weekly: true
draft: false
```

### Add a one-off event

Create a new file in `content/events/`, for example `content/events/special-workshop.md`.

Use front matter like this:

```yaml
---
title: "Vietnamese Coffee Conversation Night"
date: 2026-04-03T19:00:00+07:00
draft: false
venue: "The Local Bean, Hai Chau, Da Nang"
map_link: "https://maps.google.com/..."
time: "7:00 PM - 9:00 PM"
level_focus: "Beginner and mixed conversation tables"
venue_status: "Confirmed cafe venue"
topic_of_week: "Coffee, routines, and local favorites"
host_names: "Daisy and Kade"
capacity_target: "18 to 24 people"
recap_highlight: "A cafe-themed session with structured table prompts."
summary: "A one-night meetup focused on practical English and Vietnamese conversation around coffee culture."
show_in_past_events: true
---
```

Notes:

- `show_in_past_events: true` lets a finished event appear in recent past-event sections.
- `map_link` is optional, but the event template supports it.
- Add body content below the front matter for schedule, first-time advice, logistics, or recap details.

### Add or update a resource

Resources live in `content/resources/`.

There are two patterns in this repo:

- section landing pages such as `_index.md`
- individual resource pages such as `beginner-start.md`

Starter resources can be highlighted on the homepage. The homepage currently looks for:

```yaml
resource_type: "starter"
```

Example resource front matter:

```yaml
---
title: "Beginner Starter Pack"
date: 2026-03-01T09:00:00+07:00
draft: false
resource_type: "starter"
summary: "A simple first set of words and patterns for new members."
---
```

### Add or update a topic

Topics live in `content/topics/`.

Example front matter:

```yaml
---
title: "Food and Favorite Da Nang Spots"
date: 2026-03-20T09:00:00+07:00
draft: false
level: "All levels"
featured: true
summary: "A practical topic page for talking about food, cafes, and local favorites."
vocab_prompts:
  - "quan an (restaurant)"
  - "mon yeu thich (favorite dish)"
sample_questions:
  - "Where do you usually eat with friends?"
  - "What dish should every visitor try in Da Nang?"
---
```

Notes:

- `featured: true` can be used for homepage topic promotion.
- Keep only one featured topic unless you intentionally want Hugo to choose the first matching page.

### Edit general pages

General pages such as About, Join, Contact, and Gallery live directly under `content/`.

Examples:

- `content/about.md`
- `content/join.md`
- `content/contact.md`
- `content/gallery.md`

If a page is bilingual, update both the English and Vietnamese versions.

## Translation Workflow

This repo uses two translation mechanisms:

1. Page translations through paired content files such as:
   - `content/events/weekly-meetup.md`
   - `content/events/weekly-meetup.vi.md`
2. Interface translations through:
   - `i18n/en.yaml`
   - `i18n/vi.yaml`

Update `i18n/*.yaml` when you change text rendered by templates, buttons, badges, labels, or homepage sections.

Update `content/*.vi.md` files when you change page content meant for Vietnamese readers.

## Deployment

This site is intended for Cloudflare Pages.

- Build command: `hugo --gc --minify`
- Build output directory: `public`
- Root directory: `/`

Pushing to the deployment branch should trigger a rebuild in Cloudflare Pages.

## Repo Notes

- `themes/PaperMod/` is a git submodule. Clone with submodules if you are setting up the repo fresh.
- `public/` is currently committed in the repo. Be careful not to mix source edits and generated output unintentionally.
- `archetypes/events.md` is more minimal than the fields used by the current custom event templates, so copying an existing event file is often safer than relying on the archetype alone.

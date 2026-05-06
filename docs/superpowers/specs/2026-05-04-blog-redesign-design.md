---
date: 2026-05-04
status: in-progress
---

# Blog Redesign + Activate Weekly Notes

## Context

The blog at `gotoboy.github.io/blog/` is a personal "thought garden" hosting three distinct content shapes:

- **阅读笔记 (Reading)** — notes from books / podcasts / articles, carrying `summary` + `source` metadata
- **思考随笔 (Reflections)** — original long-form thinking
- **周记 (Weeks)** — periodic short notes; infrastructure exists in `content/weeks/` and `_templates/week.md` but never activated

Today all live content renders as identical cards in a flat reverse-chronological feed. This flattens meaningful differences in shape, density, and intent. The user is happy with the existing "quiet library" aesthetic — the work is **structural** and **typological differentiation**, not aesthetic redirection.

## Goals

- Activate Weeks section end-to-end (Hugo route + Obsidian QuickAdd command)
- Redesign homepage as a **personal foyer** (hero + 3 typed sections) rather than flat feed
- Differentiate the three card types by accent, density, eyebrow, and surfaced metadata
- Codify the design language into proper tokens (spacing / type / radius / motion / blur scales + per-section accents)
- Add a tag-cloud widget to the right sidebar so tags become actually navigable
- Reading detail pages get a "Source" block at the top of the article

## Non-goals

- Not switching themes
- Not introducing wikilinks / graph view
- Not changing font stack or base color palette
- Not building a Topics index page (deferred)

## Design tokens (custom.scss)

| Scale | Tokens |
|---|---|
| Spacing | `--gb-space-1..7` → 4 / 8 / 12 / 16 / 24 / 32 / 48 px |
| Type | `--gb-text-xs..3xl` |
| Radius | `--gb-radius-sm` 8 / `md` 14 / `lg` 18 / `xl` 22 / `pill` 999 |
| Motion | `--gb-duration-fast/base/slow` + `--gb-ease` |
| Effect | `--gb-blur-card` 14px / `--gb-blur-floating` 18px |
| Section accents | `--gb-accent-reading` (cool gray-blue) / `--gb-accent-reflection` (existing copper) / `--gb-accent-week` (warm gray-brown) |

All hardcoded values in the existing custom.scss are replaced with tokens (full rewrite, no compatibility shims).

## Information architecture

`config/_default/params.toml`:
- `mainSections = ["reading", "reflections", "weeks"]`
- `widgets.homepage = [search, archives, tagcloud]`

`config/_default/menu.toml`: add Weeks (icon `archives`, label_zh "周记", label_en "Weeks").

`_templates/week.md`: remove "legacy only" notice, set `draft: false`, align frontmatter shape with reading/reflection templates.

QuickAdd: user adds in Obsidian a new command "📅 周记" → template `_templates/week.md` → folder `content/weeks/{date}-{rand6}/index.md`. JSON snippet documented in implementation, user pastes into `.obsidian/plugins/quickadd/data.json`.

## Card variants

|            | Reading                | Reflection         | Week                |
|------------|------------------------|--------------------|---------------------|
| accent     | `--gb-accent-reading`  | `--gb-accent-reflection` | `--gb-accent-week` |
| top bar    | 4px gradient           | 4px gradient       | none                |
| eyebrow    | 📖 source domain       | 💭 REFLECTION      | 📅 Week N · YYYY    |
| body       | `summary` 2–3 lines    | first-paragraph ~120ch excerpt | body 3–4 lines |
| title size | `--gb-text-lg`         | `--gb-text-xl`     | `--gb-text-md`      |
| padding    | space-5/space-6        | space-5/space-6    | space-4/space-5     |
| radius     | xl                     | xl                 | lg                  |
| background | surface-strong         | surface-strong     | surface (lighter)   |

## Detail-page deltas

- **Reading** — top of article shows a `.source-block` (link icon + domain + URL); `summary` rendered as a quote block under the title
- **Reflection** — unchanged
- **Week** — eyebrow shows "Week N · YYYY", body uses smaller type-scale step

## Homepage shape

```
[Hero: "GoToBoy · 这里写读、想、记。" + thin underline]
[📖 最近在读 ────────────── 查看全部 →]
[Reading card] [Reading card] [Reading card]
[💭 最近在想 ────────────── 查看全部 →]
[Reflection card] [Reflection card] [Reflection card]
[📅 最近周记 ────────────── 查看全部 →]
[Week card] [Week card] [Week card]
```

Right sidebar: search · archives · tagcloud (new).

## Files

**Config**
- `config/_default/params.toml` — mainSections, widgets
- `config/_default/menu.toml` — add Weeks
- `_templates/week.md` — rewrite

**Layouts (rewrite/new)**
- `layouts/home.html` — Hero + 3 typed sections
- `layouts/single.html` — dispatch by section
- `layouts/weeks/list.html` — delete (let `_default/list.html` handle it)
- `layouts/weeks/single.html` — new
- `layouts/_partials/home/hero.html` — new
- `layouts/_partials/home/section-header.html` — new
- `layouts/_partials/home/section-list.html` — pass variant info
- `layouts/_partials/article-list/default.html` — variant dispatcher
- `layouts/_partials/article-list/reading.html` / `reflection.html` / `week.html` / `compact.html` — variant cards
- `layouts/_partials/article/article.html` — override theme: include source-block, summary, eyebrow
- `layouts/_partials/article/source-block.html` — new (Reading-only)
- `layouts/_partials/article/article-eyebrow.html` — new
- `layouts/partials/widget/tagcloud.html` — new

**Styles**
- `assets/scss/custom.scss` — full rewrite with token system

## Verification

1. `hugo server` from project root → `http://localhost:1313/blog/`
2. Homepage: hero + 3 typed sections, each with its own card variant
3. Each section's "查看全部" → its section page
4. Open a Reading post → Source block at top, summary as quote
5. Open a Reflection post → clean, no source block
6. Drop a test `content/weeks/2026-W18/index.md` → appears in Weeks section + homepage
7. Toggle dark mode → all variants OK
8. Mobile (≤768px) → sections stack, week cards stay denser
9. Right sidebar shows tag cloud, clickable

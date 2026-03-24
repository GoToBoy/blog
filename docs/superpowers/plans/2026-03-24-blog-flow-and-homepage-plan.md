# Blog Flow And Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Simplify Obsidian-to-Hugo content creation and rebuild the homepage around `阅读摘记 / 思考随笔 / 主题浏览 / 最近更新` without replacing the current theme.

**Architecture:** Keep the existing Hugo Stack theme and current content tree, but hide the technical storage model from the author. Rework QuickAdd prompts and templates so the author only chooses a lightweight writing type and title, then rebuild homepage aggregation to present calm, author-aligned sections instead of a flat recent list.

**Tech Stack:** Hugo, Hugo Stack theme overrides, Obsidian QuickAdd JSON config, Markdown content templates, SCSS

---

## File Structure

### Existing files to modify

- `.obsidian/plugins/quickadd/data.json`
  - Rename author-facing capture choices and remove manual slug-oriented prompts from the creation flow.
- `_templates/post.md`
  - Reduce required frontmatter and add the metadata needed for `阅读摘记`.
- `_templates/note.md`
  - Reduce required frontmatter and add the metadata needed for `思考随笔`.
- `_templates/week.md`
  - Remove or demote weekly-writing pressure from the author-facing creation flow.
- `config/_default/permalinks.toml`
  - Stop depending on manual `slug` entry for generated URLs.
- `config/_default/params.toml`
  - Add homepage section labels and any small configuration needed by the new homepage layout.
- `config/_default/menu.toml`
  - Remove or rename navigation that still exposes `Weekly` as a primary content model.
- `content/posts/_index.md`
  - Update section metadata to match the new author-facing language where needed.
- `content/notes/_index.md`
  - Update section metadata to match the new author-facing language where needed.
- `content/weeks/_index.md`
  - Keep only if archival compatibility is needed; otherwise reduce prominence.
- `content/about/index.md`
  - Shorten or retune the sidebar-facing description if it conflicts with the quieter homepage positioning.
- `layouts/home.html`
  - Replace the flat recent-list homepage with explicit grouped sections.
- `assets/scss/custom.scss`
  - Add homepage-specific layout and card styles for calm sectioned presentation.

### Existing content to audit or migrate

- `content/posts/中年困境思考/index.md`
- `content/notes/中年困境的思考/index.md`

These files should be updated to match the new frontmatter conventions and used as smoke-test content during homepage work.

### New files to create

- `layouts/_partials/home/section-list.html`
  - Reusable partial for rendering one homepage content section with heading, intro text, and a bounded list of entries.
- `layouts/_partials/home/topic-cards.html`
  - Reusable partial for rendering `主题浏览` cards from tags or categories.

## Implementation Notes

- Do not migrate the whole content tree to a new directory structure in this pass.
- Keep storage pragmatic: existing `posts` and `notes` directories can remain if author-facing labels and homepage presentation are updated.
- Prefer deriving URLs from file paths or Hugo defaults rather than requiring authors to type `slug`.
- Use a small explicit frontmatter field such as `writingKind = "reading"` / `writingKind = "reflection"` only if homepage grouping cannot be expressed cleanly through section mapping alone.
- Treat `weeks` as backward-compatible archived content, not an active primary creation path.

## Task 1: Lock The Author-Facing Content Model

**Files:**
- Modify: `.obsidian/plugins/quickadd/data.json`
- Modify: `_templates/post.md`
- Modify: `_templates/note.md`
- Modify: `_templates/week.md`
- Test: manual verification in Obsidian with the QuickAdd command palette

- [ ] **Step 1: Inspect the current QuickAdd capture choices and note which prompts are generated from template placeholders**

Read:
- `.obsidian/plugins/quickadd/data.json`
- `_templates/post.md`
- `_templates/note.md`
- `_templates/week.md`

Expected findings:
- `post` currently captures to `content/posts/{{VALUE:slug}}/index.md`
- `note` currently captures to `content/notes/{{VALUE:title}}/index.md`
- templates expose `slug`, `summary`, `tags`, and `draft`

- [ ] **Step 2: Decide the minimal author-facing choices**

Implement this model in the plan before editing code:
- `阅读摘记` -> stored under `content/posts/...`
- `思考随笔` -> stored under `content/notes/...`
- `week` is removed from the primary QuickAdd surface or renamed to an explicitly archival option if retention is necessary

Expected result:
- the author sees writing-intent names, not storage names

- [ ] **Step 3: Rewrite `_templates/post.md` to remove manual slug input and reduce frontmatter**

Target frontmatter shape:

```yaml
---
title: "{{VALUE:title}}"
date: {{DATE:YYYY-MM-DD}}
draft: true
tags: []
summary: ""
---
```

Body scaffold should be lighter than the current `Summary / Body` structure. Prefer a simple heading and open writing space.

- [ ] **Step 4: Rewrite `_templates/note.md` to match the low-pressure writing flow**

Target frontmatter shape:

```yaml
---
title: "{{VALUE:title}}"
date: {{DATE:YYYY-MM-DD}}
draft: true
tags: []
summary: ""
---
```

Body scaffold should encourage quick reflection rather than rigid subsections.

- [ ] **Step 5: Rewrite `_templates/week.md` or remove it from the main flow**

Preferred implementation:
- keep the file only for backward compatibility
- stop exposing it as a top-level QuickAdd choice

Expected result:
- weekly writing no longer shapes the primary blog model

- [ ] **Step 6: Update `.obsidian/plugins/quickadd/data.json` capture choices**

Required edits:
- rename `post` to `阅读摘记`
- rename `note` to `思考随笔`
- remove `{{VALUE:slug}}` from capture paths
- use title-based or date-title-based paths instead
- remove or demote the `week` choice

Preferred capture paths:

```json
"captureTo": "content/posts/{{VALUE:title}}/index.md"
"captureTo": "content/notes/{{VALUE:title}}/index.md"
```

If duplicate-title risk feels too high, use a date-title path instead:

```json
"captureTo": "content/posts/{{DATE:YYYY-MM-DD}}-{{VALUE:title}}/index.md"
```

- [ ] **Step 7: Verify the QuickAdd flow manually in Obsidian**

Run:
- Open Obsidian in this vault
- Trigger QuickAdd for `阅读摘记`
- Trigger QuickAdd for `思考随笔`

Expected:
- only `title` is prompted
- a new file opens immediately
- no slug prompt appears
- no summary prompt appears

- [ ] **Step 8: Commit the creation-flow changes**

Run:

```bash
git add .obsidian/plugins/quickadd/data.json _templates/post.md _templates/note.md _templates/week.md
git commit -m "feat: simplify blog content creation flow"
```

## Task 2: Remove Manual Slug Dependency From URLs

**Files:**
- Modify: `config/_default/permalinks.toml`
- Test: generated URLs in local Hugo output

- [ ] **Step 1: Inspect how current permalinks depend on `:slug`**

Read:
- `config/_default/permalinks.toml`
- sample content frontmatter in `content/posts/中年困境思考/index.md`
- sample content frontmatter in `content/notes/中年困境的思考/index.md`

Expected finding:
- manual slug data is still part of URL generation

- [ ] **Step 2: Replace `:slug` with a path-derived permalink strategy**

Preferred configuration:

```toml
posts = "/posts/:sections[last]/"
notes = "/notes/:sections[last]/"
weeks = "/weeks/:sections[last]/"
page = "/:slug/"
```

Alternative if Hugo resolution behaves better with leaf bundles in this repo:

```toml
posts = "/posts/:slugorfilename/"
notes = "/notes/:slugorfilename/"
weeks = "/weeks/:slugorfilename/"
```

Choose the variant that allows title-only creation without user-entered slug fields.

- [ ] **Step 3: Update existing sample content to remove stale or empty slug fields if needed**

Modify:
- `content/posts/中年困境思考/index.md`
- `content/notes/中年困境的思考/index.md`

Expected result:
- content still resolves cleanly after permalink changes

- [ ] **Step 4: Build the site to verify URLs still render**

Run:

```bash
hugo
```

Expected:
- build succeeds
- generated URLs for sample post and note do not require manual slug frontmatter

- [ ] **Step 5: Commit permalink cleanup**

Run:

```bash
git add config/_default/permalinks.toml content/posts/中年困境思考/index.md content/notes/中年困境的思考/index.md
git commit -m "feat: remove manual slug dependency from blog content"
```

## Task 3: Reframe Section Metadata And Navigation

**Files:**
- Modify: `config/_default/menu.toml`
- Modify: `content/posts/_index.md`
- Modify: `content/notes/_index.md`
- Modify: `content/weeks/_index.md`
- Modify: `config/_default/params.toml`

- [ ] **Step 1: Update section metadata so author-facing labels match the new model**

Preferred updates:
- `content/posts/_index.md` title -> `阅读摘记`
- `content/notes/_index.md` title -> `思考随笔`
- `content/weeks/_index.md` title -> archival wording such as `Weekly Archive` if the section remains public

- [ ] **Step 2: Remove `Weekly` from the main menu or move it to a low-priority archival position**

Modify:
- `config/_default/menu.toml`

Expected:
- the primary navigation no longer teaches `Weekly` as a core content identity

- [ ] **Step 3: Add homepage copy configuration to `config/_default/params.toml`**

Add a small config block such as:

```toml
[homepage]
    readingTitle = "阅读摘记"
    reflectionTitle = "思考随笔"
    topicsTitle = "主题浏览"
    recentTitle = "最近更新"
```

Optional:
- short per-section intros if needed by the homepage partials

- [ ] **Step 4: Verify navigation and labels render coherently**

Run:

```bash
hugo
```

Expected:
- menu wording matches the new taxonomy
- section pages still resolve

- [ ] **Step 5: Commit taxonomy and navigation wording updates**

Run:

```bash
git add config/_default/menu.toml config/_default/params.toml content/posts/_index.md content/notes/_index.md content/weeks/_index.md
git commit -m "feat: align blog labels with new writing model"
```

## Task 4: Build Homepage Section Partials

**Files:**
- Create: `layouts/_partials/home/section-list.html`
- Create: `layouts/_partials/home/topic-cards.html`
- Test: homepage rendering via Hugo build

- [ ] **Step 1: Create `layouts/_partials/home/section-list.html`**

The partial should accept a dict with:
- `title`
- `intro`
- `pages`
- `limit`
- `emptyText`

Suggested structure:

```go-html-template
<section class="home-section">
  <header class="home-section__header">
    <h2>{{ .title }}</h2>
    {{ with .intro }}<p>{{ . }}</p>{{ end }}
  </header>
  <div class="article-list">
    {{ range first .limit .pages }}
      {{ partial "article-list/default" . }}
    {{ else }}
      <p class="home-section__empty">{{ $.emptyText }}</p>
    {{ end }}
  </div>
</section>
```

- [ ] **Step 2: Create `layouts/_partials/home/topic-cards.html`**

The partial should render a bounded list of tags or categories as calm cards, not a dense cloud.

Suggested structure:

```go-html-template
<section class="home-section home-section--topics">
  <header class="home-section__header">
    <h2>{{ .title }}</h2>
    {{ with .intro }}<p>{{ . }}</p>{{ end }}
  </header>
  <div class="topic-card-grid">
    {{ range .terms }}
      <a class="topic-card" href="{{ .Page.RelPermalink }}">
        <span class="topic-card__name">{{ .Page.Title }}</span>
        <span class="topic-card__count">{{ .Count }}</span>
      </a>
    {{ end }}
  </div>
</section>
```

- [ ] **Step 3: Run a Hugo build after creating the partials**

Run:

```bash
hugo
```

Expected:
- build succeeds
- new partials are syntactically valid even before `layouts/home.html` is switched over

- [ ] **Step 4: Commit the homepage partial scaffolding**

Run:

```bash
git add layouts/_partials/home/section-list.html layouts/_partials/home/topic-cards.html
git commit -m "feat: add reusable homepage section partials"
```

## Task 5: Rebuild The Homepage Around Quiet Sections

**Files:**
- Modify: `layouts/home.html`
- Modify: `config/_default/params.toml`
- Test: homepage behavior in generated site

- [ ] **Step 1: Inspect how the current homepage currently gathers content**

Read:
- `layouts/home.html`
- any existing homepage widget config in `config/_default/params.toml`

Expected finding:
- homepage is currently a recent-list cut off to the last year

- [ ] **Step 2: Gather the page collections needed for each homepage section**

In `layouts/home.html`, define:
- `readingPages` from the `posts` section
- `reflectionPages` from the `notes` section
- `recentPages` from the combined recent content set
- `topicTerms` from tags or categories

Suggested Hugo sketch:

```go-html-template
{{- $pages := where (partial "helper/pages.html" .) "Draft" "!=" true -}}
{{- $readingPages := where $pages "Section" "posts" -}}
{{- $reflectionPages := where $pages "Section" "notes" -}}
{{- $recentPages := first 6 $pages -}}
{{- $topicTerms := first 8 .Site.Taxonomies.tags.ByCount -}}
```

- [ ] **Step 3: Replace the flat article list with ordered homepage sections**

Use the new partials in this order:
1. `阅读摘记`
2. `思考随笔`
3. `主题浏览`
4. `最近更新`

Expected result:
- homepage becomes a sectioned writing-space layout instead of a single feed

- [ ] **Step 4: Keep the main area free of a large intro block**

Do not add a hero intro in `layouts/home.html`.

Expected:
- personal context stays in the sidebar only

- [ ] **Step 5: Build and inspect the homepage**

Run:

```bash
hugo
```

Expected:
- homepage renders all four sections in order
- empty states are graceful when a section has few items

- [ ] **Step 6: Commit the homepage layout changes**

Run:

```bash
git add layouts/home.html config/_default/params.toml
git commit -m "feat: rebuild homepage around writing sections"
```

## Task 6: Add Calm Homepage Styling

**Files:**
- Modify: `assets/scss/custom.scss`
- Test: responsive homepage visual inspection

- [ ] **Step 1: Add explicit styles for the new homepage sections**

Add styles for:
- `.home-section`
- `.home-section__header`
- `.home-section__empty`
- `.topic-card-grid`
- `.topic-card`
- homepage-specific spacing between sections

- [ ] **Step 2: Preserve the existing quiet visual language**

Do not introduce:
- loud hero banners
- promotional call-to-actions
- dense dashboard grids

Expected:
- the homepage still feels consistent with the current site palette and typography

- [ ] **Step 3: Improve mobile layout for section cards**

Add responsive behavior so:
- topic cards collapse to one or two columns on smaller screens
- article cards retain readable spacing

- [ ] **Step 4: Build and visually inspect desktop and mobile layouts**

Run:

```bash
hugo
```

Then inspect the homepage in a browser at:
- desktop width
- tablet width
- phone width

Expected:
- sections remain calm and readable at each breakpoint

- [ ] **Step 5: Commit homepage styling**

Run:

```bash
git add assets/scss/custom.scss
git commit -m "feat: style homepage writing sections"
```

## Task 7: Retune Sidebar Copy To Support The New Positioning

**Files:**
- Modify: `config/_default/params.toml`
- Modify: `content/about/index.md`
- Test: homepage sidebar rendering

- [ ] **Step 1: Shorten the sidebar subtitle so it supports the new homepage tone**

The subtitle should feel like a quiet personal writing space, not a product tagline.

- [ ] **Step 2: Align the About page with the broader writing identity**

Reduce emphasis on highly specific frontend-career positioning if it overconstrains the blog identity.

Expected:
- the blog feels broad enough to include reading notes and life reflections

- [ ] **Step 3: Build and inspect the sidebar and About page**

Run:

```bash
hugo
```

Expected:
- the sidebar intro complements the homepage without duplicating it
- the About page still reads coherently

- [ ] **Step 4: Commit the copy updates**

Run:

```bash
git add config/_default/params.toml content/about/index.md
git commit -m "feat: align sidebar copy with blog positioning"
```

## Task 8: Final Verification And Cleanup

**Files:**
- Verify all files changed by Tasks 1-7

- [ ] **Step 1: Run the full site build**

Run:

```bash
hugo --gc --minify
```

Expected:
- successful production-style build

- [ ] **Step 2: Smoke-test the key user flows**

Verify:
- QuickAdd `阅读摘记` creates a new Markdown file with only a title prompt
- QuickAdd `思考随笔` creates a new Markdown file with only a title prompt
- homepage shows `阅读摘记 / 思考随笔 / 主题浏览 / 最近更新`
- sidebar contains the personal context, not the homepage main area

- [ ] **Step 3: Review git diff for accidental theme-wide regressions**

Run:

```bash
git status --short
git diff --stat
```

Expected:
- only planned files changed

- [ ] **Step 4: Commit final polish if needed**

Run:

```bash
git add .
git commit -m "chore: finalize blog flow and homepage refresh"
```

- [ ] **Step 5: Prepare a short implementation summary**

Include:
- what changed in the writing flow
- what changed on the homepage
- what still remains intentionally untouched

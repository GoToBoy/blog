# Blog Flow And Homepage Design

## Overview

This design updates the blog in two connected areas:

1. Simplify the writing and publishing flow so creating a new piece feels like writing Markdown, not filling CMS metadata.
2. Reframe the homepage as a personal writing space centered on accumulated thoughts and reading output, rather than the current technical content buckets.

The goal is to reduce writing friction for a new author while making the site feel more aligned with the author's actual output pattern.

## Current Problems

### Writing Flow

The current templates expose publishing-system fields directly to the author:

- `title`
- `slug`
- `date`
- `draft`
- `tags`
- `summary`

For this blog, those fields are not equally important. Requiring them upfront makes content creation feel heavier than the act of writing itself.

The current model also uses technical buckets like `posts`, `notes`, and `weeks`, which reflect Hugo structure more than the author's intent.

### Homepage

The current homepage mostly renders a recent list. While the visual styling is already calm and intentional, the information architecture still feels template-driven.

The author wants:

- the sidebar to hold personal context
- the main area to focus on accumulated writing and thought
- a quieter, more stable layout
- content categories that match natural writing habits instead of rigid output pressure

## Design Principles

### 1. Writing First

Creating content should feel like "write a Markdown file and publish it", not "create and configure an entry."

### 2. Low Pressure Taxonomy

Category names should invite consistent output instead of implying that every piece must be polished or substantial.

### 3. Sidebar For Context, Main Area For Content

Personal introduction belongs in the sidebar. The homepage main area should not lead with a large self-description block.

### 4. Quiet Presentation

The homepage should feel like a calm personal writing space, not a magazine front page or an aggressively optimized content product.

## Proposed Content Model

Replace the current author-facing mental model of `post / note / week` with these homepage-facing groupings:

- `阅读摘记`
- `思考随笔`
- `主题浏览`
- `最近更新`

### Meaning Of Each Group

#### 阅读摘记

Content produced from reading books, essays, articles, or other materials. This includes excerpts, summaries, and reorganized takeaways.

#### 思考随笔

Personal reflections, life observations, reactions, and extensions of previous reading or experience.

#### 主题浏览

A navigational layer that groups content by broader themes such as technology, life, reading, writing, or other topics that emerge over time.

#### 最近更新

A lightweight chronological stream near the bottom of the homepage for recency and continuity.

## Writing Flow Design

### Author Experience

The author should only need to decide:

- title
- content body
- optionally, whether the piece belongs more naturally to `阅读摘记` or `思考随笔`

Everything else should either be automatic or optional.

### Frontmatter Strategy

Required by default:

- `title`
- `date`

Optional:

- `summary`
- `tags`

Automatic or hidden from the author:

- `slug`
- `draft` default behavior

### Slug Handling

The current configuration uses `:slug` in permalinks, which forces author-visible slug management.

Recommended change:

- stop requiring manual slug input
- either auto-generate slug from title during creation, or remove slug dependency from the permalink structure and let Hugo derive URLs from file paths

Preferred direction: remove manual slug entry from the creation step entirely.

### Summary Handling

`summary` should not be mandatory at creation time.

Recommended behavior:

- if `summary` is present, use it
- otherwise use Hugo-generated summary or an excerpt from the body

### Draft Handling

`draft` should not be something the author thinks about every time a file is created.

Recommended behavior:

- new content templates can still default to `draft: true` internally if that matches the publishing workflow
- but this should not be an author decision field surfaced in QuickAdd prompts

### Tags Handling

Tags should be optional and only used when they meaningfully support later topic browsing.

They should not be required when the author's main goal is simply to get a piece written.

## Homepage Design

### Overall Positioning

The homepage should be a personal writing-space homepage, not a generic article list and not a polished "featured works" landing page.

### Sidebar

The sidebar remains responsible for:

- avatar
- site title
- short blog description
- primary navigation
- social links

The sidebar can carry the introduction and context. The main content area should not repeat that function.

### Main Area Structure

The main area should use quiet, clearly separated sections in this order:

1. `阅读摘记`
2. `思考随笔`
3. `主题浏览`
4. `最近更新`

This order reflects the author's real output pattern:

- reading and summarizing
- extending into personal reflection
- organizing themes over time
- maintaining a sense of recency without letting chronology dominate the page

### Section Behavior

#### 阅读摘记

Show a small set of the latest or most relevant reading-based pieces.

The cards should feel inviting and lightweight, not heavy or academic.

#### 思考随笔

Show recent personal reflections with slightly softer presentation than the reading section.

This section should signal that unfinished but meaningful thinking is welcome.

#### 主题浏览

Present theme entry points as calm navigation cards rather than a dense tag cloud.

The purpose is browsing, not metadata display.

#### 最近更新

Show a concise chronological list at the bottom, enough to make the blog feel alive without making the whole homepage a feed.

## Information Architecture Implications

This design separates:

- how content is stored in Hugo
- how content is created in Obsidian/QuickAdd
- how content is presented on the homepage

The internal directory structure does not need to map one-to-one to the author's mental model, as long as the creation flow and homepage presentation do.

## Approach Options Considered

### Option 1: Keep Existing Structure And Only Rename Labels

Pros:

- minimal implementation effort
- low migration risk

Cons:

- does not actually reduce author friction
- preserves the same technical-first mindset
- likely leaves the homepage feeling like a modified theme

### Option 2: Simplify Creation Flow And Rebuild Homepage Sections

Pros:

- directly addresses both user pain points
- aligns system behavior with actual writing habits
- preserves the current visual tone while changing structure

Cons:

- requires coordinated changes across templates, config, and homepage logic

This is the recommended option.

### Option 3: Full Visual Rebrand With New Content Model

Pros:

- strongest aesthetic reset

Cons:

- too much change for the current stage
- risks solving style before structure
- increases implementation and maintenance cost

## Error Handling And Edge Cases

### Sparse Content

If a section has too little content, the homepage should degrade gracefully:

- show fewer items
- avoid empty decorative containers
- let `最近更新` provide continuity

### Mixed Content

Some pieces may blur the line between reading notes and personal reflection.

The content model should tolerate this. The system only needs a practical primary placement, not perfect taxonomy purity.

### Future Evolution

If the author later accumulates stronger long-form work, the homepage can add a highlighted piece or featured block without changing the core structure.

## Testing Strategy

### Content Creation Verification

Verify that a new entry can be created with materially fewer prompts than before.

Success criteria:

- no manual slug entry
- no required summary entry
- no required tag entry
- author can begin writing immediately after entering a title

### Homepage Verification

Verify that the homepage:

- no longer feels like a plain recent-list page
- keeps personal context in the sidebar
- presents the new sections clearly on desktop and mobile
- still behaves correctly when content counts are low

## Recommended Implementation Sequence

1. Simplify templates and QuickAdd-facing metadata requirements.
2. Adjust permalink or slug strategy to remove manual slug input.
3. Introduce a content typing strategy that can support `阅读摘记` and `思考随笔`.
4. Rebuild homepage section logic around the new structure.
5. Refine section styling so the layout stays quiet and intentional.

## Out Of Scope

These items are intentionally excluded from this design:

- a full theme replacement
- a full CMS or admin UI
- advanced search or recommendation systems
- aggressive SEO optimization work

## Final Recommendation

Implement a low-friction writing flow and a quiet homepage structured around:

- `阅读摘记`
- `思考随笔`
- `主题浏览`
- `最近更新`

This gives the author a blog that is easier to write into and more truthful in how it presents the work: not as a polished publication machine, but as an ongoing space for reading, reflection, and accumulation.

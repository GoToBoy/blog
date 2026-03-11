# Blog Workflow

This repository is both:

- an `Obsidian` vault for writing
- a `Hugo` site for build and deployment

Open `/Users/taro/Blog` directly in Obsidian.

## Content Layout

- [content/posts](/Users/taro/Blog/content/posts): published long-form posts
- [content/notes](/Users/taro/Blog/content/notes): published short notes
- [content/drafts](/Users/taro/Blog/content/drafts): local drafts, never rendered or deployed
- [content/private](/Users/taro/Blog/content/private): private notes, never rendered or deployed

Each article or note should use a leaf bundle:

```text
content/posts/my-article/
  index.md
  image.png
```

This matches the current Obsidian attachment setting `attachmentFolderPath: "./"`, so pasted images land next to `index.md`.

## Writing Rules

- Create new files from templates in [_templates](/Users/taro/Blog/_templates).
- Prefer one folder per post or note, with the Markdown file named `index.md`.
- Reference local images with relative paths, for example `![](image.png)`.
- Do not store publishable content under `drafts` or `private`.

Section-level defaults are handled by Hugo:

- `posts` cascade to category `posts`
- `notes` cascade to category `notes`
- `drafts` are always draft and never published
- `private` is always draft/private and never published

## Local Preview

Run:

```bash
hugo server -D
```

`-D` includes drafts during local preview.

## Deployment

Push to `main` or `master` and GitHub Actions will build and deploy the site with Hugo. Workflow files live in [.github/workflows](/Users/taro/Blog/.github/workflows).

## Project TODO

- update site metadata in [config/_default/config.toml](/Users/taro/Blog/config/_default/config.toml)
- update theme settings in [config/_default/params.toml](/Users/taro/Blog/config/_default/params.toml)
- set the final `baseurl` before production deployment

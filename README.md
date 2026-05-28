### My blog

## Running Locally

### Prerequisites
- [Hugo](https://gohugo.io/installation/) (extended edition)

### Running the Development Server
```bash
hugo server
```

The site will be available at `http://localhost:1313`

The server watches for changes and automatically rebuilds the site.

To include future-dated posts:
```bash
hugo server --buildFuture
```

## Writing Posts

Create a new file in `content/posts/` with the format `YYYY-MM-DD-title-slug.md`:

```markdown
---
date: 2024-01-15T00:00:00-05:00
slug: "title-slug"
title: "Your Post Title"
tags: [tag1, tag2]
---

Your content here...
```

Tags are always arrays (use `[tag]` even for a single tag). Hugo auto-generates tag pages — no need to create them manually.

### AI disclosure

Add `ai_conversation_url` (string or list) to a post's front matter to render the AI disclaimer linking the source conversation(s).

### Series

Multi-part posts live under `content/series/<series-name>/`. Each post sets `series` and `series_part`; the series `_index.md` can carry an `ai_conversation_url` and the `ai-generated` tag, which every post in the section inherits.

## Deployment

Push to `main` and GitHub Actions will automatically build and deploy the site.

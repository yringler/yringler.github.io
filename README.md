### My blog

## Running Locally

### Prerequisites
- [Hugo](https://gohugo.io/installation/) (extended edition)

### Setup
Clone with submodules (for the PaperMod theme):
```bash
git clone --recurse-submodules https://github.com/yringler/yringler.github.io.git
```

If you already cloned without submodules:
```bash
git submodule update --init --recursive
```

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

## Deployment

Push to `main` and GitHub Actions will automatically build and deploy the site.

# Claude.md - Project Guide

This is a personal Hugo blog hosted on GitHub Pages at blog.yehudardevelopment.com.

## Project Structure

```
yringler.github.io/
├── hugo.toml                  # Site configuration
├── content/
│   ├── posts/                 # Blog posts (Markdown files)
│   ├── chats/                 # AI conversation transcripts
│   └── about.md               # About page
├── layouts/
│   ├── partials/
│   │   ├── ai-disclaimer.html     # Blue disclaimer for AI-generated content
│   │   ├── in-review-disclaimer.html  # Orange disclaimer for WIP content
│   │   ├── series-nav.html        # Multi-part series navigation
│   │   └── extend_footer.html     # Footer extension point
│   ├── posts/
│   │   └── single.html           # Post layout (injects disclaimers/series nav)
│   └── 404.html
├── static/
│   ├── CNAME                  # Custom domain config
│   ├── robots.txt             # SEO settings
│   └── clean-chat.html        # Claude chat sanitizer tool
├── assets/
│   └── css/extended/
│       └── custom.css         # Custom styles (disclaimers, series nav)
├── themes/
│   └── PaperMod/              # Theme (git submodule)
├── .github/workflows/
│   └── hugo.yml               # GitHub Actions deploy workflow
└── CLAUDE.md
```

## Technology Stack

- **Hugo**: Static site generator
- **Theme**: PaperMod with custom layout overrides
- **Hosting**: GitHub Pages (deployed via GitHub Actions)
- **Deployment**: Automatic on push to `main` branch

## Running the Site Locally

```bash
hugo server                    # Start dev server at localhost:1313
hugo server -D                 # Include draft posts
hugo server --buildFuture      # Include future-dated posts
```

The server auto-rebuilds on file changes.

## Content Management

### Creating Blog Posts

1. Create file in `content/posts/` with format: `YYYY-MM-DD-title-slug.md`
2. Use this front matter template:

```yaml
---
date: 2024-01-15T00:00:00-05:00
title: "Your Post Title"
tags: [tag1, tag2]
ai_conversation_url: https://claude.ai/share/... # Optional: single conversation URL
# OR for multiple conversations:
# ai_conversation_url:
#   - https://claude.ai/share/...
#   - https://claude.ai/share/...
---

Your content here...
```

**Important**:
- `date` field in front matter determines publication date
- Posts dated in the future won't be published unless `--buildFuture` is used
- Use hyphens in filename slugs, not underscores

### Tags System

Hugo auto-generates tag pages via taxonomies. No need to create individual tag page files.

- Tags index: `/tags/`
- Individual tag pages: `/tags/tag-name/`
- Just add tags to post front matter

**Existing tags**: ai, ai-generated, poetry, coding, in-review

### AI-Generated Content

Posts with `ai_conversation_url` in front matter display a blue disclaimer box at the top. This field supports both single URLs and arrays of multiple URLs:

```yaml
# Single conversation
ai_conversation_url: https://claude.ai/share/conversation-id

# Multiple conversations
ai_conversation_url:
  - https://claude.ai/share/conversation-id-1
  - https://claude.ai/share/conversation-id-2
```

The disclaimer is rendered via `layouts/partials/ai-disclaimer.html`, injected by the custom `layouts/posts/single.html`.

### Series Support

For multi-part posts, add `series` and `series_part` to front matter:

```yaml
---
series: series-name
series_part: 1
---
```

A navigation box automatically appears showing all parts of the series.

## Site Configuration

Key settings in `hugo.toml`:

- **Title**: "Random thoughts of me"
- **Author**: Yehuda Ringler
- **URL**: https://blog.yehudardevelopment.com
- **Theme**: PaperMod (auto dark/light mode)
- **Permalink format**: `/:year/:month/:day/:title/`

Navigation header: About, Tags

## Custom Layouts

### Post Layout (`layouts/posts/single.html`)
Overrides PaperMod's default to inject:
- In-review disclaimer (for posts tagged "in-review")
- AI disclaimer (for posts with `ai_conversation_url`)
- Series navigation (for posts with `series` param)

### Partials (`layouts/partials/`)
- `ai-disclaimer.html`: Blue box for AI-generated content transparency
- `in-review-disclaimer.html`: Orange box for WIP content
- `series-nav.html`: Navigation for multi-part series
- `extend_footer.html`: PaperMod footer extension point

## Utilities

### Claude Chat Sanitizer (`static/clean-chat.html`)

Web tool for cleaning up Claude conversation exports. Accessible at `/clean-chat.html`.

## Git Workflow

- **Main branch**: `main` (deploy target)
- GitHub Actions automatically builds and deploys on push to `main`

## Writing Conventions

1. **Post titles**: Use descriptive, engaging titles
2. **Content style**: Mix of technical, philosophical, and personal topics
3. **Formatting**:
   - Use headers for structure (##, ###)
   - Hugo supports footnotes natively via Goldmark (`[^1]`)
   - Use blockquotes for emphasis (>)
   - Bold for key terms (**term**)
4. **AI collaboration**: Be transparent about AI involvement via disclaimer

## Common Tasks

### Add a new post
```bash
# Create content/posts/YYYY-MM-DD-title.md with proper front matter
# Tags are auto-generated, no need to create tag pages
```

### Update site config
```bash
# Edit hugo.toml
# Hugo server auto-reloads
```

### Deploy changes
```bash
git add .
git commit -m "Description of changes"
git push origin main
# GitHub Actions auto-builds and deploys
```

## Important Files to Preserve

- `hugo.toml`: All site configuration
- `layouts/posts/single.html`: AI disclaimer + series integration
- `layouts/partials/ai-disclaimer.html`: Transparency feature
- `static/CNAME`: Custom domain configuration
- `.github/workflows/hugo.yml`: Deployment pipeline
- `themes/PaperMod`: Theme submodule

## Contact & Metadata

- **Author**: Yehuda Ringler (yrappdev@gmail.com)
- **GitHub**: @yringler
- **Site**: https://blog.yehudardevelopment.com
- **Description**: Personal blog about technology, philosophy, and life

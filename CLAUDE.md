# Claude.md - Project Guide

This is a personal Jekyll blog hosted on GitHub Pages at blog.yehudardevelopment.com.

## Project Structure

```
yringler.github.io/
├── docs/                    # Jekyll site root
│   ├── _config.yml         # Site configuration
│   ├── _posts/             # Blog posts (Markdown files)
│   ├── _layouts/           # Custom layouts (home, post, tag)
│   ├── _includes/          # Reusable components (footer, post-tags, ai-disclaimer)
│   ├── assets/             # Static assets (CSS, images)
│   ├── tags/               # Tag pages (one file per tag)
│   ├── chats/              # AI conversation transcripts
│   ├── tools/              # Utility tools (Claude chat sanitizer)
│   ├── Gemfile             # Ruby dependencies
│   └── index.markdown      # Homepage
├── index.html              # Root redirect
└── README.md               # Setup and usage instructions
```

## Technology Stack

- **Jekyll**: Static site generator (v4.3.2 compatible)
- **Theme**: Minima (v2.5) with custom overrides
- **Hosting**: GitHub Pages
- **Ruby**: 2.7 or higher required
- **Plugins**:
  - jekyll-feed (RSS/Atom feeds)
  - jekyll-seo-tag (SEO metadata)
  - jekyll-sitemap (XML sitemap)

## Running the Site Locally

Always work from the `docs/` directory:

```bash
cd docs
bundle install              # First time setup
bundle exec jekyll serve    # Start dev server at localhost:4000
```

The server auto-rebuilds on file changes.

## Content Management

### Creating Blog Posts

1. Create file in `docs/_posts/` with format: `YYYY-MM-DD-title-slug.md`
2. Use this front matter template:

```yaml
---
layout: post
title: "Your Post Title"
tags: [tag1, tag2]
ai_conversation_url: https://claude.ai/share/... # Optional: for AI-generated content
---

Your content here...
```

**Important**:
- Post filename date determines publication date (not front matter)
- Posts dated in the future won't be published until that date
- Use hyphens in filename slugs, not underscores

### Tags System

When adding a new tag to a post, create a corresponding tag page:

1. Create `docs/tags/tag-name.md`:

```yaml
---
layout: tag
title: "Tag: Tag Name"
tag: tag-name
permalink: /tags/tag-name/
---
```

2. Use lowercase, hyphenated tag identifiers
3. Tag pages automatically list all posts with that tag
4. The main tags index at `/tags/` auto-generates from existing tag pages

**Existing tags**: ai, ai-generated, poetry, coding

### AI-Generated Content

Posts with `ai_conversation_url` in front matter display a blue disclaimer box at the top:

```yaml
ai_conversation_url: https://claude.ai/share/conversation-id
```

The disclaimer is automatically included via `_includes/ai-disclaimer.html` (see `_layouts/post.html:20-22`).

## Site Configuration

Key settings in `docs/_config.yml`:

- **Title**: "Random thoughts of me"
- **Author**: Yehuda Ringler
- **URL**: https://blog.yehudardevelopment.com
- **Timezone**: America/New_York
- **Permalink format**: `/:year/:month/:day/:title/`
- **Theme skin**: auto (respects user's dark/light mode preference)

Navigation header includes:
- About page
- Tags index

## Custom Layouts & Includes

### Layouts (`docs/_layouts/`)
- `home.html`: Homepage post list
- `post.html`: Individual post view (includes AI disclaimer logic)
- `tag.html`: Tag archive pages

### Includes (`docs/_includes/`)
- `ai-disclaimer.html`: Blue disclaimer box for AI-generated content
- `post-tags.html`: Tag badges displayed on posts
- `footer.html`: Custom footer
- `social.html`: Social media links

## Utilities

### Claude Chat Sanitizer (`docs/tools/claude-chat-sanitizer.html`)

Web tool for cleaning up Claude conversation exports. Accessible at `/clean-chat.html`.

### Chats Directory (`docs/chats/`)

Storage for AI conversation transcripts referenced in blog posts.

## Git Workflow

- **Main branch**: `main` (deploy target)

When committing:
- Use descriptive commit messages
- Include co-authorship when appropriate
- Work in feature branches for complex changes

## Writing Conventions

Based on existing content:

1. **Post titles**: Use descriptive, engaging titles (often questions or provocative statements)
2. **Content style**: Mix of technical, philosophical, and personal topics
3. **Length**: Varies from short posts to long-form essays (2,000+ words)
4. **Formatting**:
   - Use headers for structure (##, ###)
   - Include footnotes for citations (Jekyll supports automatic footnote numbering)
   - Use blockquotes for emphasis (>)
   - Bold for key terms (**term**)
5. **AI collaboration**: Be transparent about AI involvement via disclaimer

## Common Tasks

### Add a new post
```bash
cd docs/_posts
# Create YYYY-MM-DD-title.md with proper front matter
# If using new tags, create tag pages in docs/tags/
```

### Update site config
```bash
# Edit docs/_config.yml
# Restart Jekyll server to see changes
```

### Deploy changes
```bash
git add .
git commit -m "Description of changes"
git push origin main
# GitHub Pages auto-deploys from main branch
```

## Troubleshooting

- **Posts not appearing**: Check filename date format and future date filtering
- **Tags not working**: Ensure tag page exists in `docs/tags/` with exact tag name match
- **Local build errors**: Run `bundle install` and ensure Ruby version 2.7+
- **Styling issues**: Minima theme uses `docs/_sass/` for custom overrides

## Important Files to Preserve

- `docs/_config.yml`: All site configuration
- `docs/Gemfile`: Ruby dependencies (locked to GitHub Pages versions)
- `docs/_layouts/post.html`: AI disclaimer integration
- `docs/_includes/ai-disclaimer.html`: Transparency feature
- `docs/CNAME`: Custom domain configuration
- `docs/robots.txt`: SEO settings

## Development Notes

- Site uses GitHub Pages gem bundle for compatibility
- Theme is Minima with custom layouts overriding defaults
- Jekyll processes everything in `docs/` directory
- `_site/` is auto-generated (gitignored)
- Custom domain configured via CNAME
- Site is Windows-compatible (includes Windows-specific gems)

## Contact & Metadata

- **Author**: Yehuda Ringler (yrappdev@gmail.com)
- **GitHub**: @yringler
- **Site**: https://blog.yehudardevelopment.com
- **Description**: Personal blog about technology, philosophy, and life

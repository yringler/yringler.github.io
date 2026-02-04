### My blog

## Running Locally

### Prerequisites
- Ruby (version 2.7 or higher recommended)
- Bundler (`gem install bundler`)

### Setup
1. Navigate to the docs directory:
   ```bash
   cd docs
   ```

2. Install dependencies:
   ```bash
   bundle install
   ```

### Running the Development Server
```bash
bundle exec jekyll serve
```

The site will be available at `http://localhost:4000`

The server will watch for changes and automatically rebuild the site when you modify files.

## Working with Tags

### Adding Tags to Posts

Add tags to any post by including them in the front matter:

```markdown
---
layout: post
title: "Your Post Title"
tags: ai
---
```

For multiple tags, use an array:

```markdown
---
layout: post
title: "Your Post Title"
tags: [ai, philosophy, technology]
---
```

Tags will automatically appear:
- On the individual post page (below the title/date)
- On the home page in the post list
- In the tags index at `/tags/`

### Creating Tag Pages

When you add a new tag to a post, you need to create a corresponding tag page:

1. Create a new file in `docs/tags/` directory (e.g., `docs/tags/philosophy.md`)
2. Add the following front matter:

```markdown
---
layout: tag
title: "Tag: Philosophy"
tag: philosophy
permalink: /tags/philosophy/
---
```

3. Replace `philosophy` with your tag name (use lowercase, no spaces)
4. The tag will automatically appear in the tags index with a count of posts

### Tag Page Template

Copy this template for new tags:

```markdown
---
layout: tag
title: "Tag: [TAG_NAME]"
tag: [tag-name]
permalink: /tags/[tag-name]/
---
```

Replace `[TAG_NAME]` with the display name (can have capitals/spaces) and `[tag-name]` with the tag identifier (lowercase, hyphenated).
---
date: 2026-03-06T00:00:00-05:00
title: "From Sacred Text to Static Site: Building Sha'ar HaYichud Resources with AI"
tags: [ai, coding, ai-generated]
ai_conversation_url: https://claude.ai/share/22428a46-c5ef-4879-beda-2c1662ac45b7
---

There's a book I've wanted to share with the world for years. *Sha'ar HaYichud* (שַׁעַר הַיִּחוּד — "The Gate of Unity"), written by the Mitteler Rebbe, Rabbi DovBer Schneuri, is a foundational Chassidic text of remarkable depth. Years ago I went through the entire book and divided it into labeled sections and subsections — a structural layer I felt would make it significantly more accessible to readers. That work sat in my notes, half-forgotten, until a few weeks ago when something clicked and I decided to finally publish it.

What followed was a surprisingly fun engineering journey, guided heavily by AI (Claude Code, specifically), that ended up touching static site generation, Cloudflare Pages, edge functions, GitHub's API, and a round-trip CMS built entirely on static infrastructure. Here's how it went.

---

## Step 0: The Content Problem

Before any of this was a web project, it was a markup problem. I needed a format that could represent my hierarchical divisions of the text — chapters, sections, subsections, labels — in a way that was structured and machine-readable but also something I could actually edit. I landed on a custom XML format. You can see an example chapter file [here](https://github.com/yringler/shaar-hayichud-sections/blob/master/src/texts/chapter_01.xml).

XML is great for structure, but painful to edit by hand. So I did what any reasonable person with access to AI would do: I had Claude Code build me an Angular app with a GUI and keyboard shortcuts specifically designed to let me rapidly divide and label text. That became the [section editor](https://tool.shaarhayichudresources.com/) — a tool that's publicly accessible, though some of its features (like loading directly from the Sha'ar HaYichud data and committing back to GitHub) are purpose-built for my own workflow.

The source and section editor repos are on GitHub:
- [shaar-hayichud-sections](https://github.com/yringler/shaar-hayichud-sections) — the 11ty site and content
- [section-tool](https://github.com/yringler/section-tool) — the Angular editor

---

## Step 1: First Publication — GitHub Pages + XSLT

With XML in hand, the next question was: how do I get this in front of people? My first answer was XSLT. If you're not familiar with it, XSLT is a declarative XML transformation language — powerful, but with a syntax that's genuinely intimidating. I had Claude generate the stylesheet, which is exactly the kind of task AI is perfect for: the logic is well-defined, the output is verifiable, and the alternative is spending an afternoon learning a niche spec. I added the XSL stylesheet and a small Node script to generate an index page, and the result was actually pretty nice — the XML transformed to readable HTML with chapter navigation and decent formatting. This lived in its own GitHub repository and got deployed to a subpath of my blog at [blog.yehudardevelopment.com](https://blog.yehudardevelopment.com/), via a GitHub Actions workflow that built the Angular editor and published the XSLT output to GitHub Pages.

The workflow for getting the Angular app onto the blog felt genuinely creative to me: on every push to the editor repo, a GitHub Actions job created a release with the compiled build artifacts. That triggered a repository dispatch event to the blog repo, which ran its own workflow, looped through a configured list of external repos, pulled down the latest release artifacts, and dropped them into the right subpath. Complicated, but it worked well — and the separation was actually a feature. The Angular app only rebuilt when its own repo changed, not on every blog edit. The blog just pulled the latest release artifact, so there was natural caching baked into the architecture: two independent build pipelines, loosely coupled via GitHub releases.

---

## Step 2: A Real Domain — Moving to Cloudflare Pages

GitHub Pages was fine, but this content deserved its own home. I registered [shaarhayichudresources.com](https://www.shaarhayichudresources.com/en/) through Cloudflare, and that's when I discovered how good Cloudflare Pages actually is. The setup is almost trivially simple: point it at a repo, specify the build command, specify the output directory, and it handles everything. No fiddling with GitHub Actions for the deployment itself.

The bare domain and `www` both point to Cloudflare Pages. Cloudflare also makes redirects trivially easy to configure, so the bare domain redirects cleanly to `www`. The tool lives at [tool.shaarhayichudresources.com](https://tool.shaarhayichudresources.com/).

---

## Step 3: An Eleventy Site

With a real domain, it was time for a real site. I'd been using a Node script and XSLT, but neither was a proper foundation for growing the project. After [discussing options with Claude](https://claude.ai/share/b25c4150-585f-45cb-a2f4-268c66c300ac), I landed on [Eleventy (11ty)](https://www.11ty.dev/) — a deliberately simple, fast, low-ceremony static site generator. It felt right for the goals: no framework overhead, just structured data becoming HTML, fast and cacheable.

At first, the 11ty site didn't fully replace the XSLT pipeline — it consumed it. The build was two steps: run the XSLT script to transform the XML into HTML, then feed that output into 11ty. It worked, but it was slow and inelegant.

Eventually I had Claude implement the XML parsing natively in JavaScript as a [custom 11ty data source](https://claude.ai/share/4c09b736-1c90-4b32-aa11-79ba08807a1f), reading the XML directly. Claude generated the JS from the existing XSLT with no real trouble — which says something about how well-defined the transformation logic already was. Now it's a single unified build process, noticeably faster. The XSLT files still live in a separate folder in the repo, kept for reference.

---

## Step 4: Pulling in the Audio Classes

I already had a separate project that predated this one: a [Flutter mobile app](https://play.google.com/store/apps/details?id=org.yrappdev.shaar_hayichud&hl=en_US&pli=1) for listening to audio classes on Sha'ar HaYichud, with the audio files hosted on AWS S3. The app had a data file in a custom markup format — my source of truth for all the classes: titles, structure, sets of classes from different rabbis, ordering, everything.

I had Claude read the original Dart parsing code for that format and reimplement it in Node/TypeScript for the 11ty build. The source file — a custom markup format containing all class titles, structure, ordering, and metadata — is [here](https://github.com/yringler/shaar-hayichud-sections/blob/master/data.txt). With some iteration, it worked. Now the static site built all the audio class pages automatically from the same data file that drove the mobile app.

The audio files themselves [moved from AWS S3](https://claude.ai/share/c3b1e61b-5ce4-4f77-aec4-f3565dba4f37) (complicated, expensive-feeling, hard to reason about) to **Cloudflare R2**. Cloudflare has a web GUI for migrating data between buckets — a few hundred MP3 files transferred in seconds. R2 makes it trivial to expose a bucket through a custom domain, so the files are now served from `media.shaarhayichudresources.com`, with proper CORS headers configured directly in Cloudflare Pages. One small config change to the data file's base URL, a rebuild, and everything pointed at the new location.

---

## Step 5: A Round-Trip CMS on Static Infrastructure

This is the part I'm most pleased with.

The first step was getting the 11ty build to expose the raw XML files and a JSON index as part of its output — a static "API" with zero server required. Once that was in place, the Angular editor was already deployed at its own subdomain. I configured CORS headers on the static site to allow requests from the tool's subdomain, and now the editor could fetch the JSON index, populate a dropdown of all files, and load whichever XML the user selected — directly from the static site, no manual copy-paste from the IDE.

That handled reads. For writes, I needed something server-side. The GitHub API is the answer I didn't know existed [before Claude surfaced it](https://claude.ai/share/4f83ac5b-aeb4-4c4d-882b-eb97a9018a54): you can commit a file to a GitHub repository with a single authenticated POST request. No cloning, no `git` commands, no server maintaining local state. You give it the repo, the path, the content, the commit message, and a personal access token — and GitHub handles everything else.

I added a Cloudflare Pages Function to the editor's repo. The Angular app posts the filename and updated XML content to the function; the function authenticates using a secret token (stored as a Cloudflare Pages secret) and makes the GitHub API call. Four secrets configured, a small function deployed, and I had full round-trip editing: load from the static site, edit in the GUI, save back to the repo.

For security, nothing fancy: a long random token generated with a single `openssl` command, stored in Cloudflare as a secret, saved in my password manager, and cached in localStorage after first entry. Not enterprise auth — but appropriate for a personal tool where the write endpoint commits to a specific repo.

The end result: a full GUI CMS, with GitHub as the database. No backend, no database server. Cloudflare Pages and Workers are free at this scale — the only thing I'm paying for is a domain name.

---

## The Architecture, Zoomed Out

What I ended up with is a nice illustration of a principle I've come to appreciate: **scale your complexity to your actual needs, in parallel layers.**

On the server side:
- **Static output** handles almost everything — HTML, structured data, raw XML, JSON indexes. No server needed.
- **A single edge function** handles the one thing that genuinely requires server-side logic: authenticating and proxying the GitHub commit.
- If needs grew more complex, there's a clear path to fuller server infrastructure — but why pay that cost before you need to?

On the client side:
- **No JavaScript** on the public-facing site. Pure HTML and CSS, fast and cached everywhere.
- **Sprinkled JavaScript** could handle small interactive needs if they arise.
- **A full Angular app** at a separate subdomain handles the complex, stateful editing workflow.

One underrated part of this whole setup: Cloudflare Pages gives you a live preview URL for every branch, automatically. That meant I could have an idea, describe it to Claude Code, push the branch, and immediately have a real deployed URL to test on my phone — all while rocking a baby to sleep. The feedback loop between idea and working preview was tight enough that a lot of this got built in genuinely stolen moments. Claude Code handled all of the infrastructure code: the GitHub Actions workflows (before everything moved to Cloudflare), the Cloudflare function, the data parsing rewrite, the CORS configuration, the GitHub API integration. I provided the architecture instincts and the domain knowledge. The combination worked.

---

The site is live at [shaarhayichudresources.com](https://www.shaarhayichudresources.com/en/) — Sha'ar HaYichud with full section divisions, audio classes, and (eventually) English translation. It's a long-term project, but the infrastructure is now genuinely in place to support it.

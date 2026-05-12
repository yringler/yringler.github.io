---
date: 2026-05-19T00:00:00-05:00
slug: "why-i-abandoned-my-sophisticated-ai-coding-workflow"
url: "/2026/05/19/why-i-abandoned-my-sophisticated-ai-coding-workflow/"
title: "Why I Abandoned My Sophisticated AI Coding Workflow"
tags: [ai, ai-generated]
series: AI-coding-shift
series_part: 1
---

A few months ago I [wrote a post](/2026/01/22/parallel-ai-coding-prerequisites/) arguing that AI parallelism would force developers to take clean architecture seriously, because coupling now has an immediate cost in blocked parallel work. I still think that's true. But I want to start this series with a confession: the elaborate workflow I built on top of that insight is mostly not what I actually do anymore.

This isn't a retraction. The economic argument holds. What I got wrong was the workflow that I thought followed from it.

## The Workflow on Paper

Here's what I designed, and what I genuinely believed was the responsible way to do AI-assisted development:

Spin up multiple agents in separate git worktrees, each working on a bounded task carved out of a plan. As each one finishes, do a fast tactical review and merge it into an intermediate staging branch. Once the whole set is integrated, open a single formal PR from the staging branch to main and do a strategic review there — not "is each piece correct" but "did these collectively move us toward the goal."

Two-stage review. Tactical correctness validated quickly per-agent, strategic coherence validated once at the end. Worktrees prevent merge conflicts. The staging branch creates a low-stakes parking place for work that's "done enough" but not "done done." Everything bounded, everything reviewable, everything responsible.

I was proud of it.

## What Actually Happened

I stopped using it. Not all at once and not deliberately — I just slowly noticed that I wasn't doing it anymore.

The honest reason is that it required more sustained focus than I could actually deliver. Spinning up four agents, holding their contexts in my head, doing fast tactical reviews on each, then context-switching back up to do a strategic review of the integration — that's a lot of cognitive load to maintain for what is, in my case, a side-project schedule with kids and a day job pulling at the other side.

Meanwhile, I was shipping smaller things — [a scrum poker app](https://poker.yehudardevelopment.com/), some utilities, eventually starting a lectures app — using a much looser approach. Write a prompt. Let Claude Code run. Glance at the output. If it works, ship it. If it doesn't, look at it briefly, decide whether to iterate or throw it away. No worktrees. No staging branches. No two-stage review. Just *prompt, glance, ship.*

It felt irresponsible. It was also working better than my responsible workflow, because the responsible workflow wasn't actually running.

## The Sophistication Trap

This is the part I want to sit with, because I think it generalizes.

A workflow you don't execute is worth zero. A messier workflow you actually execute is worth something. This is obvious when stated plainly, but it's hard to internalize when you've designed something that *looks* correct on paper and want to defend it.

What I built was a workflow optimized for the assumption that line-level review was the locus of quality. Every piece of it — the bounded tasks, the per-agent reviews, the staging branch — was there to make sure I could trace every line of generated code through a review gate before it landed. The two-stage structure was an admission that I couldn't review every line in one pass, so I split the review into smaller passes.

But the underlying assumption was wrong. Line-level review of AI-generated code isn't where quality lives, at least not for me. I'll come back to where quality actually lives in later posts. For now the point is just that I was building elaborate machinery to enforce a discipline that didn't matter, and the elaboration is what made it unsustainable.

## What Replaced It

What I actually do now is roughly this:

I think about the problem hard, often away from the keyboard. When the problem is non-trivial I open a long-form chat with Claude and we go back and forth on architecture until the design feels solid. That conversation produces an artifact — usually a fairly detailed prompt file. Then I hand that prompt to Claude Code and let it run. When it comes back I look at the result at the *architectural* level: are the boundaries right, are responsibilities in the right places, is anything in there that smells structurally wrong. I don't read every line. Bugs that surface during use get fixed; if the AI struggles unusually hard to fix one, that's a signal to look at the architecture, not to keep prompting.

For larger projects this scales by running multiple Claude Code sessions at once — different parts of the codebase, different features. The worktree mechanics still apply. What's gone is the heavy review machinery in between. Each session produces something I can test by using it. If it works, it works.

This is what people call "vibe coding," more or less, and the name has a dismissive edge to it. I want to push back on that. What I'm doing isn't unprincipled — it's principled at a different layer. The principles moved up the stack. Architectural review still happens, rigorously. Strategic decisions about what to build and what to throw away are still mine. I just stopped pretending I was going to verify every line.

## The Reframe

If I had to name the shift in one sentence: **responsibility in AI-assisted development isn't line-level review, it's strategic oversight at the right altitude.**

That sentence is going to do a lot of work across the rest of this series. The next post is about what "the right altitude" means in practice — how to recognize when AI is struggling because the problem is hard versus when it's struggling because something further up is broken, and what to do in each case. The third post is about the operational layer: which model to use when, and the harder discipline of throwing away expensive work that turned out to be on the wrong track. The fourth post returns to the economic argument I made in January and tries to draw out its real consequences — which I now think are bigger than I gave them credit for.

I want to keep the original post up, and I don't want to walk it back. The forcing function is real. What I had wrong was the response. I built a workflow that respected the forcing function but didn't respect my own limits, and the result was a beautiful piece of methodology gathering dust while a shabbier-looking practice was doing the actual work of shipping software.

The shabbier practice turns out to have its own structure. That's what the rest of the series is about.

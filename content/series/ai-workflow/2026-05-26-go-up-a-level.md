---
date: 2026-05-26T00:00:00-05:00
slug: "the-real-skill-is-knowing-when-to-go-up-a-level"
url: "/2026/05/26/the-real-skill-is-knowing-when-to-go-up-a-level/"
title: "The Real Skill is Knowing When to Go Up a Level"
tags: [ai-generated, in-review, ai, coding]
series: AI-coding-shift
series_part: 2
---

In [the first post](/2026/05/19/why-i-abandoned-my-sophisticated-ai-coding-workflow/) I argued that responsibility in AI-assisted development isn't line-level review — it's strategic oversight at the right altitude. This post is about what that means in practice. Specifically: how to recognize when the right move is to stop pushing at the current level and step up a layer.

This is the single most useful pattern I've found, and it shows up at every scale.

## The Pattern

Whenever something isn't working — a bug AI keeps failing to fix, a feature it keeps implementing wrongly, a plan that keeps generating awkward code — the wrong response is to push harder at the same level. The right response is almost always to go up one.

- Stuck on a bug → check the architecture around it.
- Stuck on a feature → check the spec.
- Stuck on a spec → check the problem framing.
- Stuck on the problem framing → check whether you're solving the right problem at all.

This is the opposite of what sunk-cost thinking produces, which is always *"just one more attempt here."* Pushing harder feels productive because each individual try is cheap. Stepping up a level feels expensive because you're abandoning visible progress to redo something that already seemed done.

But the economics are flipped from how they feel. Retries at the wrong level burn tokens with low expected value — you're trying to solve a problem that has the wrong *shape*. Going up a level changes the shape of the problem, which is where the real expected value is.

## AI Friction Is a Signal

The trigger for going up a level is almost always the same: AI is struggling more than it should.

This is a real diagnostic, and it took me a while to trust it. I used to interpret AI struggle as a capability problem — wrong model, bad prompt, needs more context. Sometimes that's right. But more often, when I saw Sonnet (or even Opus) thrashing on what should have been a routine task, the real problem was that the surrounding code had tangled dependencies or a leaky abstraction, and the "correct" fix required understanding a wide context that the model couldn't hold coherently.

The model isn't dumb. The problem is shaped wrong.

I had a bug recently in the lectures app — a piece of state that should have been trivial to update kept producing the wrong result. Sonnet tried, failed, tried a different angle, partially fixed it but broke something else. The instinct was to switch to Opus and try again with more capability. Instead I asked Opus *not* to fix it — to trace the data flow from source to where the bug manifested and recommend architectural improvements. It came back with a clear picture: there was a layer of indirection missing, the state was being touched in two places that should have been one, and the bug was just the visible symptom of that. Once the architecture was fixed, the bug went away on its own, and the area was easier to work in afterward.

The bug wasn't the problem. The problem was the architecture, and the bug was just where it surfaced.

## Plan Review Is Where Leverage Lives

If AI friction during implementation tells you to go up a level, the inverse is also true: time spent at the higher level prevents friction later. The single highest-leverage moment in my workflow is reviewing a plan before any code gets written.

Plan mode in Claude Code is the lightest form of this — the agent describes what it's about to do before it does it. Even at that scale, the review catches a lot. The most common thing I catch is what I think of as *additive complexity:* the AI's bias toward adding rather than replacing.

A real example. I had a piece of functionality that handled some flow one way, and I needed a new feature that required handling it differently. The plan that came back proposed supporting both — keep the old path working, add a new path for the new case. Two ways of doing the same thing. From the AI's perspective this is the safe move: it doesn't break any existing callers, it adds the new capability, and someone else can decide later whether to consolidate. From my perspective the old path didn't actually need to exist anymore. I told it: *just switch entirely to the new way.* The resulting plan was simpler, the resulting code was simpler, and a whole category of future confusion was eliminated before a single line was written.

This is the pattern I keep seeing. AI defaults to additive solutions because additive solutions are locally safe. It doesn't have the product context to know whether the old path *should* exist. That decision has to come from you. And the cheapest place to make it is in the plan, not in the code.

One sentence at planning time can save hundreds of lines of code and the eventual refactor to remove them.

## Re-architect, Don't Re-prompt

The bigger version of the same lesson hit me on a refactor in the lectures app. I had a data model where any item could have multiple parents. It seemed clean and flexible when I designed it — a generalization that didn't cost much. But every feature that needed to know *where* in the hierarchy something lived had to handle the general case: walk multiple parents, deduplicate, decide which path to display. Each feature was slightly harder than it should have been.

Eventually I was trying to add a progress-tracking feature, and Opus, mid-planning, flagged the problem directly: *"There's no clean way to compute a single path through this hierarchy. How do you want to handle this?"* It offered me a few options.

My first instinct was to pick an option and move on. Instead, after some staring, I realized the right answer was that I'd been wrong about needing multi-parent in the first place. No real use case required it. The flexibility was speculative. I threw away the planning work, did a separate refactor to collapse the model to a single parent, and *then* came back to the feature. The feature became straightforward.

The thing I want to name here is what Opus did. It didn't unilaterally re-architect the data model — it shouldn't have, that's a domain decision. But it surfaced the architectural concern as a question and put it in front of me. That moment, where a planning model elevates something from implementation detail to architectural question, is exactly the human-in-the-loop moment the whole workflow depends on. When it happens, pay attention. The model isn't being indecisive; it's pattern-matching on something that's going to block you.

## The Junior Dev Analogy

The cleanest framing I've found for all of this is the senior-dev / junior-dev relationship.

When a junior dev fails at a task, the failure is rarely pure incompetence. It's almost always that the task was underspecified, the codebase wasn't prepared for it, or the problem crossed boundaries they couldn't navigate alone. A good senior responds by decomposing the task, cleaning up preconditions, or recognizing that this isn't a junior-appropriate task in the first place. *Not* by standing over their shoulder saying "try again."

AI agents fail in essentially the same ways and respond to the same management. If the AI can't do something, the solution is not to keep pouring tokens into reprompting. It's to ask whether the task is well-scoped, whether the surrounding code supports it, and whether the architecture lets the change be local. If the answer is no, the responsibility is yours — you went up a level too late, or you handed off a task you shouldn't have.

And there's a discipline embedded in this that I want to make explicit: **don't accept code the AI had to fight to produce.** It's tempting, because you *can* often force something to work — enough prompting, enough manual intervention, and the tests pass. But you've now accumulated hidden debt. Code the AI struggled to write is code the AI will struggle to maintain, extend, and reason about later. The difficulty wasn't incidental. It was diagnostic.

Sometimes the right call is to defer the feature until you have time to do the architectural work properly. That feels like slowing down, but shipping duct-taped code in an AI-assisted workflow is worse than in a traditional one, because every future AI session that touches that area pays the tax forever.

## What This Costs You

Going up a level is psychologically expensive in a way the math hides. You're throwing away visible work — a partial implementation, a generated plan, sometimes hours of conversation. Sunk cost screams at you to push forward. The cost of the alternative is invisible, distributed across every future session that has to work in the messy area you didn't fix.

The most useful single discipline I've developed is the willingness to discard. Code, plans, prompts, sometimes entire architectural directions. The artifact is disposable. The understanding you built while producing it isn't — that stays with you, and the next attempt is faster and sharper because of it.

Which brings me to the operational layer of all this — which models to use for which kind of work, and the specific discipline of throwing away expensive output. That's [the next post](/2026/06/02/model-tiering-and-the-sunk-cost-trap/).

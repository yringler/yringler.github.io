---
date: 2026-06-02T00:00:00-05:00
slug: "model-tiering-and-the-sunk-cost-trap"
url: "/2026/06/02/model-tiering-and-the-sunk-cost-trap/"
title: "Model Tiering and the Sunk Cost Trap"
tags: [ai, ai-generated]
series: ai-coding-shift
series_part: 3
---

[The previous post](/2026/05/26/the-real-skill-is-knowing-when-to-go-up-a-level/) was about *when* to go up a level. This one is about the operational layer underneath that decision: which model to use for which kind of work, and the harder discipline that makes the whole thing actually work — being willing to throw away expensive output.

The two topics are connected. If you're not willing to discard, your model choices don't matter, because you'll end up patching whatever the cheapest model produced regardless of how wrong its foundation was.

## The Tiering I Settled On

The split I use, roughly:

**Opus for planning and architectural review.** This is where capability matters most. Planning is where one missed implication or one undetected coupling becomes hours of downstream pain. Architectural review is the same — you're asking the model to hold a wide context and reason about how parts of a system interact, which is exactly what stronger models are better at. The cost is justified because the decision being made affects everything that comes after it.

**Sonnet for implementation against a well-specced plan.** Once the architecture is decided and the spec is tight, implementation is mostly mechanical. Sonnet is fast, cheap relative to Opus, and more than capable when the task is well-bounded. The trick is that this only works *if* the planning was done with a stronger model — Sonnet implementing a vague spec produces vague code.

**Gemini (free tier) for prototyping and proof-of-concept.** This sounds backwards at first — why give the lowest-capability tier the role of trying things out? Because the prototypes are *supposed* to fail, and a model that struggles is more informative than a model that papers over the difficulty.

## The Cheap-Model-As-Stress-Test Trick

This is the part of the tiering I find most useful and least obvious.

When I'm building something I don't fully understand yet — a new library, an unfamiliar service, a feature I haven't designed before — I deliberately start with a cheap model running an early version of the prompt. The output is usually bad. That's the point.

A weaker model fails in *informative* ways. It surfaces the parts of the spec that were underspecified, because it can't make the leaps a stronger model would silently make to cover the gaps. It writes the awkward implementation that reveals the awkward architecture. It surfaces edge cases I hadn't thought through, by getting them wrong loudly.

The Gemini run isn't trying to produce shippable code. It's a *spec refinement loop.* I look at what it got wrong, ask why it got wrong, and discover that the real issue is something I didn't specify. The prompt gets sharper. The architecture gets clarified. By the time I'm ready to actually ship a version, the spec is battle-tested — and *then* I run it with Sonnet, and the result is much cleaner than if I'd jumped straight to Sonnet on the original sketchy prompt.

This is counterintuitive because it looks like wasted work. It isn't. The cheap-model failure was load-bearing. You couldn't have written the final prompt without going through it.

## The "Never Patch Upward" Rule

The other rule that fell out of using multiple models is: **never use a stronger model to fix a weaker model's output.**

If Gemini's code has a problem that Sonnet can fix, fine — that means the problem was within Gemini's tier and I just need to keep iterating with Gemini. If the problem requires Opus to even understand, then I shouldn't have been using Gemini for that task in the first place. Patching with Opus means I'm paying twice — once for the bad attempt, once for the fix — and ending up with code of uncertain coherence, half-written by one model and half-patched by another.

The right move when a weaker model can't fix its own output is to escalate the whole task. Throw away what it produced. Re-spec if needed. Run the task with the stronger model from the start.

There's a partial exception, which I want to name honestly: sometimes I'm in a rush and I'll let Opus fix a Sonnet bug just to ship. I notice when I'm doing it. It's a deliberate cost — I'm trading code coherence for time. The policy isn't iron, but I try not to drift into doing it by default, because that's how you end up with codebases that no model can reason about cleanly.

## Throwing Away Expensive Work

Here's the hardest part, and the one that took me longest to internalize.

I've thrown away substantial work in this process. Opus planning sessions that ate real chunks of my usage allowance. Implementation runs that took an hour to set up and another hour to discover were on the wrong track. Multiple prototypes of the same feature, each abandoned because something earlier in the chain needed to change.

The instinct to keep iterating on a bad foundation is incredibly strong, *especially* when the foundation cost money to build. Sunk cost screams. The plan looks reasonable, the implementation is partially working, *one more fix* and it'll be done. Don't.

The thing I had to learn — and I'm still learning — is that **the artifact is disposable but the understanding isn't.** When I throw away a plan, I don't throw away what I learned writing it. The next plan gets written faster and is more grounded because of the discarded one. When I scrap an implementation, the bugs and friction I saw in it inform the next attempt. The knowledge stays with me. Only the output goes in the trash.

This reframes the cost. The expensive Opus planning session that I discarded wasn't wasted — it was the price of learning what the real problem was. The bad Gemini prototype wasn't wasted — it was the price of refining the spec. The thrown-away Sonnet implementation wasn't wasted — it was the price of finding the architectural issue underneath.

A clean run on a solid spec produces better code than ten iterations patching toward the same target — even if the total token cost ends up similar. Accumulated corrections leave scar tissue. Fresh implementations on proven specs don't. *Get it right the first time on the third try* is a real principle, not a contradiction.

## The Compound Discipline

Tiering and discarding work together. If you tier models well but can't discard, you'll end up using Opus to patch Sonnet's mistakes and producing hybrid code that nobody — human or model — can reason about cleanly. If you can discard but don't tier well, you'll churn through expensive attempts solving the wrong problem with the right model.

The combined practice is something like:

1. **Plan with the strongest model you can afford.** This is the highest-leverage moment.
2. **Prototype with the weakest model that can run the prompt.** Use its failures to refine the spec.
3. **Implement with the cheapest model that can do the task cleanly given the refined spec.**
4. **When something is off, escalate the whole task — don't patch across tiers.**
5. **When something is fundamentally off, throw it away and restart from a better starting point.**

None of this requires elaborate workflow machinery. It requires a willingness to spend resources unevenly — pouring cost into planning and review, being parsimonious during implementation, and accepting that some fraction of work is going to be discarded by design.

That last part is worth saying clearly: **a workflow where nothing gets thrown away is a workflow that's accumulating debt.** The model that never had its output discarded is a model whose mistakes are now load-bearing in your codebase. Discarding isn't a sign of failure. It's a sign that the quality control is actually running.

## Where This Leaves Us

Three posts in, the picture is something like: don't review every line, do review architecture; when AI struggles, go up a level rather than push harder; use stronger models where their reasoning matters and cheaper models where their failures are diagnostic; and be ruthless about discarding work that was on a wrong track.

What this all serves is the original economic argument I made [back in January](/2026/01/22/parallel-AI-coding-prerequisites/) — that clean architecture has immediate value now, not deferred value. I want to come back to that argument [in the final post](/2026/06/09/architecture-has-immediate-economic-value-now/), because I now think its consequences are bigger and stranger than I gave them credit for. Some of the tradeoffs that defined software engineering for decades aren't tradeoffs anymore.

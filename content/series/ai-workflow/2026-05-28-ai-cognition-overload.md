---
title: "Addendum 1: AI Coding as Superstimulus"
tags: [ai-generated, ai, coding]
series: AI-coding-shift
series_part: 5
---

Every compulsive behavior I'd ever heard warned about had one thing in common: it was obviously a waste. Junk food, endless scrolling, the worse stuff a person can lose an evening to — the harm announces itself. You know what you're doing while you do it. The internal argument is short because the verdict is never in question. You're not building anything. You're feeding a loop. The recognition that it's destructive is what eventually lets you stop, or never start.

AI coding broke that pattern for me, and it took a while to notice, because nothing about it looked like a problem. I was shipping. The architecture was clean. I was planning before I prompted, reviewing what came back, making real decisions. By every external measure I was being a responsible engineer. And I still walked away from some of those sessions feeling the specific kind of hollowed-out that I associate with having been *had* — the feeling of a reward circuit that got run harder than it should have.

AI coding is the first activity I know of that is genuinely productive and a compressed dopamine loop at the same time. The two used to be mutually exclusive. Now they're the same act.

### The gap that used to be there

There's an old idea from ethology that explains the mechanism better than anything I could invent. In the 1930s the Dutch biologist Niko Tinbergen noticed that certain birds, given a choice between their own pale, speckled eggs and an enormous garish plaster fake, would abandon the real eggs and try to incubate the dummy.[^1] Herring gull chicks pecked harder at an exaggerated cartoon of a beak than at an actual parent. He called these things *supernormal stimuli*: artificial versions of a natural cue, dialed past anything that occurs in the wild, that hijack an instinct evolved for the real version. The fake wins because the instinct was never calibrated for a world that contained the fake.

Decades later the Harvard psychologist Deirdre Barrett took that concept and pointed it at us.[^2] Her argument is that most of modernity's traps are supernormal stimuli aimed at drives that made sense on the savannah and make no sense now. Sugar and fat tuned past anything in nature. Pornography tuned past any partner. The instinct fires at full strength on the fake, because evolution had no reason to install a ceiling.

What all of Barrett's examples share is that they're *substitutes*. The candy stands in for nutrition you don't get. The screen stands in for a relationship it can't actually be. The stimulus is hollow, and on some level you can feel the hollowness even while you can't stop. That hollowness is doing important work. It's the tell. It's how you catch yourself.

Now hold that next to what AI coding does to the structure of building software.

The natural reward in programming was always gated by effort. You wanted the thing to exist; you worked, often for a long time, often through frustration; and then it existed, and the satisfaction arrived. The gap between *I want this* and *here it is* was wide, and the width was the point. Your nervous system learned to associate the reward with the work, because the work was the only path to the reward. That's the call-and-response the whole motivational system is built on.

AI coding collapses the gap to nearly zero. You describe the thing and the thing appears. Not a toy version — the real feature, in your real codebase, often better-structured than you'd have bothered with by hand. The desire-to-result distance that used to be measured in hours or days is now measured in the length of a prompt. That is, structurally, a supernormal stimulus. The reward your brain evolved to grant for *building something* is now available at a fraction of the cost it was calibrated for.

### Why this one is worse than the obvious ones

Here's where it stops being a fun analogy and starts being a real problem.

Every supernormal stimulus Barrett describes is recognizable as an escape. That recognizability is the safety mechanism. The reason a person can eventually quit the junk is that there's nothing on the other side of it — no output, no artifact, no defensible reason to keep going. The behavior and the harm point in the same direction, so the harm-reduction heuristic — *is this destructive?* — fires cleanly and gives you something to push against.

AI coding defeats that heuristic completely. You ask *is this destructive?* and the honest answer is no. You built a working app. The tests pass. You shipped. The heuristic returns "all clear" because by its own logic everything is clear. There's no hollowness to catch, because the output isn't hollow. It's real. The compulsive version of the behavior and the responsible version are the same behavior, producing the same artifacts, and they feel nearly identical from the inside.

So the usual escape hatch — *notice it's a waste, then stop* — doesn't exist here. There's nothing to notice. You can run that reward loop for ten hours, produce genuinely good work, and have your judgment quietly outpaced by the loop the entire time without a single signal that anything is off. The productivity is the camouflage.

And the displacement is the same as with any other superstimulus, just aimed somewhere less obvious. The way an artificial stimulus can make a real relationship feel flat by comparison, AI-velocity building makes ordinary work feel unbearable. A normal engineering task — the kind with friction, where you grind for an afternoon for an hour's worth of visible progress — can't compete. Why would it? You know exactly what that same afternoon could have produced with an agent. The dynamic ranges don't reconcile. Once you've felt the compressed loop, the slow one feels broken, even when the slow one is the healthy one.

### Metacognition as neurological hygiene

I've come to think of metacognition — the running awareness of your own state while you work — as the load-bearing skill of using AI well. I used to frame that purely as a methodology thing: am I using the right model for this, is my architecture actually clean, am I going up a level when the AI struggles instead of throwing more tokens at it. All true. But there's a second axis I missed for a while, and it's the more important one.

The question isn't only *am I doing this correctly?* It's *am I actually deciding right now, or am I being pulled forward by a loop that's faster than my judgment?* Those produce identical-looking sessions. The only place the difference is visible is from the inside, and only if you're looking. The skill is the looking.

There's an obvious-sounding answer to all this, and it's a good one for the right person: put the gap back by hand. Plan with the AI but write the implementation yourself. Force a deliberate step between deciding and acting — sleep on the decision, write the spec out longhand, make yourself do the boilerplate so you feel where the architecture is awkward. Re-impose the friction the tool removed. That genuinely works. It re-attaches the reward to something your hands did, which is the natural pathway, not the compressed one. If you're earlier in your career and still building architectural taste, or you're not under hard time pressure, it might be the right way to work, full stop.[^3]

But that's not for me. My AI projects run on the side, in whatever hours exist around everything else. The whole reason I lean on AI for nearly all of it is that I don't have the time to do otherwise — that's the constraint, not a preference I could simply revise. There is no afternoon to spend hand-writing implementation as a calibration exercise. There's no space to add space. The friction solution assumes a slack in the schedule that, for me, is exactly the thing that doesn't exist.

So when the standard advice says *slow down and plan*, I can't read it as a structural fix, because I can't actually slow down. What's left when you strip out the room to maneuver is one tool, and it's the one I keep coming back to: self-awareness and care. The same metacognition that catches a bad model choice or a coupling problem, turned inward and asked to do a second job it isn't usually credited with — noticing, in the moment, when the loop has gotten ahead of the judgment, and pulling back on nothing but that noticing. No imposed gap. Just the watching, while going full speed.

### Living inside it

I don't think there's a perfect solution, and I'm suspicious of anyone selling one, because the root cause isn't a bad habit you can break — it's a mismatch between an ancient reward system and a tool that was impossible to build until about two years ago. We're the first cohort to run this experiment, and we're running it on ourselves. The honest answer is that there's no off switch, because — unlike the obviously-destructive superstimuli — you don't want there to be one. You should keep building. The output is real.

What's left is awareness. Noticing, while it's happening, that the direction you're being pulled is partly the work and partly a circuit firing on a fake it can't distinguish from the real thing, and correcting against the pull on the strength of that noticing alone. The hope — and for me it's mostly held — is that the correction doesn't stay effortful forever. Catch yourself often enough and some of it becomes the new baseline, the way any practiced discipline eventually metabolizes into something closer to taste. You end up able to operate at this velocity without the velocity operating you.

That's a harder ask than "don't do the obviously bad thing." But it also points somewhere better than the old version of the problem ever could. The compulsive behaviors we used to warn about led nowhere by definition. This one, managed, leads to the actual work — just with a reward system you've had to teach, on purpose, to keep up.

[^1]: Niko Tinbergen, the Dutch ethologist who coined the term *supernormal stimulus* in the 1930s–50s. His experiments showed birds preferring exaggerated artificial cues — oversized, over-colored dummy eggs; cartoonishly enlarged beak models — over the real signals their instincts evolved to track.

[^2]: Deirdre Barrett, *Supernormal Stimuli: How Primal Urges Overran Their Evolutionary Purpose* (W. W. Norton, 2010). Barrett extends Tinbergen's concept to modern human behavior, arguing that instincts shaped for a pre-industrial environment are routinely hijacked by engineered stimuli — processed food, pornography, mass media — that exaggerate natural cues past anything our regulation was built to handle.

[^3]: This "plan with AI, code by hand" approach isn't mine — it comes from a developer far more cautious about handing implementation to AI than I am (I'll link him here once I track down the source again), and I think it's a genuinely good operating point for someone whose constraints allow it.

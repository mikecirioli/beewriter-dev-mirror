# Unify/Diataxis: generate a tutorial

*Tutorials work differently from the other three page types in two ways. Read the two notes below before the rest.*

## Two things that make tutorials different

**1. You answer the six design questions yourself, and tutorials are the type most likely to stop at pipeline step 5.** Before any outline exists, a tutorial needs answers to "what will the learner build," "who is the learner," "what must be ruthlessly excluded," and three more. **Answer them yourself** from the ticket, linked PR, and product repo, and state the answers and your reasoning in the PR description — exactly the same pattern as the type decision in `skills/draft-docs/profiles/unify-diataxis/analyse.md`. The difference from the other three generators: these questions are a genuine product-sense judgment (what's a meaningful, safe, concrete thing for a *learner* to build), more than they are a fact-finding exercise. If you can't answer all six with real confidence from what's available, **that is `skills/draft-docs/SKILL.md` pipeline step 5** — don't force a design decision past the point where it's actually guessing. Expect tutorials to hit that stop-before-drafting outcome more often than how-to, explanation, or reference content does. That's the design working correctly, not a gap in it.

**2. Correctness is checked by readers after publishing, not by a person testing every step first. That's a deliberate choice, not a shortcut.** A tutorial PR goes through the same path as any other content (writer review, same as always), but **nobody is expected to click through the product confirming every step works** before it merges. Instead, a published tutorial is watched the same way the rest of the plan already watches reader quality — PostHog signal where it exists, support tags, direct feedback — and problems get fixed from that signal, not caught in advance.

This only works once there's enough example content for your own judgement to be worth something, and `skills/draft-docs/profiles/unify-diataxis/examples/` has no curated tutorials yet. So the practical consequence today is to be **more conservative, not less**, about the six design questions above: if the ticket, linked PR, and product repo don't support real confidence in all six, that's `skills/draft-docs/SKILL.md` pipeline step 5, not a plausible-sounding guess papered over by "a reader will catch it eventually." The deferred-testing model is what you accept *once a tutorial is confidently designed and drafted* — it isn't permission to lower the bar for getting there in the first place.

**This is an interim position.** Testing tutorial steps before publishing may come later, as part of a separate review and verification step. That's out of scope for this skill, so don't try to solve it here.

Still state this plainly in every tutorial's PR description — not as an instruction to go test it, but as a disclosure of which quality-assurance model applies: *"This tutorial's correctness is checked through reader signal after publishing, not by a pre-publish walkthrough. Confidence in the design-question answers above is [state honestly: high / moderate / low], mainly because `skills/draft-docs/profiles/unify-diataxis/examples/` has no curated tutorials yet to judge against."*

## What a tutorial is

Learning-oriented, for someone at study, not at work. The tutorial bears the responsibility for the learner's success — the learner's only job is to follow directions. Contrived and safe: no choices, no real-world branching, always reversible, exact specified values throughout.

| vs. how-to | Tutorial | How-to |
|---|---|---|
| Orientation | Learning | Task |
| Learner is | At study | At work |
| Environment | Contrived, safe, single path | Real-world, branches and forks |
| Values | All specified exactly | General, user brings context |
| Responsibility | The tutorial's | The user's |

Not a tutorial: a real-world task guide (how-to), an explanation of how something works, a spec of options, or "everything you can do with X."

## Answer the six design questions yourself, then say so

**With `skills/draft-docs/profiles/unify-diataxis/examples/` empty, hold a high bar for confidence here** — these six are a product-sense judgement, and judgement grounded in nothing is a guess wearing the shape of a decision. Lean toward pipeline step 5 (not enough to draft) over a confident-sounding answer you don't actually have grounds for.

1. **What will the learner build?** Concrete, visible, achievable within the tutorial, meaningful enough to care about finishing. ("A working pipeline that builds and tests a sample app" — not "an understanding of how pipelines work.")
2. **What will they gain?** Separate from #1 — the skills, vocabulary, and familiarity acquired by doing it.
3. **Who is the learner?** Baseline knowledge; what the tutorial can assume, what it must never assume.
4. **What's the safe starting state?** Reproducible, and the learner can always restart from it.
5. **What are the visible checkpoints along the way?** Not just the end — frequent, small, meaningful results.
6. **What must be ruthlessly excluded?** Anything not required to reach the end result.

State all six, with reasoning, in the PR description. If the ticket, linked PR, and product repo genuinely don't support confident answers to all six — stop before drafting (pipeline step 5), don't guess a learner journey.

## Build the outline (internal step, not a checkpoint)

Introduction (what's built, what's gained, starting state) → sequential sections, each one stage of the journey with an action, a visible result, something to point out, and expectation narrative where the learner might be uncertain → conclusion (what was built, brief reflection, next steps). Check as you build it: no branches, every value specified exactly, the learner can restart at any point, every section produces something visible — if a section produces nothing visible, restructure or cut it.

## Page attribute: `:diataxis-type: tutorial`

Set this near the top of the file, after the `abbr.adoc` include and before the title — confirmed in real Unify pages (e.g. `connect-your-repository.adoc`). `skills/review-docs/SKILL.md` cross-checks it against the actual type decision before output. Applies whether this page is standalone or one part of a series (section 3c) — a series part is still a tutorial.

## Page title

**"Build/Create/Set up your first X"**. This is the docs team's chosen pattern. "Get started with X", seen on some existing pages, is too vague, so don't treat it as an accepted alternative.

- ✅ "Build your first pipeline" / "Create your first component"
- ❌ "Pipeline tutorial" (no outcome) / "Getting started with pipelines" (vague) / "How to create a pipeline" (that's a how-to title)

## Introduction

Concrete from the first sentence, "we" language — tutor and learner together:

```
= Build your first pipeline

In this tutorial we will create a pipeline that automatically builds and tests a sample application every time code is pushed to a repository.
Along the way we will encounter the {PRODUCT} pipeline editor, the relationship between components and pipelines, and what a successful build looks like.
```

Never: "In this tutorial you will learn..." (presumptuous), bullet-pointed learning objectives (turns it into a lesson plan), or "After completing this tutorial, you will be able to..."

## Prerequisites: minimal, specific, never conceptual

"A {PRODUCT} account with the *Developer* role in at least one organization," not "access to {PRODUCT}." Never "an understanding of CI/CD" — tutorials build understanding, they don't assume it.

## Headings need explanatory text immediately after them — same hard rule as every other type

Present-tense doing-phrases ("Connect the repository," not "Repository connection"), each followed by a sentence or two of narrative orientation before any step.

## Writing steps: conversational, narrated, exact

- "We" where natural; narrate what's happening, not just what to do.
- **Narrative of expectation** before any step where the learner might be uncertain: "The build will be queued and should start within a few seconds. You will see the status indicator change from grey to blue."
- **Point things out**, don't explain them: "Notice that the pipeline name appears in the breadcrumb trail." One sentence connecting it to something worth knowing, not a paragraph.
- **Anticipate the likely failure**, don't leave the learner stranded: "If you see `BUILD FAILURE` instead, you have probably [cause] — go back to step 3 and check [thing]."
- **Exact values, always.** "Enter the name `sample-pipeline`," never "enter a name for your pipeline." If a value genuinely must be the learner's own (a repo URL), isolate and flag it explicitly as the one exception.
- **Explanation stays out.** One-sentence inline reason at most, or a link to an explanation page — never a `NOTE` block delivering a paragraph of concept.

## Conclusion

Concrete recap mirroring the introduction's language, genuine and brief acknowledgement ("You now have a working pipeline," not "Congratulations!"), no bulleted "what you learned" recap (patronising), then links to the how-tos and explanation pages for what the learner will want next.

## Related pages (required, every time)

Next logical how-to, explanation for a concept encountered but not explained, reference for anything configured, next tutorial in a series if one exists.

## Navigation

Tutorials go **second** in their sub-area's nav (after explanation, before how-to and reference).

## Examples

Read `skills/draft-docs/profiles/unify-diataxis/examples/` once populated (not yet).

## Before handing off to self-check

Besides the usual style scan: is the design-question reasoning actually in the PR description, with an honest confidence statement? Is the deferred-testing disclosure present? Those two are specific to this file and `skills/review-docs/SKILL.md`'s general pass won't catch their absence on its own.

# Unify/Diataxis: generate an explanation page

*Write the outline as an internal working step, not a deliverable: don't stop for approval between outlining and drafting.*

## What explanation is

Understanding-oriented, read away from active work — "even in the bath." Discusses why and how something works; never instructs. Distinguishing it from the other three types:

| vs. | Explanation is | The other type is |
|---|---|---|
| How-to | Understanding-oriented, read away from work, permits reflection | Task-oriented, used during work, demands action |
| Reference | Discursive, includes perspective, read linearly | Precise, minimal, factual, designed for lookup |
| Tutorial | About study, discusses the "why" | About acquisition, teaches by doing |

Explanation is *about* its topic — it circles the subject from different angles rather than walking the reader through it.

## Build the outline (internal step, not a checkpoint)

1. Opening: what this explains, why it matters, broader context.
2. 3–6 sections, each deepening or broadening understanding, building from foundational to more complex, each connecting to the last.
3. Within each: conceptual focus, context, analogies where they genuinely help, design rationale and trade-offs, implications.
4. A connections section if relevant — related concepts, how-tos for practical application.

Generate directly from this; it's not presented for approval.

## Page attribute: `:diataxis-type: explanation`

Set this near the top of the file, after the `abbr.adoc` include and before the title — the existing convention in real Unify pages. `skills/review-docs/SKILL.md` cross-checks it against the actual type decision before output.

## Page title

**"Understanding [concept]"**, or **"About [concept]"** when "Understanding" doesn't fit:

- ✅ "Understanding Pipeline architecture" / "About security scanning types"
- ❌ "Pipeline architecture concepts" (doesn't signal type) / "How Pipeline architecture works" (sounds like a how-to)

*(Note the known conflict with BeeWrite's own `style.adoc`, which gives "About security recommendations" as a wrong-title example — `shared/beewrite-core.md` resolves this: the Unify profile's convention wins here until BeeWrite is harmonised.)*

## Opening

- Be clear about the conceptual territory and why understanding it matters, in 1–3 sentences.
- **Never start with the page title restated** — "Understanding X helps..." is the exact pattern to avoid. Start with what the concept *is* or *does*.
- `{PRODUCT}` attribute, never a hardcoded name.

```
= Understanding Pipeline architecture

{PRODUCT} uses a controller-agent architecture to distribute build workloads across multiple machines.
Understanding this architecture is essential for designing scalable CI/CD systems, troubleshooting build failures, and making informed decisions about infrastructure capacity.
```

not:

```
❌ "Understanding Pipeline architecture in {PRODUCT} helps administrators design..."
```

## Headings need explanatory text immediately after them — same hard rule as every other type

```
=== The controller-agent model

CloudBees CI uses a distributed architecture where a central controller coordinates build work across multiple agents.
```

Never a heading followed directly by content with no framing sentence.

## Be concise — this is explanation's main failure mode, not length

Explanation drifts toward padding more than any other type. Use this before-and-after example as the calibration:

**Too verbose** (discussing CloudBees-credential vs. social-auth trade-offs across 26 lines, repeating the same point about control vs. convenience three times in different words) compresses to:

```
*CloudBees credentials* provide direct platform control over authentication policies, including multifactor authentication, password requirements, and account recovery.
However, users must manage an additional set of credentials specifically for {PRODUCT}.

*Social authentication* (GitHub OAuth and Google) delegates identity management to external providers, reducing password management burden but limiting organizational control over security policies.
```

Six lines carry the same trade-off the 26-line version did. **If a paragraph doesn't change the reader's understanding, cut it** — this applies more strictly here than in any other profile file.

## Technical depth: enough to build real understanding, not enough to become reference

- **Right level:** "the controller evaluates the agent specification and searches for matching agents; if multiple match, it considers load and queue depth."
- **Too detailed** (this belongs in reference, not here): a weighted-scoring breakdown with exact numeric weights.
- **Too shallow** (doesn't build understanding): "Pipelines run on agents."

## Analogies, used deliberately

Map to something genuinely familiar, make the mapping explicit, don't overextend it, and say where it breaks down if that matters:

```
Think of the controller as a project manager and agents as construction workers.
The project manager coordinates and tracks progress; the workers do the actual building.
The project manager doesn't swing a hammer — that's not their job.
```

## Admonitions sparingly

Explanation should flow as prose. Reserve `NOTE`/`TIP`/`IMPORTANT` for points that genuinely need to interrupt that flow — don't default to one per section.

## Related pages (required, every time)

```
== Related pages

* xref:howto/configure-agent.adoc[Configure an agent]
* xref:reference/pipeline-agent-syntax.adoc[Pipeline agent syntax reference]
* xref:explanation/build-triggers.adoc[Understanding build triggers]
```

Link to how-tos that apply the concept, reference pages with the detailed specs, related explanation pages, and tutorials that teach it hands-on.

## Navigation

Explanation pages go **first** in their sub-area's nav (before tutorial, how-to, reference) — the one place the ordering differs from `skills/draft-docs/profiles/unify-diataxis/generate-howto.md`.

## Examples

Read `skills/draft-docs/profiles/unify-diataxis/examples/README.md` before drafting. It lists live Unify pages to read directly. Lead with `understanding-release-orchestration.adoc` if you only have room to read one closely — it's the tightest model of this file's own "cut ruthlessly" principle in the set. `understanding-components.adoc` carries a known minor caveat (a repetitive opening); read it anyway, just don't copy that specific habit.

## Before handing off to self-check

Quick self-scan: does this read like understanding, not instructions (no imperative "navigate to," no numbered steps)? Could it be read away from the product? Is every paragraph earning its place? `skills/review-docs/SKILL.md` runs the fuller pass regardless.

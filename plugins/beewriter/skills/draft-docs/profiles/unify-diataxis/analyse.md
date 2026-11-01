# Unify/Diataxis: analyse and classify

*Information gaps don't pause the run. They go to `shared/gap-list.md` after drafting, except where step 5 of `skills/draft-docs/SKILL.md` applies (there's nothing to draft at all).*

## Step 1: extract what's there, note what isn't

From the ticket, linked PR, and comparable existing pages (via `shared/jira-ingest.md` and `shared/repo-map-lookup.md`), extract:

- Capability/feature: what does this let users do?
- Technical components, integration points, prerequisites, user impact, access method (UI path, API endpoint, Pipeline syntax).
- Working examples: config, Pipeline code, use cases.
- Constraints, limitations, known issues.
- If this amends an existing page: what changes, what's preserved, what breaks (cross-references, aliases).

Note gaps as you go — don't resolve them here, just mark them. They get classified properly in step 4.

## Step 2: scope and complexity

- Technical scope: installation/config, usage/development, integration, security, administration.
- Complexity: simple (one feature, clear purpose), moderate (several options, some decisions), complex (architectural decisions, multiple integration points).

This mainly affects estimated length and how many sections the draft needs — it isn't a gate.

## Step 3: decide the Diataxis type(s)

Tutorial, how-to, explanation, reference — the standard Diataxis indicators apply (learning vs. doing vs. understanding vs. looking up). **Decide and move on.** State the decision and your reasoning in the PR description (`skills/pr-description/SKILL.md`), and only turn it into a gap-list question if the content genuinely supports two readings that would produce materially different pages — not as a routine confirmation step.

If content spans multiple types, split into separate files per type (BeeWrite's strict-separation rule, unchanged).

## Step 4: classify gaps — this feeds `shared/gap-list.md`, not a pause

- **Critical**: how users access the feature, exact behaviour in different scenarios, error messages, required prerequisites. Missing these risks an actively wrong page.
- **Important**: practical examples, edge cases, troubleshooting, related features.
- **Nice-to-have**: advanced use cases, performance notes, historical context.

Pass this classification straight through to `shared/gap-list.md` once drafting and self-check are done — don't stop here to wait for it to be resolved. The one exception is `skills/draft-docs/SKILL.md` pipeline step 5: if critical gaps are so extensive that no page would be more right than wrong, that's not a gap list, it's a reason not to draft at all.

## Step 5: amendments to existing docs

If this changes a published page: identify which sections, what preserves, what a human needs to re-verify (cross-references, examples). Carry anything genuinely uncertain into the gap list, same as a new-content gap.

## Output of this stage

A short internal record (not a deliverable in itself) of: the chosen type(s), the light outline, and the classified gap list — feeding directly into `skills/draft-docs/profiles/unify-diataxis/generate-howto.md` (or the matching generator for the chosen type) and then `shared/gap-list.md`. No stop here, no "approve this outline" step.

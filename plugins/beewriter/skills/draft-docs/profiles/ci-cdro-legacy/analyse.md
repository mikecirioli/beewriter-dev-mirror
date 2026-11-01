# CI/CDRO legacy: analyse and classify

*Based on the page-type rules CI and CD/RO writers already use. This runs unattended: there's no step where a person confirms the page type. State the decision and your reasoning in the PR description instead; the draft PR and gap list are the review surface.*

**This profile does not use Diataxis.** It uses the plugin's own page-type model — Procedure, Concept, Reference, Landing — and BeeWrite's own house convention for mixing explanatory and procedural content on one page. **Do not import Unify's strict type-separation rule or its Tutorial/Procedure title exemptions into this profile.** That was a real methodology error made and corrected once already — see "What this profile is not" below before touching anything here.

## Step 1: extract what's there, note what isn't

From the ticket, linked PR, and comparable existing pages (via `shared/jira-ingest.md` and `shared/repo-map-lookup.md`), extract:

- Capability/feature: what does this let users do?
- Technical components, integration points, prerequisites, user impact, access method (UI path, CLI, API).
- Working examples: config, pipeline/plugin definitions, use cases.
- Constraints, limitations, known issues.
- If this amends an existing page: what changes, what's preserved, what breaks (cross-references, aliases).

Note gaps as you go — don't resolve them here, just mark them.

## Step 2: decide the page type

**Procedure** (action-oriented, "how to do X"):
- Triggers: steps, sequences, instructions; verbs like "configure," "install," "troubleshoot," "deploy"; the goal is to accomplish a specific task.
- Title: verb-first, not a gerund (`style.adoc`'s real rule — "Configure X," "Install X," "Deploy X," never "Configuring X" or "Installing X"). The only literally banned generic words are *Use, Work with, Overview, Introduction, About* — nothing else is banned by name. "Get started with X" is **not** banned: it starts with a verb, isn't a gerund, isn't on that list. Don't flag it.
- Structure: prerequisites stated in-line or as the opening context (not necessarily a separate heading — that's a Unify/Diataxis convention, not this profile's), numbered steps, verification.

**Concept** (explanation-oriented, "what is X," "why X matters"):
- Triggers: explains ideas, architecture, recommendations; nouns like "architecture," "security," "credentials"; no steps, just explanatory content.
- Title: noun-first.
- Structure: opening paragraph (what it is, why it matters), aspect sections, cross-references to related procedures.

**Reference** (data-oriented, lookup tables, API/parameter docs):
- Triggers: structured data, lists, specifications; tables, definitions, parameters; the goal is to look something up.
- Title: descriptive, not generic.
- Structure: brief description, then tables or definition lists, minimal prose.

**Landing** (navigation-oriented, index of child pages):
- Triggers: a list of related topics or sub-pages; the goal is navigation.
- Structure: overview paragraph, grouped links to child pages.

**Decide and move on.** State the decision and reasoning in the PR description (`skills/draft-docs/pr-and-jira-output.md`), the same as Unify's profile — don't pause for confirmation, and only raise it as a gap-list question if the content genuinely supports two readings that would produce materially different pages.

## What this profile is not: mixing Concept and Procedure on one page is correct, not a defect

BeeWrite's `best-practices.adoc` has a section called "Restate the problem or process," written for BeeWrite as a whole, before Unify ever layered Diataxis on top of it: *"Before providing a technical procedure, restate the problem (kbase) or process (docs), and then give a brief explanation of how it is going to be solved... before the exact steps."* This is the documented house convention for this profile — concept-before-procedure framing within a single page is expected, not a type-mixing violation. Several of the real CI examples curated for this profile (see `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md`) do exactly this and are correctly flagged as clean, not caveated. **Never apply "never mix types, split into separate files" here** — that is Unify's own `CLAUDE.md` rule, written for its Diataxis adoption, and was never CI/CDRO's rule.

## Step 3: classify gaps — feeds `shared/gap-list.md`

Same three-tier classification as Unify's profile (critical / important / nice-to-have) — see `skills/draft-docs/profiles/unify-diataxis/analyse.md` step 4 for the definitions, unchanged here. Pass straight through to the gap list once drafting and self-check are done.

## Step 4: amendments to existing docs

If this changes a published page: identify which sections, what preserves, what a human needs to re-verify (cross-references, examples). Carry anything genuinely uncertain into the gap list.

## A standing, standard-independent rule regardless of page type: cross-references must resolve to a real anchor

This is the most common defect in these repos: pages that use the full heading text as the cross-reference fragment (for example, `xref:page.adoc#Creating_a_rule[]` where the target page's real anchor, auto-generated or explicit, doesn't match that string). This has nothing to do with which anchor *syntax* is used — `[#id]`, `[id=id]`, and `[[id]]` are all valid AsciiDoc, and `[[id]]` should not be flagged as wrong (see `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md`'s note on this). It's about whether the fragment after `#` actually matches an anchor that exists in the target. **Before emitting any cross-reference to a specific section (not just the page), confirm the anchor exists in the target file** — don't assume a heading's visible text is also its ID.

## Output of this stage

A short internal record of: the chosen page type, the light outline, and the classified gap list — feeding into the matching `generate-*.md` and then `skills/review-docs/SKILL.md`. No stop here, no "approve this outline" step.

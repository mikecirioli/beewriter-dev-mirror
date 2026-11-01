# CI/CDRO legacy: generate a Concept page

*Runs as one unattended pass, like `skills/draft-docs/profiles/ci-cdro-legacy/generate-procedure.md`.*

## What a Concept page is

Explanation-oriented: "what is X," "why X matters," architecture, recommendations. No steps — if the content starts accumulating a numbered sequence of actions, that's a sign some of it belongs in a Procedure page instead, cross-linked rather than merged in.

## Page title

Noun-first: `Security recommendations`, `Pipeline architecture`, `Credentials and user impersonation` (a real example from this set, see `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md`). Same banned-word list as Procedure pages: *Use, Work with, Overview, Introduction, About.*

## Structure

- Opening paragraph: what it is, why it matters.
- Aspect sections with explanatory content.
- Illustrative examples where they genuinely help (a clean real example in this set uses an ASCII hierarchy diagram for this purpose).
- Related information: cross-references to related procedures and concepts.

## Style

Prose-heavy. Cross-references to related Procedure pages are expected and normal — a Concept page pointing a reader toward the Procedure page that acts on what it just explained is the standard pattern, not a boundary violation.

## Anchors, product attributes, terminology

Same rules as `skills/draft-docs/profiles/ci-cdro-legacy/generate-procedure.md` — shared BeeWrite layer, not page-type-specific.

## Examples

Read `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md` before drafting.

## Before handing off to self-check

Quick self-scan: no numbered action sequence masquerading as "concept," cross-references checked against real anchors, no gerund-form or banned-word title.

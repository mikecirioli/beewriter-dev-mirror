# CI/CDRO legacy: generate a Reference page

*Runs as one unattended pass, like `skills/draft-docs/profiles/ci-cdro-legacy/generate-procedure.md`.*

## What a Reference page is

Data-oriented: lookup tables, parameter lists, API specifications. The goal is to look something up quickly, not to read linearly.

## Page title

Descriptive, not generic — never bare "Reference."

## Structure

- Brief description up top.
- Tables for multi-column data; definition lists for parameter-description pairs.
- Section groupings for related items.
- Minimal prose — this page type is "boring by design" (the same framing already used for Unify's reference examples applies here unchanged).

## The one failure mode to actively guard against

`skills/review-docs/SKILL.md`'s "don't invent syntax or parameters by analogy to a similar system" rule applies with full force here, and reference pages are where it's most likely to bite: a plugin name, a parameter, or a CLI flag that doesn't exist anywhere in the ticket, its linked PR, or the actual product repo must go in the gap list or get a `// DOCS WRITER VERIFY:` comment — never filled in from what a similarly-named CI or CD/RO feature, or an adjacent tool, would plausibly have.

## Anchors, product attributes, terminology

Same rules as `skills/draft-docs/profiles/ci-cdro-legacy/generate-procedure.md`.

## Examples

Both repos have a Reference example; see `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md`. For CI, read `secure/pages/cjoc-permissions.adoc` first (the tightest model, pure definition list, zero cross-references); `mcp-router/pages/mcp-tool-reference.adoc` is a secondary, more narrative option. For CD/RO, read `install-trad/pages/remote-agent-permissions.adoc`. Do not read `properties/pages/intrinsic-properties.adoc` as a model even though it's structurally the strongest Reference page in either repo — it has a systematic broken-cross-reference defect (self-referencing fragments that don't resolve) so don't imitate it.

## Before handing off to self-check

Quick self-scan: every parameter, flag, and syntax element traced to a real source, no analogy-filled gaps, tables used for genuinely tabular data rather than prose forced into a table.

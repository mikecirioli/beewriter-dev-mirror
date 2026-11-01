# CI/CDRO legacy: generate a Procedure page

*Runs as one unattended pass: outline, draft and validate without stopping for approval. See `skills/draft-docs/profiles/ci-cdro-legacy/analyse.md`.*

## What a Procedure page is

Action-oriented: "how to do X." Not Diataxis's "how-to" category by name, but the same practical shape — a reader who wants to accomplish a specific task, not learn a concept.

## Page title

Verb-first, not a gerund: `Configure X`, `Install X`, `Troubleshoot X`, `Deploy X`. The real banned-word list (`style.adoc`) is short: *Use, Work with, Overview, Introduction, About* — nothing else is banned. Don't invent additional exemptions or additional bans by analogy to Unify's Diataxis title rules (`skills/draft-docs/profiles/ci-cdro-legacy/analyse.md`'s "what this profile is not" section).

## Structure

- **Prerequisites**: bullet list with specifics. Unlike Unify's how-to convention, this profile doesn't require folding prerequisites into the opening paragraph — a dedicated Prerequisites section is normal and already used across the real example set (see `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md`).
- **Opening/concept framing (recommended, not optional)**: restate the problem or process being solved before the steps, per `best-practices.adoc`'s "Restate the problem or process" section. This can be a short paragraph or an "About X" subsection ahead of the numbered steps — it is not a type-mixing violation in this profile.
- **Action section(s)** with verb-phrase titles.
- **Verification**, where the real content supports one — don't invent a verification step that isn't grounded in the ticket or a comparable page.

## Steps

- Numbered list, imperative verbs (Navigate, Select, Enter, Configure).
- Declare the language on every code block (`[source,groovy]`, `[source,yaml]`, `[source,bash]`).
- Mark anything uncertain with `// DOCS WRITER VERIFY:` rather than inventing a plausible value — `skills/review-docs/SKILL.md` decides whether that stays a comment or becomes a gap-list question.
- Mark uncertain cross-references with `// DOCS WRITER VERIFY: xref target exists` — and separately, per `skills/draft-docs/profiles/ci-cdro-legacy/analyse.md`'s standing rule, confirm any *section* cross-reference's fragment actually matches a real anchor in the target before emitting it, not just that the target page exists.

## Anchors

Generate an anchor immediately above every subheading. Any of the three real, valid forms is acceptable — `[#id]`, `[id=id]`, or `[[id]]` — but prefer `[#kebab-case-id]` for new content: it's the form `links.adoc` itself uses throughout and recommends for consistency. **Do not flag existing `[[id]]`-style anchors in a page being amended as wrong or in need of replacement** — that's a real but INFO-level preference, not a standards violation (confirmed directly against the `cloudbees-docs` plugin's own review severity rules, which explicitly say not to flag `[[id]]` as old-style or incorrect).

## Product attributes and terminology

Same as Unify's profile: product attributes in prose, full names in code blocks, banned/preferred terms from `word-usage.adoc` applied exactly. This part of BeeWrite is shared across every profile, not Diataxis-specific.

## Related pages

End with a "Related pages" section where the real content supports genuine cross-links — not a padding section if there's nothing real to link to.

## Examples

Read `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md` before drafting. Several of the real CI examples open with a short concept-framing paragraph or subsection before their steps — read that pattern as the expected shape for this profile, not as something to strip out.

## Before handing off to self-check

Quick self-scan: goal and context stated before the steps (even briefly), imperative mood throughout, no heading without introductory text, code blocks declare a language, cross-reference fragments checked against real anchors. `skills/review-docs/SKILL.md` runs the fuller pass regardless.

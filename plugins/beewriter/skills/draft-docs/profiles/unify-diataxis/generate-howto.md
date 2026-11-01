# Unify/Diataxis: generate a how-to guide

*Write the outline as an internal working step, not a deliverable: don't stop for approval between outlining and drafting.*

## What a how-to guide is

Task-oriented, for users already competent and at work, not at study. One goal per guide. No teaching, no reference-grade completeness — link out to explanation and reference pages instead of absorbing their content.

- ✅ "How to configure a pipeline to trigger on pull requests"
- ❌ "How to use the settings menu" (tool-focused, not task-focused)

A how-to is a recipe: assumes the reader can cook, gives only the steps for this result.

## Build the outline (internal step, not a checkpoint)

From `skills/draft-docs/profiles/unify-diataxis/analyse.md`'s output:

1. Opening context (1–3 sentences: what this accomplishes, why, the end result). Note prerequisites that need an admonition.
2. Main procedure sections (2–5 typical), each a cohesive sub-task, titled with a verb phrase.
3. Within each section: numbered steps, decision points, expected outcomes, code examples, admonitions where a specific requirement arises.
4. Troubleshooting, if there are genuinely common issues — not a padding section.

Use this outline to generate directly. It does not get presented for approval.

## Page attribute: `:diataxis-type: how-to`

Set this near the top of the file, after the `abbr.adoc` include and before the title — the existing convention in real Unify pages. `skills/review-docs/SKILL.md` cross-checks it against the actual type decision before output.

## Page title

Verb phrase, specific about the outcome, no "How to" prefix (redundant with the how-to-guides folder):

- ✅ "Configure SAST rules" / "Manage scan findings" / "Set up multifactor authentication"
- ❌ "SAST configuration" (not a verb phrase) / "How to configure SAST rules" (redundant)

## Opening

- One or two sentences: what this does, the benefit.
- Prerequisites: for one or two, put them in the intro ("Before you begin, ensure you have…") or an `IMPORTANT` admonition; a section with one or two bullets looks thin. For three or more, or prerequisites that each need a link or explanation, a `== Prerequisites` section is fine (BeeWrite's `best-practices.adoc`). When reviewing, treat either as acceptable, not a must fix.
- `{PRODUCT}` attribute, never a hardcoded product name.
- Never start with "This guide explains/shows..." — start with the action verb.

```
= Manage organizations

Create, access, and manage xref:platform-administration:explanation/understanding-organizations.adoc[organizations and sub-organizations] to build hierarchical structures that align with your organizational needs.

NOTE: You need administrative permissions in your organization to manage organizational structure. For permission details, refer to xref:platform-administration:reference/rbac-permissions-reference.adoc[RBAC permissions reference].
```

## Headings: every heading needs explanatory text immediately after it

No heading is ever immediately followed by another heading or by steps with no introduction — this is a BeeWrite house rule, and it's strict:

```
=== Configure SAML authentication

This procedure connects your organization to a SAML identity provider for single sign-on access.

. Navigate to menu:Organization[Security settings].
```

not:

```
=== Configure SAML authentication     ← missing explanation
. Navigate to menu:Organization[Security settings].   ← jumps straight to steps
```

Use the "To [verb phrase]:" pattern when steps are self-explanatory and need no extra context; use a context sentence first when they don't.

## Step style

- Imperative mood: "Navigate to," "Select," never "You should" or "The user."
- Specific, not abstract: "Select your organization from the organization selector in the upper left," not "Navigate to your target organization context."
- Bold actual UI element text only: `Select *Save*`, not `Select the *Save* button`.
- Named roles/permissions bolded: `Assign the *Admin* role`, not "grant admin access."
- No vague alternatives ("or similar option," "the appropriate button") and no "etc." — name the actual options.
- List items over three words end with a period; short fragments don't.
- Include expected outcomes after key steps, and show example values/placeholders explicitly (`<controller-name>`), with the placeholder's meaning stated.

## Admonitions

`NOTE` for helpful extra information, `TIP` for best practice, `IMPORTANT` for something the user must not miss, `WARNING` for serious consequences, `CAUTION` for minor ones. Match the severity to the content — don't default to `NOTE` for everything.

## Code and configuration

Declare the language on every block (`[source,groovy]`, `[source,yaml]`, `[source,bash]`). Show expected output where it helps confirm success. Mark anything you can't confirm with `// DOCS WRITER VERIFY:` (`skills/review-docs/SKILL.md` decides whether that stays a comment or becomes a gap-list question) rather than inventing a plausible value.

## Related pages (required, every time)

End every how-to with a "Related pages" section: the companion explanation page, relevant reference pages, and genuine prerequisite/next-step how-tos — not every tangentially related guide.

```
== Related pages

* xref:explanation/pipelines.adoc[Understanding pipelines]
* xref:reference/pipeline-syntax.adoc[Pipeline syntax reference]
```

## Navigation

After generating, add the page to the module's `partials/nav.adoc`, how-to guides placed third within its sub-area (after explanation and tutorial pages, before reference), using empty-bracket xrefs when the nav text matches the title exactly.

## Examples

Read `skills/draft-docs/profiles/unify-diataxis/examples/README.md` before drafting. It lists live Unify pages to read directly. One of them (`configure-saml-single-sign-on.adoc`) carries a known minor caveat, noted in the manifest; read it anyway, just don't copy that specific call.

## Before handing off to self-check

Quick self-scan against: goal stated up front, logical step order, no heading without introductory text, no "click"/"go to"/"you'll see" (use select / navigate to / displays), Oxford commas, American English, one sentence per line. `skills/review-docs/SKILL.md` runs the fuller pass regardless — this is just not leaving the obvious stuff for it to catch.

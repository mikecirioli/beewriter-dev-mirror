# Unify/Diataxis: generate a reference page

*Write the outline as an internal working step, not a deliverable: don't stop for approval between outlining and drafting.*

## What reference is

Information-oriented, consulted during work, not read during study. "Boring by design" — if it's engaging or narrative, it's drifted into explanation; if it includes tasks and goals, it's drifted into a how-to.

| vs. | Reference is | The other type is |
|---|---|---|
| Explanation | Neutral, factual, for lookup during work | Discursive, contextual, for study |
| How-to | Describes the machinery, structure mirrors the product | Shows how to achieve a goal, structure mirrors the task |
| Tutorial | Describes all options, for looking up facts | Teaches one approach, for learning by doing |

## Build the outline (internal step, not a checkpoint)

1. Document structure: sections and subsections.
2. Content inventory per section (what's covered, briefly).
3. Organisation approach — alphabetical, by category, by hierarchy — pick whichever matches how the machinery is actually structured, not an arbitrary default.
4. Format patterns: table, definition list, or code block, chosen per the formatting principle below.
5. A completeness check: does this cover every option/field/permission that exists, not just the ones the ticket happened to mention?

Generate directly from this.

## Page attribute: `:diataxis-type: reference`

Set this near the top of the file, after the `abbr.adoc` include and before the title — confirmed in real Unify pages (e.g. `release-management-reference.adoc`). `skills/review-docs/SKILL.md` cross-checks it against the actual type decision before output.

## Page title

**Noun + "reference"**:

- ✅ "Pipeline syntax reference" / "User permissions reference" / "SAST scanner configuration reference"
- ❌ "Pipeline syntax" (doesn't signal type) / "Reference for pipeline syntax" (awkward) / "Pipeline syntax guide" (sounds like a how-to)

## Opening

Brief and factual — state what's being specified, not "this page specifies...":

```
= RBAC permissions reference

RBAC permissions in {PRODUCT} are organized into categories that define user and team access across applications, environments, and organizational resources.
Use this reference when configuring security settings, troubleshooting permission issues, or creating custom roles.
```

not: `❌ "This page specifies all RBAC permissions available in {PRODUCT}..."`

## Headings need explanatory text immediately after them — same hard rule as every other type

No heading followed straight by a table or code block with no framing sentence; no heading followed straight by a sub-heading with nothing said about the parent section first.

## Formatting: the simplest structure that serves the content

- **Unordered list** for simple term/definition pairs.
- **Definition list** (`term:::`) for more detailed specifications — name, one-sentence description, then factual details (default, valid range, requires/implies).
- **Table** only for genuinely multi-attribute comparisons (`[cols="2,1,3"] |=== |Name |Type |Description`).
- **Nested lists** for hierarchy (permission trees, category/subcategory structures).

Don't default to a table because it looks thorough — a flat list is often clearer for simple pairs.

```
executors:::
Number of concurrent builds the agent can run.
Type: Integer.
Valid range: 1-100.
Default: 2.
```

## Always specify, where they exist

Default value, valid range or constraint, required vs. optional, type, and relationships (`Requires:`, `Implies:`, `Required for:`). An entry missing these where the product actually has them is incomplete, not just terse.

## Examples: minimal, correct usage only

Reference can show a short usage example, but never explains *why* or *when* to choose one option over another — that's explanation's job, not this file's:

```
agent label:::
Run on agent matching specified label.
+
[source,groovy]
----
agent {
    label 'linux'
}
----
```

## Admonitions: rarely

Reference is neutral. `IMPORTANT`/`WARNING` only for a critical, factual consequence of misuse — most reference content needs none at all.

## Related pages (required, every time)

```
== Related pages

* xref:explanation/rbac-architecture.adoc[Understanding RBAC in CloudBees CI]
* xref:howto/configure-rbac.adoc[Configure role-based access control]
```

Link to how-tos that use these specs, explanation for conceptual background, related reference pages consulted together, and tutorials that teach the specs hands-on.

## Navigation

Reference pages go **last** in their sub-area's nav (after explanation, tutorial, how-to).

## Examples

Read `skills/draft-docs/profiles/unify-diataxis/examples/README.md` before drafting. It lists live Unify pages to read directly.

## Don't borrow syntax from a similar-looking adjacent system

Confirmed, real incident (see `skills/review-docs/SKILL.md`): Unify's workflow syntax resembles GitHub Actions closely enough that a prior pass used `github.*` context variables where the product actually uses `cloudbees.*`, among other invented parameters. Reference content is where this bites hardest, because it's exactly the content a reader trusts as authoritative. Every syntax element, parameter name, and context variable must trace to the ticket, its linked PR, or the actual product repo — not to "what the equivalent would be called in a similar tool."

## Before handing off to self-check

Quick self-scan: is every option/field/permission the ticket and product repo surfaced actually documented, with default/type/range where applicable? Is the tone neutral throughout — no opinion, no "why," no step-by-step creeping in? `skills/review-docs/SKILL.md` runs the fuller pass regardless. **A missing specification is exactly the kind of thing that belongs in the gap list** (`shared/gap-list.md`) if the product repo and ticket didn't make it findable — don't silently omit an option you couldn't confirm.

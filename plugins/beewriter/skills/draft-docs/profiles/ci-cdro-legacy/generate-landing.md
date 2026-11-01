# CI/CDRO legacy: generate a Landing page

*CI and CD/RO currently use two different landing-page shapes. CD/RO's landing pages are moving to CI's shape, so a new landing page in either repo uses CI's shape. Both are documented below: the first is what every new page should look like, and the second is what you'll find when reading or amending an existing CD/RO page.*

## What a Landing page is

Navigation-oriented: an index of child pages, not content in itself. Used sparingly — most tickets in this profile will resolve to a Procedure, Concept, or Reference page, not a new Landing page.

## The target shape for any new Landing page, CI or CD/RO: the `section-landing-page` renderer

**Generate this shape for every new landing page, in both repos.** It's CI's repo-wide mechanism and the one CD/RO is moving to. It isn't a style preference: a new page in the older plain-xref shape (below) would be out of step with where CD/RO is heading.

- **File naming**: `intro.adoc`, not `index.adoc`.
- **Header is different from every other page type in this profile**: starts directly with `:renderer: section-landing-page`, then `:summary:`, then the `= Title`. **No `include::ROOT:partial$abbr.adoc[]` line at all** — don't add one; the real example doesn't have it, and `skills/review-docs/SKILL.md`'s usual "line 1 must be the abbr include" expectation does not apply to this page type.
- **The `:summary:` line must use hardcoded product names, never attributes.** Per `docsite-usage/docs/modules/contribution/pages/summary.adoc`: on pages using `:renderer: section-landing-page` (this page type, exactly), attributes don't resolve inside `:summary:` when it's displayed in search results — `{PRODUCT}` would render as the literal string `{PRODUCT}`, not the product name. This is the opposite of every other page type in this profile, where `:summary:` always uses attributes. Don't apply the general rule here by habit.
- **Body**: almost entirely a `[source,yaml,role="renderer",subs=attributes+]` literal block (`....` delimiters, not `----`), containing:
  - `title`, `description` (top-level, site-rendered)
  - `quickLinks:` — a short list of `title`/`url` pairs, the few most important entry points
  - `pageType: product-landing-page`
  - `cards:` — the real navigation content, a list of `heading`/`description`/`url` triples, one per child page
- **URLs are site-rendered paths** (`"/docs/cloudbees-ci/latest/pipelines/creating-pipeline"`), not Antora `xref:` syntax. For a CD/RO page, mirror the same path shape under the CD/RO docs root (`/docs/cloudbees-cd/latest/...`) — confirm each `url:` path corresponds to a real page's rendered path (module + page name) in the repo. This can't be exhaustively verified without the live rendered site; mark any URL you can't trace to a real source file with `// DOCS WRITER VERIFY:`.
- Use `{PRODUCT}`-style attributes inside the YAML values exactly as prose would (the real CI example does: `{PRODUCT} Pipeline guide`, `{CPS}`, `{CTRL}`) — the `subs=attributes+` on the block is what makes that resolve.

**Example**: `docs/modules/pipelines/pages/intro.adoc` (CI). Read it whichever repo the ticket is in. See `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md`.

## CD/RO's current, pre-migration shape — for reading/amending existing pages, not for drafting new ones

This is what you'll find if a ticket touches an *existing* CD/RO landing page (for example, `dashboards-built-in/pages/index.adoc`, see `skills/draft-docs/profiles/ci-cdro-legacy/examples/README.md`) — plain overview paragraph, an admonition where there's a real precondition, then a flat bullet list of `xref:child-page.adoc[]` entries (empty brackets). Recognize it so you don't flag it as some other page type by mistake, and don't strip it out unprompted if a ticket only asks for a small amendment — but if a ticket is building a *new* CD/RO landing page, or an amendment substantial enough that the writer would reasonably expect it, use the renderer shape above instead, and say so plainly in the PR description, citing [DOCS-12447](https://cloudbees.atlassian.net/browse/DOCS-12447) (this page intentionally doesn't match its siblings yet, because the siblings haven't been migrated, tracked there).

## Style (both shapes)

Minimal content, navigation-focused either way. Mark every child-page link with a gap-list note or `// DOCS WRITER VERIFY:` if the target's existence or exact path isn't confirmed against the real repo — don't assume a plausible-sounding page exists.

## Before handing off to self-check

Every `url:` in `cards:`/`quickLinks:` traced to a real page, YAML well-formed inside the `....` block, no stray `include::ROOT:partial$abbr.adoc[]` added. If amending an existing CD/RO page in its current plain-xref shape rather than migrating it, every linked child page confirmed to exist in the real repo.

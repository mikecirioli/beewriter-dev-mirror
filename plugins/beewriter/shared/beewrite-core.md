# BeeWrite — interim pointer

**This file is a placeholder, not a true per-profile standards split.** The ideal design loads a `core` layer plus a Diataxis profile layer plus a legacy profile layer, so each profile loads only what it needs. That split hasn't happened yet; a future, token-cheaper version of this skill should build it.

**Until that split exists, both profiles read BeeWrite directly and in full, plus a second real source:**

- Source: `cloudbees-beewrite-standards/` inside `docsite-usage`. Get a current copy first (`shared/freshness-check.md` section 2). Don't assume the cache is current without checking.
- **Also read, every run, from `docs/modules/contribution/pages/`** (also in `docsite-usage`): `document-headers.adoc`, `attributes.adoc`, `summary.adoc`, `page-categories.adoc`, `partials.adoc`. These are authoritative standards outside `cloudbees-beewrite-standards/`. For example, `document-headers.adoc` explains that a blank line before the page title silently breaks document-header processing. `page-categories.adoc`'s list is a closed vocabulary (additions need a named owner's approval), so treat it as the full list, not examples.
- **The rest of that same directory is situational, not always-load**: `redirects.adoc` (renaming/moving/deleting a page), `internal-only.adoc`/`gated-content.adoc` (prerelease or gated content), `conditional-text.adoc`, `cross-links.adoc`, `versions.adoc`, `noindex.adoc`, `lexicon.adoc`, `next-builds.adoc`. Know these exist; read the specific one only when a ticket's content actually calls for it.
- **`cloudbees-docs-plugin.adoc` in that directory documents an older plugin** (`cloudbees-docs`), not this one. Don't treat it as guidance for this skill, and don't edit it as part of a drafting run.
- This costs more tokens per run than a properly split design would, which is expected and acceptable for now, but should be revisited once that split exists — don't let this interim become permanent by default.

**Explanation-page titles in Unify:** BeeWrite's `style.adoc` lists "About security recommendations" as a wrong title in general, but makes an explicit exception for Diataxis-profiled (Unify) explanation pages, which use "About X" or "Understanding X". The exception applies only to explanation pages. The Unify profile's generation files follow it.

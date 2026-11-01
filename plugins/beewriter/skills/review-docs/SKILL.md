---
name: review-docs
description: Review CloudBees documentation against BeeWrite standards and the page-type rules, report what to fix, and fix it on request. Use when the user asks to review, check, proofread, audit, or fix a docs page, a set of pages, or a docs PR, or asks what to ask an SME about a draft. Also run on your own draft as the self-check step of draft-docs.
---

# Review docs

File paths in this skill are relative to the BeeWriter plugin root, two folders up from this file.

## Two ways this runs

- **Self-check, inside `skills/draft-docs/SKILL.md`** (pipeline step 7): you're checking your own fresh draft. Fix what you can directly, mark the rest (see "On finding something"), commit, then hand over to the gap list.
- **On request**: someone asks you to review a page, a folder or a PR. Report first; change files only if asked to fix. Steps:
  1. **Find the profile** from the repo, as `skills/draft-docs/SKILL.md` describes. Unify uses the `unify-diataxis` rules; CI and CD/RO use `ci-cdro-legacy`. Outside those repos, say so and review against BeeWrite alone.
  2. **Get current standards** (`shared/freshness-check.md` section 2) and read `shared/beewrite-core.md`.
  3. **Work out each page's type** from its content and attributes, using the profile's `analyse.md`, then apply that type's `generate-*.md` checklist plus every check below.
  4. **Report** findings grouped as **must fix** (wrong, broken, or a build or standards error), **should fix** (a BeeWrite rule a reviewer would flag) and **consider** (style judgement). Give the file and line, the rule, and the suggested change. Keep it short: skip anything you'd fix silently in self-check mode and list those as one line ("12 minor style fixes, apply them?").
  5. **Questions for an SME:** if a fact can't be confirmed from the page, ticket, linked PRs or product repo, list it as a question using `shared/gap-list.md`'s rules for writing questions.
  6. **Fixing:** when asked to fix, apply the agreed changes, leave a `// DOCS WRITER VERIFY:` comment where a fix needs information you don't have, and summarize what changed. On a PR branch, commit to that branch; never merge.

## Check against

- The profile's own generation file or files: the quality checklist in each (content quality, structure, style guide compliance, technical accuracy).
- `shared/beewrite-core.md`, plus the profile's own standards layer.
- Page-type separation: Diataxis types (Unify profile) or procedure, concept and reference (CI/CDRO profile). Did the draft stay one type, or drift, for example by mixing explanation into a how-to?

## On finding something

- **Fixable without more information** (a passive sentence, a missing Oxford comma, a gerund heading that should be a verb phrase): fix it directly. Don't gap-list style issues that don't need an SME.
- **Not fixable without more information** (an uncertain UI label, an unconfirmed field name): if it isn't worth an SME's time, leave a `// DOCS WRITER VERIFY:` comment in the content. If it is, carry it forward to `shared/gap-list.md`. A gap-list question is something a person needs to answer, and goes to the SME as an inline PR review comment. `DOCS WRITER VERIFY` is for the writer, never the SME.

### `// DOCS WRITER VERIFY:` stays in the source

The name makes it clear the marker is for the writer, so an SME reviewing the PR can skip it. Keep it as a source comment only; don't post it as an inline PR comment. Posting it would put it in front of whoever reviews first, often the SME, which is the noise the marker exists to avoid. The writer who started the run sees these comments in the diff.

## Never claim verification that didn't happen

Reviewers notice, and rightly challenge, a PR that reads as if someone reproduced a failure or tested a fix by hand when an agent drafted it. That's a different problem from an unflagged factual gap (`shared/gap-list.md` covers those): it's the PR's own narrative implying first-hand testing that never happened.

Re-read the PR description (if there is one) and the content for phrasing like "this fails because...", "verified that..." or "tested and confirmed...". Wherever it reads as hands-on verification, check whether that happened in this run. If it didn't, rewrite it to say what *was* checked (the ticket, the linked PR, the product repo, a comparable existing page), and that the run didn't include testing against the live product. A PR can have no gap-list questions and still fail this check if its tone overclaims.

## Check the `:diataxis-type:` attribute matches the decision

Unify pages carry a `:diataxis-type:` attribute (`how-to`, `explanation`, `reference`, `tutorial`) near the top of the file, after the `abbr.adoc` include and before the title. Every Unify generator sets it on new pages. Check it here: does it match the page's actual type (in self-check mode, what the profile's `analyse.md` decided)? A mismatch (a how-to tagged `:diataxis-type: reference`, say) is a contradiction to fix before output. It's cheap and deterministic, so don't skip it.

## Don't invent syntax or parameters by analogy to a similar system

Earlier Unify Workflows reference content shipped with invented API parameters, unsourced version requirements, a misclassified scanner type, and GitHub Actions' `github.*` context variables where the product uses `cloudbees.*`. That last one is the failure to watch for: CloudBees Unify workflow syntax looks enough like GitHub Actions that pattern-matching from GitHub Actions documentation produces plausible, wrong syntax.

**If a syntax element, parameter or context variable isn't confirmed in the ticket, its linked PR or the product repo, it goes in the gap list or gets a `// DOCS WRITER VERIFY:` comment. Never fill it in from what a similar system would use.** This matters most for reference pages, but applies everywhere.

Pages in the Unify Workflows area may still contain errors of this kind. Treat them with caution when you use them as comparable pages.

**Checking a generic upstream system's public documentation isn't the same as confirming this product's convention.** For example, Docker's own Kubernetes-driver example gives a canonical BuildKit builder name, and CloudBees' internal convention differs from it. An external check answers "is this plausible?", not "is this what we do here?". Treat it like a guess from an adjacent system: it can inform a `// DOCS WRITER VERIFY:` note, but it doesn't justify stating the value as fact unless something in this repo confirms it too.

## Check the authoritative source before deciding a question needs a person

Before treating an API-behavior or content question as needing SME or writer input, **check whether a public, authoritative source already answers it**: a live API spec, a confirmed page elsewhere in the repo, documented product behavior. This is the other half of "don't invent by analogy": that rule says don't guess when you can't check, and this one says check by default, without waiting to be asked.

Fetch the raw document directly, not through a summarizing step, when exact field names or values matter; a paraphrase can smooth over the one detail you needed. If the source clearly answers the question, act on it and say so. Only if the source is silent or ambiguous does it become a gap-list item.

## Don't overuse colons in place of em dashes

Banning em dashes doesn't remove the habit behind them; it shifts it to whatever punctuation is still allowed, usually colons. Overused colons give the same monotonous, clause-stacking feel the em-dash rule is meant to fix.

**This isn't "avoid colons."** A colon introducing a list, a clarification or a definition is correct, and BeeWrite's em-dash rule names colons as a valid alternative. Watch the frequency: if several sentences in a row each join two clauses with a colon, vary them. Use a separate sentence, a different connector, or two independent sentences.

## In self-check mode, finish completely before the gap list runs

As `shared/gap-list.md` requires, don't start generating gap-list comments while self-check is still editing content. Finish, commit, then move on.

---
name: draft-docs
description: Draft CloudBees documentation from a Jira ticket, unattended, finishing in a draft PR with a batched gap list of open questions. Use when the user gives a Jira ticket key and asks to draft, write, or generate the documentation for it, in a CloudBees docsite repo (Unify, CI, or CD/RO).
---

# Draft docs from a Jira ticket

**Plugin version:** 0.1.0

File paths in this skill are relative to the BeeWriter plugin root, two folders up from this file.

## Overview

Drafts a page, or a small set of pages, from a Jira ticket in one unattended pass: no approval steps along the way. The draft PR and its gap list are where the writer reviews the result.

It picks a profile from the repo it's running in:

| Repo | Profile |
|---|---|
| `docsite-cloudbees-unify` (Unify) | `skills/draft-docs/profiles/unify-diataxis/` |
| `docsite-cloudbees-ci`, `docsite-cloudbees-cd` (CI, CD/RO) | `skills/draft-docs/profiles/ci-cdro-legacy/` |
| Anything else | Stop and say so. Don't guess a profile for a repo this skill isn't set up for. |

## Prerequisites

- **VPN** (Tailscale), connected.
- **GitHub and Jira access.** Every action (reading, committing, opening the PR, posting comments) happens as the person or identity running the skill. `docsite-cloudbees-cd` and `docsite-cloudbees-common` are private repos, so the CI/CDRO profile needs read access to both.
- **Run it from inside the docs repo** the ticket's content belongs to. That's the repo the draft commits to and opens the PR against.

## Reference files

Standards come from two sources, kept current by `shared/freshness-check.md`. Read that file rather than duplicating it here.

| Alias | What it covers |
|---|---|
| BEEWRITE_CORE | `cloudbees-beewrite-standards/modules/ROOT/pages/`: core style, structure, and terminology, every run |
| BEEWRITE_SYNTAX | `cloudbees-beewrite-standards/modules/syntax/pages/`: AsciiDoc syntax conventions |
| CONTRIBUTION_CORE | `docs/modules/contribution/pages/{document-headers,attributes,summary,page-categories,partials}.adoc`: Antora structure, every run |
| CONTRIBUTION_SITUATIONAL | The rest of `docs/modules/contribution/pages/`. Read only the page a ticket's content calls for; see `shared/beewrite-core.md` |

## Pipeline

1. **Ingest:** read the ticket (`shared/jira-ingest.md`).
2. **Resolve the product repo:** `shared/repo-map-lookup.md`. An unresolved or candidate-only area is a note for step 8, not a silent guess.
3. **Get fresh copies:** `shared/freshness-check.md`, for the standards cache, the docs repo you're drafting into, and any product repos needed for context.
4. **Analyse and classify:** the profile's `analyse.md`. State the page-type decision and reasoning in the PR description; don't ask for confirmation.
5. **Decide whether a draft is possible at all.** If the ticket, linked PR and a comparable existing page don't add up to a page that would be more right than wrong, stop: post one Jira comment naming what's missing, open no PR, and end the run. This is different from step 8's cap: it means "nothing to draft", not "a draft with open questions".
6. **Draft:** the profile's `generate-*.md`, plus `shared/beewrite-core.md`, plus the profile's `examples/README.md`. Load only the standards layer the profile needs, not all of BeeWrite.
7. **Self-check:** apply `skills/review-docs/SKILL.md` to your own draft, in self-check mode (fix what you can directly, mark the rest). It must fully finish, and the content must be committed, before step 9. Comments anchored before then go stale as soon as the self-check edits anything.
8. **Build the gap list:** `shared/gap-list.md`.
9. **Output:** `skills/draft-docs/pr-and-jira-output.md`. Open the draft PR (description per `skills/pr-description/SKILL.md`), add preview links, post the gap list as one batched review, update the Jira ticket, and leave the PR as draft.

## Running it

Ask, for example "draft the docs for BEE-12345", or run `/beewriter:draft-docs BEE-12345`.

## Related skills

- **After the PR is open**, feedback is handled by `skills/respond-to-review/SKILL.md`.
- **Spin-off work** found while drafting gets its own ticket via `skills/jira-ticket/SKILL.md`.

## Not included

- **SME tagging.** Step 9 never requests a reviewer or @-mentions anyone. The writer is the PR author and is notified automatically.
- **Merging, or marking the PR ready for review.** Always the writer's decision.

## Keywords

cloudbees documentation, asciidoc, beewrite, draft docs, write docs, jira ticket, unify, cloudbees ci, cloudbees cd, cdro

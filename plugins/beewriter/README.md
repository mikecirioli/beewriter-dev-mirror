# BeeWriter Plugin for Claude Code

Drafts, reviews and researches CloudBees documentation to BeeWrite standards. Its main skill drafts docs from a Jira ticket, unattended, and opens a draft PR with a single list of open questions for the writer.

## Purpose

Given a Jira ticket, BeeWriter reads the ticket and any linked PRs, finds the right product repo for context, drafts the page (or small set of pages) to BeeWrite standards, checks its own work, and opens a **draft** PR. It runs straight through with no approval steps along the way: the draft PR and its gap list are where the writer reviews the result.

A writer always decides when the PR is ready for review and when to merge it. BeeWriter never does either.

## Audience

- **Technical writers** drafting CloudBees Unify, CI, or CD/RO documentation who want a complete first draft to work from, rather than a blank page.

## Skills

Each skill has its own description, so you can just ask Claude in plain English. You don't need to name the skill or tell Claude where to look.

| Skill | Ask something like |
|---|---|
| `draft-docs` | "Draft the docs for BEE-12345." Or run `/beewriter:draft-docs BEE-12345`. |
| `review-docs` | "Review this page against BeeWrite." "Check the pages in this PR." "Fix the style issues." |
| `respond-to-review` | "Work through the review comments on PR #123." "What's still open on this PR?" |
| `jira-ticket` | "Write a Jira ticket for updating the SSO docs." |
| `pr-description` | "Write the PR description for these changes." |
| `research` | "What's the background to BEE-12345?" "Which repo holds the code for Feature Management?" |
| `standards` | "What does BeeWrite say about em dashes?" "Which attribute do I use for CloudBees CI?" |

Shared building blocks the skills use (standards caching, Jira reading, the product-to-repo map, the gap-list rules, GitHub API notes) live in `shared/`.

### Drafting: `/beewriter:draft-docs`

**Usage:** `/beewriter:draft-docs TICKET-KEY`, or ask "draft the docs for TICKET-KEY".

Run it from inside the docs repo the content belongs to. That's the repo it branches from and opens the PR against. It picks a drafting profile from the repo:

| Repo | Profile |
|---|---|
| `docsite-cloudbees-unify` | Unify (Diataxis page types: how-to, explanation, reference, tutorial) |
| `docsite-cloudbees-ci`, `docsite-cloudbees-cd` | CI and CD/RO (procedure, concept, reference, landing) |

In any other repo it stops and says so rather than guessing.

## What you get

- **A draft PR** titled `[TICKET-KEY] <summary>`, on a branch named for the ticket, with the new or changed pages.
- **A PR description** that states the page-type decision and why, lists the pages changed, and says plainly what was and wasn't checked.
- **A gap list**: one batched list of open questions the draft couldn't answer from the ticket, linked PRs or product code.
- **`// DOCS WRITER VERIFY:` comments** in the AsciiDoc source wherever a detail (a UI label, a field name, an xref target) couldn't be confirmed. Resolve or remove these before merging.

## Prerequisites

- **VPN** (Tailscale), connected.
- **`git`**, and the **GitHub CLI (`gh`)** signed in with your account.
- **Jira access** from Claude Code, through the Atlassian MCP server.
- **Read access to `docsite-cloudbees-cd` and `docsite-cloudbees-common`** if you draft CI or CD/RO content. Both are private repos, not readable org-wide by default. If you don't have access, the run stops and names the repo rather than guessing.

BeeWriter runs under your own GitHub and Jira credentials, so everything it does (branches, commits, PRs, comments) shows as you.

## Standards

BeeWriter drafts to two sources in `docsite-usage`:

- `cloudbees-beewrite-standards/`: style, structure, and terminology.
- `docs/modules/contribution/`: Antora structure (document headers, attributes, summaries, page categories, partials).

It also reads product attributes from `docsite-global`.

These are cached locally and refreshed automatically when they're more than 7 days old, so there's no separate update command. Product and docs repos it reads for context are shallow-cloned for the run and then discarded. See `shared/freshness-check.md`.

## Key principles

- **Unattended.** No approval steps mid-run. The draft PR and gap list are the review surface.
- **Standards first.** Follows BeeWrite, loading only the parts the active profile needs.
- **No invention.** Anything not confirmed from the ticket, a linked PR or the product repo goes in the gap list or a `// DOCS WRITER VERIFY:` comment, never filled in by analogy with a similar product.
- **No merging.** A writer always makes the call.

## Installation

```
/plugin install beewriter@cloudbees-marketplace
```

To try an unreleased version, use the dev marketplace described in the main [README](../../README.md#developer) and install `beewriter-dev`.

## Development

See the main [README](../../README.md) for plugin development guidelines. To change which live pages the drafting profiles learn from, edit the manifests in `skills/draft-docs/profiles/*/examples/README.md`.

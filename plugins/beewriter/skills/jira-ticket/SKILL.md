---
name: jira-ticket
description: Write and create a Jira ticket for CloudBees documentation work to the docs team's standard (plain opening sentence, background, scope, decisions, out of scope, open questions). Use when the user asks to create, write, raise, or draft a Jira ticket or issue for docs work, or to update an existing docs ticket's plan.
---

# Write a Jira ticket for docs work

*The shared standard for every profile: there's nothing profile-specific about how a ticket describes a problem. The one exception: if the ticket names a page type, use the vocabulary the target repo uses (Diataxis's tutorial, how-to, explanation and reference for Unify; procedure, concept, reference and landing for CI/CDRO), never the other profile's terms.*

## Who uses this skill

Anything that creates a docs ticket:
- The drafting skill, when drafting turns up separate or out-of-scope work that needs its own ticket.
- Any future intake agent that creates docs tickets.
- A writer asking Claude for a ticket, for example "write a ticket for updating the SSO docs".

Write to this standard every time, whoever is creating the ticket, so docs tickets read consistently.

## What a Jira ticket description is for

The plan and the reasoning behind it, for whoever picks this up — possibly the author, months later, with zero memory of the conversation that produced it. More abstract than a PR description: the problem being solved and how we intend to solve it, not the eventual diff. Jira can carry more detail than a PR description — there's more to say at this stage — but it's still not a design document. If a section runs past a few bullets, check whether it belongs here at all.

## Structure

No "TL;DR" or "Summary" heading. Jira already has a system field called Summary (the ticket title) — labeling a second thing "Summary" in the body invites exactly the confusion you'd expect ("update the summary" — which one?). Just start the description with the plain sentence, no signpost needed:

- **First line, unlabeled**: one sentence, two only if one genuinely can't carry it, covering what's being done and roughly how.
- **Background**: why this work is needed, two to four sentences.
- **Scope**: what will be created or changed. Name the pages or areas affected, as plain text — this is the abstract plan, not a page-by-page link list (that's the PR description's job, once the actual set of changed files exists).
- **Decisions**: each choice already made, with a one-line reason. Include the approach chosen over alternatives, so the reasoning survives until the work is picked up.
- **Out of scope**: only items a reader might reasonably assume are included.
- **Open questions**: unresolved decisions. Don't say who should answer them — the right person often isn't known in advance.

Omit any section that would be empty or padded. Don't write acceptance criteria, a definition of done, or a "done when" checklist — inventing one trains readers to skip the section, which is worse than not having it. If the user supplies acceptance criteria, include them exactly as given, don't expand or reword.

## Write from the perspective of the global system being changed, not a personal or local artifact

Jira is a shared, cross-team source of truth. A ticket describes what's changing about the shared thing, not the private way the need was found. For example, "update BeeWrite's rule on X", not "reconcile my style notes against BeeWrite": a personal working file isn't a counterparty to a company-wide standard. How you found the gap (comparing notes, a bug report, a conversation) is background at most, never the ticket's subject. If the work is "update X", say X is being updated and why, even if you found the need by looking at something only you have.

## Don't cite source material unless asked

Don't cite, link, or name the documents, related tickets, PDFs, Confluence pages, or session context the ticket was derived from. State the facts the reader needs directly, as facts. If a reference would genuinely help, ask rather than add it unprompted. (This is about *incidental* source material — a planning doc, a Slack thread, a prior ticket. It has nothing to do with the PR description's page-link requirement, which is about this ticket's own actual output, not its inputs.)

## Never include SME questions

A ticket description is a plan, not a Q&A log. Any question for an SME — whether it came up while drafting the ticket or afterward — goes in a comment, never folded into the description. This holds even after the ticket exists: a reviewer's question on the ticket is a comment, full stop.

## The description is frozen once created, with two narrow exceptions

**Don't amend a ticket's description after creation.** If the plan materially changes — the problem turns out to be different from what was first understood, or the intended solution changes — don't rewrite the description to match. Instead:

1. Post a comment with the real update: what changed, and why.
2. Add one short line to the *top* of the existing description: `NOTE: see [this comment](<link>) for an update to this plan.` — a pointer, not a rewrite.

This keeps the original plan intact as a record (useful context for understanding the project's actual history) while making sure nobody reads a stale description without noticing it's stale. Minor corrections (a typo, a broken link in the description itself) aren't a "material departure" and don't need this treatment — just fix them directly.

**The second exception: once a PR opens against this ticket, add one line to the top of the description: `PR: [#N](<link>)`.** Jira's GitHub integration already links the PR in the Development panel, but that sidebar is easy to miss. This edit is mechanical and tied to one event, the PR opening; it isn't a general licence to touch the description. Still post the Jira comment as well (`skills/draft-docs/pr-and-jira-output.md` section 5), because it carries the open-question count and this line doesn't.

## Writing guidance

- Write for someone who wasn't in the conversation, including the author months later. Avoid phrases that depend on current context ("as discussed," "the current plan," "this session").
- Prefer specifics over summaries: name the pages, features, and decisions.
- Don't invent details. If something is unknown, list it as an open question.
- American English, sentence case, no em dashes (same as everywhere else this skill writes prose).

## Output

Create the Jira ticket directly, with the Atlassian MCP tools or whatever equivalent you have. Unless the user says otherwise, create it in the project they name; if they don't name one, ask. Show the user the draft first when they're working with you interactively; when running as part of an unattended skill, create it directly.

## Before finishing

- The description opens with a plain, unlabeled sentence, not a "TL;DR"/"Summary" heading.
- No acceptance criteria, unless supplied word for word.
- No references to source material the user didn't ask for.
- No SME questions anywhere in the description.
- If this is an amendment to an existing ticket's plan: a comment was posted, and a one-line `NOTE:` pointer was added to the top of the description — nothing else in the description changed.
- If a PR just opened against this ticket: a `PR: [#N](<link>)` line was added to the top of the description, and the usual Jira comment was still posted too — nothing else in the description changed.

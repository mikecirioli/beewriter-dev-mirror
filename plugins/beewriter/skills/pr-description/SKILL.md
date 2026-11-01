---
name: pr-description
description: Write a pull request description for a CloudBees docs PR to the docs team's standard (Jira link, plain summary, ordered Pages Changed list with preview links, changes, departures, review checks). Use when the user asks to write, draft, or improve a PR description for docs changes, or to open a docs PR.
---

# Write a docs PR description

The shared standard for every profile. Nothing here is Unify- or CI/CDRO-specific, except that you name a page type using the term the target repo uses (as in `skills/jira-ticket/SKILL.md`).

## What a PR description is for

The reviewer, now: what changed, where, and what to check. Not a restatement of the ticket's background or reasoning. Don't repeat what the ticket says unless the work departed from it. Keep it short: the diff is the record, and the description tells a reviewer where to look and why.

## Structure

No "Summary" heading, consistent with the Jira standard. Just one or two plain sentences at the top.

- **First line: a link to the Jira ticket**, `Jira: [TICKET-KEY](<link>)`. The `[TICKET-KEY]` PR title links the PR in Jira's Development panel, but nothing links back to Jira from inside the PR, so this line does.
- **Second line, unlabeled:** what changed, in one or two sentences.
- **Pages changed:** see "Linking the pages" below. Required whenever the PR touches more than one page. Leave it out only for a single-page change, where the title already says it.
- **Changes:** what was added, changed or removed, grouped by kind. Name the files.
- **Departures from the ticket:** anything done differently from the ticket's scope, with a one-line reason each. A page-type decision, a scope limit, or a disclosure from a freshness check or a profile's generator goes here, not under an invented extra heading.
- **Before merging:** unresolved `// DOCS WRITER VERIFY:` items or open questions, as a pointer to the gap list, not a restatement of it.
- **Review checks:** concrete and specific to this change. Never a generic "verify it renders" or "confirm links work". Every check must name something in this diff a reviewer could get wrong or miss. Leave the section out if there's nothing that specific.

Leave out any section that would be empty or padded.

## Linking the pages

The docsite build bot posts its own list of preview links on every PR, but it's unordered and below the fold, and reviewers rarely look at it. **Link every created or changed page in the PR description instead**, where a reviewer sees it straight away, in an order that helps.

**Order by significance first, then by position in the site nav. Never alphabetically.**

1. **New pages** first.
2. **Existing pages with substantial content changes** next. Judge "substantial" by the proportion of the page that changed, not an absolute line count: ten changed lines is substantial on a 40-line page and trivial on an 800-line one.
3. **Existing pages with a small, targeted edit** next.
4. **Pages touched only incidentally** (a `nav.adoc` entry, a cross-link added from an unrelated page, a partial-only change) last. These can usually be grouped into one line.

Within a tier, order by each page's position in its module's `nav.adoc`, the site's own hierarchy, not by filename or title.

For example, a PR that substantially rewrites three pages and makes minor edits to six others lists the three rewrites first, in nav order, then the six minor edits, in nav order.

**Link target: the staged preview page, not the repo source file.** The reviewer is there to check the rendered page. The preview URLs only exist once the build bot has commented on the PR, which takes seconds; `skills/draft-docs/pr-and-jira-output.md` section 3 covers how to wait for it, read its table, and fall back to a repo link (disclosed in the description) for any page without a preview.

**Link text: the page's title** (its `= Heading` line), not the filename or path. A list of titles tells a reviewer what they're looking at before they click.

## Don't cite incidental source material unless asked

As with the Jira standard, don't link to a planning doc, a Slack thread or an unrelated earlier ticket unless asked. This doesn't apply to the Pages Changed list, which is the PR's own output.

## Never include SME questions

Questions for a reviewer belong in review comments: inline where there's a specific line, top-level where there isn't (`skills/draft-docs/pr-and-jira-output.md` section 4). Never in the description.

## Don't change the description once the PR is open, with one exception

If something changes materially after opening (a fix round changes the scope, or a reviewer's input changes what "done" means), don't rewrite the description to match. Post the update as a PR comment. If a reviewer opening the PR fresh could be misled without it, add one line to the top of the description: `NOTE: see <link to comment> for an update.` Change nothing else. Minor corrections, like a typo or a broken link in the description, don't count as material and can just be fixed.

Filling in the Pages Changed preview links straight after opening (below) is part of creating the PR, not a change to it.

## Writing guidance

- Read the diff (`git diff main...HEAD`, plus uncommitted changes) before writing. Describe what the diff shows, not what was planned.
- Write for a reviewer who wasn't part of the run.
- American English, sentence case, no em dashes. Search for the literal `—` character before output; don't assume you avoided it.

## Output

Inside `skills/draft-docs/SKILL.md`, write the body straight into the PR when you create it (`skills/draft-docs/pr-and-jira-output.md` section 1). When a writer asks you directly, show them the description first, then create or update the PR when they're happy. Pages Changed can't have its preview links yet, so write everything else at creation, then fill in the preview links once the build bot's comment arrives (`skills/draft-docs/pr-and-jira-output.md` section 3).

## Before finishing

- The description opens with `Jira: [TICKET-KEY](<link>)`, then a plain, unlabeled sentence, not a "Summary" heading.
- Every created or changed page is linked, ordered by significance then nav position, never alphabetically, with the page title as link text and the preview URL as the target (or a repo link where no preview was available, disclosed as such).
- No references to incidental source material the user didn't ask for.
- No SME questions anywhere in the description.
- Every review check names something specific to this diff.
- If the PR was already open and something changed materially: a comment was posted and, only if a fresh reader could be misled without it, a one-line `NOTE:` pointer was added to the top of the description. Nothing else changed.

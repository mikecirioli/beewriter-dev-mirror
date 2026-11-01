# Output: the draft PR and the gap list

The last stage. By this point the content is drafted, self-checked and committed, and the gap list (`shared/gap-list.md`) is built. This file is purely mechanical: it doesn't decide what to say, only how to post it.

## 1. Open the draft PR

- **Title:** `[TICKET-KEY] <short summary>`. Jira picks this up and links the PR in the ticket's Development panel, but nothing from Jira appears inside the PR itself. That's why `skills/pr-description/SKILL.md` opens every PR body with an explicit `Jira: [TICKET-KEY](<link>)` line. Don't skip it on the assumption the title covers it.
- **Branch name:** the ticket key. **Branch from `origin/main` explicitly.** The local checkout may be on an unrelated or stale feature branch. Check `git status` before branching, and stash first if the working tree isn't clean.
- **State: draft**, not ready for review. A draft PR also triggers the docsite-engine build and recommendations check before anyone looks at the content.
- **Body:** follow `skills/pr-description/SKILL.md`, the shared standard for every profile. It covers structure, the ordered Pages Changed list, language rules, and keeping the description unchanged after opening.

## 2. Commit

- The generated AsciiDoc file or files.
- The module's `nav.adoc` update. New pages must be added there.

## 3. Finalize the Pages Changed section with preview links

Reviewers get far more from a rendered preview than from a repo file link, so wait for the preview bot:

- Poll `GET /repos/.../issues/{N}/comments` for a comment from `cloudbees-docs-staging[bot]`. Check every few seconds and time out at 2 minutes. It normally posts within about 10 seconds.
- Parse its `| File |` table (`| [/site/path](preview URL) |` rows) directly. Don't recompute the repo-path-to-site-path mapping: the bot already does it correctly, and its list already leaves out partials and nav-only changes.
- Update the PR body to replace each Pages Changed entry's link with the matching preview URL. Use `gh api repos/OWNER/REPO/pulls/N --method PATCH` (see `shared/github-api-notes.md` for why not `gh pr edit`).
- If the bot doesn't comment within the timeout, or a page isn't in its table, keep the repo file link for that page and say so in the PR description. Don't block the rest of the run on one missing preview.

## 4. Post the gap list as one batched PR review

- One review (`COMMENT` event), not one API call per question.
- Each critical or important question from `shared/gap-list.md` that relates to a specific line becomes an inline review comment on that line.
- Any question that doesn't relate to a line goes in a top-level comment on the same review.
- Submit the whole review in one action, so it sends one notification, not several.
- **Don't @-mention anyone, and don't request a reviewer.** The writer is the PR's author and is notified of the review automatically.
- **After submitting, re-fetch and count.** `GET /repos/.../pulls/N/comments` and check the count matches what you intended before telling the writer it posted. A successful response for the review doesn't prove its inline comments attached (see `shared/github-api-notes.md`).

## 5. Add the PR link to the ticket, two ways

Jira's Development panel already links the PR, but it's a sidebar that many people don't notice. Do both of these:

- **Add one line to the top of the ticket description:** `PR: [#N](<link>)`, as allowed by `skills/jira-ticket/SKILL.md`. Don't change anything else in the description.
- **Post a Jira comment** with the PR link and the number of open questions: "Opened a draft PR with N open questions: `<link>`." Nothing else; the detail lives in the PR. The comment is for reviewers who follow Jira rather than GitHub.
- Use the same language rules as the PR body: sentence case, American English, no em dashes.
- **If drafting turned up separate work that needs its own ticket**, write it to `skills/jira-ticket/SKILL.md`'s standard. Link it from a comment on the original ticket rather than adding it to the original ticket's description.

## 6. Leave the PR as draft

Don't mark it ready for review. That's the writer's decision. The run ends once the draft PR and gap list both exist.

Feedback that arrives after this is handled by `skills/respond-to-review/SKILL.md`.

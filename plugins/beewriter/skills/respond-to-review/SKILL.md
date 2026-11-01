---
name: respond-to-review
description: Work through review feedback on a CloudBees docs PR. Read every open comment, make the fixes, reply on each thread, resolve what's done, and re-request review. Use when the user asks to address, handle, respond to, or work through review comments or feedback on a docs PR, or asks what's still outstanding on one.
---

# Respond to review feedback on a docs PR

File paths in this skill are relative to the BeeWriter plugin root, two folders up from this file.

Works on any docs PR, whether or not `skills/draft-docs/SKILL.md` opened it.

## Steps

1. **Find everything that's open.** Use the GraphQL `reviewThreads` query filtered to `isResolved: false`, plus top-level comments. Don't rely on a REST comments fetch (see "Don't treat a REST comments fetch as complete" below).
2. **Sort each comment:** a correction to make, a question to answer, a judgement call or scope decision for the writer, or a conflict with a source you've checked. Before treating something as needing a person, check whether an authoritative source already answers it (`skills/review-docs/SKILL.md`, "Check the authoritative source").
3. **Make the fixes** on the PR's branch, following BeeWrite (`shared/beewrite-core.md`) and the rules below. Commit; never merge.
4. **Reply and resolve** as described below.
5. **Report to the writer** what changed, what's waiting on them, and what's waiting on a reviewer.

## Replying, resolving and re-requesting

**Inline (threaded) review comments: reply, then resolve, but only once it's fixed.** Reply on the thread saying what changed, then resolve the conversation. A reply alone leaves the thread looking open; resolving without a reply loses the reason for anyone who revisits it.

- A reply uses the REST comments endpoint with `in_reply_to` set to any comment ID in that thread.
- Resolving isn't available over REST. It needs the GraphQL `resolveReviewThread` mutation, which takes the thread's node ID (`PRRT_...`), not a comment's database ID. Fetch thread IDs with a GraphQL `reviewThreads` query first.
- If a comment wasn't actioned (deferred, answered with a question, or a scope decision for the writer), reply explaining why and leave the thread unresolved. An honest "not yet" is better than silence.

**Top-level (non-inline) comments get their own direct reply**, naming who asked, rather than being folded into a general summary. They can't be resolved, so a visible reply is the only way to show they were addressed.

**If a comment links an attachment you can't open (a PDF, an image, any uploaded file), say so and ask.** Don't guess, and don't skip it silently. GitHub serves comment attachments from `user-attachments/...` URLs that need a signed-in browser session; API tokens, including GitHub App tokens, get a 404. Name the comment, say the attachment can't be opened through the API, and ask the writer to paste the relevant content or save the file locally and give you the path.

**Once every thread is resolved or has a clear open question, re-request review from people who've already reviewed this PR.** Only people with a submitted review already on the PR (a `COMMENTED` review counts), never anyone new. Check completion with the same `reviewThreads` query: every thread must be resolved or have a reply. Re-request once per round of fixes, not once per comment.

**Don't treat a REST comments fetch as complete.** `pulls/N/comments` paginates at 30 results by default and gives no sign that it's truncated, so it can silently miss unresolved comments. The GraphQL `reviewThreads` query, filtered to `isResolved: false`, is the reliable check. Run it before reporting that a PR's feedback is fully handled or re-requesting review.

## Writing the fixes and replies

### Don't lift an SME's comment prose into documentation

When an SME's review comment supplies new facts, such as the business value of a feature, **extract the facts and write the sentence fresh in house style**, as you would with a ticket description. Lightly copy-editing their sentences shows: you get long compound sentences joined by "but", which is how people write quick PR comments, not how BeeWrite writes. Only keep their exact wording when it must be exact (a precise technical term, an error message, something they've asked to be quoted). SME comments are written quickly, often by non-native English speakers, and never for customers. However fluent they sound, treat them as draft material, not publishable prose.

### When replying to a resolved comment, state what changed

Most review comments are corrections of fact, not opinions to agree with. State plainly what changed. A reply like "agreed this isn't true until X ships" frames a fact as a judgment call that never existed. Save "agreed", "good point" and "you're right that..." for the few comments that really are judgment calls.

### Don't settle conflicts between a verified source and a reviewer; flag them

If a reviewer's claim conflicts with a source you've checked (for example, a reviewer says a value is missing from a list, and the API spec doesn't include it either), flag it as a `// DOCS WRITER VERIFY:`, naming both sides. Don't silently add the value, and don't silently keep the source's version.

Deciding which side wins depends on who has authority on that specific point, and you can't tell that from a GitHub username. The engineer who built the feature, the PM closest to the ticket, and an uninvolved commenter can all look the same. Let the writer resolve it. **Once the writer gives a clear answer, act on it straight away and stop flagging it.** The uncertainty was about authority, and that's now settled.

## Tool notes

Follow `shared/github-api-notes.md` when replying, resolving or re-requesting through `gh`.

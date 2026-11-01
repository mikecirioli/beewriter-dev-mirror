# Build the gap list

Runs after the self-check (`skills/review-docs/SKILL.md`) has fully finished and the content is committed — never before, and never interleaved with editing. A gap-list question anchored to a line that then gets edited goes stale the moment it changes; sequencing this strictly after self-check is what prevents that.

## Classify every open point

Carry forward the three categories from the analysis step (`skills/draft-docs/profiles/*/analyse.md`):

- **Critical** — without this, the page could be actively wrong, not just incomplete. Becomes a question.
- **Important** — meaningfully affects quality or completeness, not correctness. Becomes a question.
- **Nice-to-have** — becomes a line in the PR description, never a question. Don't ask an SME something that doesn't need their input to be useful.

## Cap

Keep critical + important questions to **5 or fewer**. If there are more than that:

- Don't fire a long list at anyone. Stop short.
- Post a note to the writer (not an SME) that the ticket produced more open questions than a reasonable gap list should carry, and why — this is the same signal as step 5 of the pipeline ("not enough to draft"), just discovered one stage later.

## Line-specific vs general

Most gaps tie to one line or sentence — these get an inline, line-anchored comment (`skills/draft-docs/pr-and-jira-output.md`). Some don't (a scope question like "does this apply to the Essentials plan" isn't about any one sentence) — these get a top-level comment on the same batched review, not a forced line anchor.

## Write each question so it's answerable in one reply

Every question should:

- Name what you already checked (the ticket, the linked PR, the comparable page you drafted from) and that it wasn't enough — don't ask something the ticket already answers.
- Be specific enough to answer in a sentence. "Is this right?" is not a gap-list question; "does the Essentials plan include this field, or only Enterprise?" is.
- Never invent a plausible-sounding answer and ask for confirmation of it dressed as fact — ask the open question directly.

This is the quality bar the forward-unchanged-rate measurement depends on. A vague or already-answered question is exactly what erodes the goodwill this whole design is trying to protect.

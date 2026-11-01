# Ingest the ticket

Input to the whole run is one Jira ticket key. This stage turns it into what the rest of the pipeline needs.

## Read

- The ticket's summary, description, and acceptance criteria (if any).
- Linked PRs. The team's PR title convention (`[TICKET-KEY] summary`) means a PR referencing this ticket is usually findable by searching for the ticket key in PR titles/branches in the repo(s) `shared/repo-map-lookup.md` resolves — there is no dev-panel API available to this skill, so this text-match is the mechanism, not a shortcut.
- `fixVersion` / release target, if set — useful context for the draft, not required to proceed.
- Any linked tickets (duplicates, blocks, relates-to) — read for context; don't chase the whole graph.

## Read-only, always

This stage never writes to Jira. It only reads the ticket and whatever it links to.

## If the ticket links to an external spec or API docs page

API docs pages are often JS-rendered (Scalar, for example), so a plain fetch returns little more than the page title. Guessing a default spec path (`/openapi.json`) on the same host may return `401 Unauthorized`, which looks like an access problem but usually just means the wrong filename. **Don't conclude the spec is inaccessible from a 401 on a guessed path.** Fetch the page's raw HTML directly (a plain `curl`, not a fetch tool that converts to Markdown) and look for the spec file's URL in its embedded config, usually a `<script>` block naming a `.yaml` or `.json` file. Public API docs are often public with no auth at all once you find the real file.

## If the ticket itself is missing basics

A ticket with no description and no linked PR isn't necessarily a dead end — `shared/repo-map-lookup.md` and the product repo may still supply enough. But if this stage finds effectively nothing (no description, no linked PR, no resolvable repo), say so explicitly when the pipeline reaches step 5 (can a draft even be written) — don't let a thin ingest quietly turn into a thin, guessed draft.

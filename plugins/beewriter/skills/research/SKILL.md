---
name: research
description: Gather the context behind a CloudBees docs topic or Jira ticket (the ticket and its links, related PRs, the product repo that holds the code, and the existing docs pages that cover it), and summarize what's known and what isn't. Use when the user asks for background, context, or research on a ticket or feature, asks which repo holds the code for a product area, or asks what the docs already say about something.
---

# Research a docs topic or ticket

File paths in this skill are relative to the BeeWriter plugin root, two folders up from this file.

Read-only. This skill never writes to Jira, GitHub or the docs.

## Starting from a ticket

1. **Read the ticket** as `shared/jira-ingest.md` describes: summary, description, acceptance criteria, linked PRs, linked tickets and fix version.
2. **Find the product repo** with `shared/repo-map-lookup.md`, from the ticket's component.
3. **Read the code that matters**: shallow-clone the product repo as in `shared/freshness-check.md` section 3, and read the linked PRs' changes and the files around them.
4. **Find the existing docs** that cover the area (below).

## Starting from a topic

1. **Search Jira** for recent tickets on the topic, and read the most relevant ones as above.
2. **Find the product repo** by matching the topic to a product area in `shared/product-repo-map.yaml`. If nothing matches, say so rather than guessing a repo from its name.
3. **Find the existing docs** (below).

## "Which repo holds the code for X?"

Answer from `shared/product-repo-map.yaml`, and always give its `confidence` (`verified`, `candidate` or `unresolved`) with the answer. Treat candidates as unconfirmed, and say so.

## Finding the existing docs

Search the docs repo you're in, or the right docsite repo for the product (`docsite-cloudbees-unify`, `docsite-cloudbees-ci`, `docsite-cloudbees-cd`), for pages on the topic: titles, `:keywords:`, and the module's `nav.adoc`. List the pages that already cover it and where a new page would sit in the nav.

## What to report

- **What's known**, with where each fact came from (the ticket, a PR, a file in the product repo, an existing page).
- **What isn't known**: the open questions an SME would need to answer, written as `shared/gap-list.md` describes.
- **Where the docs stand**: pages that already cover this, and whether they look current.

Keep facts and guesses separate. Never fill a gap from what a similar product does (see `skills/review-docs/SKILL.md`, "Don't invent syntax or parameters by analogy").

If a repo can't be read, name it and say access may be needed, as `shared/freshness-check.md` describes, then carry on with what you can read.

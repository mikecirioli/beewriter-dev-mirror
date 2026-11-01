# Resolve the product repo

Look up the ticket's product area/component against `shared/product-repo-map.yaml` (currently at `shared/product-repo-map.yaml` — move alongside the skill, or load it from wherever the plugin's final home ends up; don't duplicate it).

## Matching

1. Take the Jira component(s) on the ticket.
2. Find the matching area in the map.
3. Read `confidence`:
   - **`verified`** — get a fresh read of the listed repo(s) (`shared/freshness-check.md` section 3) and proceed normally.
   - **`candidate`** — get a fresh read of the listed repo(s), but say so explicitly in the PR description ("the product repo for this area is unconfirmed; I used `<repo>` on a best-effort basis").
   - **`unresolved`** — there's no repo to read. This is a **critical gap**, not something to skip past: carry it into step 5 of the pipeline (can a draft even be written without it?) and, if drafting proceeds anyway from ticket text alone, flag it as the first item in the gap list.
4. If the ticket's component isn't in the map at all (areas get added or renamed), treat it the same as `unresolved` — don't guess a repo by name-matching on your own.
5. If the map lists a repo but you can't read it, treat it the same as `unresolved` too, and name the repo in the gap-list item (see `shared/freshness-check.md`, "Access failures").

## What this file does not do

It doesn't update `shared/product-repo-map.yaml`. Keeping the map current is a manual task for now — this file only ever reads it.

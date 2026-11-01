# Get a fresh, usable clone before reading

This plugin can run on any machine, not just one with every CloudBees docs and
product repo already cloned as a sibling. Don't assume any clone already
exists. Three different kinds of repo need different treatment.

## 1. The docs repo you're drafting into

This is just your current working directory — the prerequisite in `skills/draft-docs/SKILL.md`
already says to run this from inside it. No cloning needed; read and write the
working tree directly, same as any normal git workflow. The one exception:
**branch from `origin/main` explicitly** before committing, not whatever the
working tree happens to be on — the checkout may be on a stale or unrelated branch.

## 2. The standards repos: a persistent, shared cache

`cloudbees-beewrite-standards` and `docs/modules/contribution` (both in
`docsite-usage`), plus `docsite-global`, are read on every single run
regardless of which product the ticket is about. Cache them once, reuse, and
refresh periodically, rather than cloning fresh every run:

1. Look for the cache at `.cache/docsite-usage` and `.cache/docsite-global`,
   relative to the docs repo you're running in (gitignore this directory if it
   isn't already).
2. **If missing**, shallow clone it: `git clone --depth 1 https://github.com/cloudbees/docsite-usage.git .cache/docsite-usage` (and the same for `docsite-global`).
3. **If present**, check its age. If the most recent commit (`git -C .cache/docsite-usage log -1 --format=%cd --date=relative`) is more than 7 days old, refresh it: `git -C .cache/docsite-usage pull --ff-only`. If the pull fails (diverged history from an old shallow clone), delete and re-clone rather than fighting it.
4. **One exception**: if the ticket's own content is about `docsite-usage` itself (a BeeWrite standards change, like adding or fixing a rule), you're already running this skill from inside `docsite-usage` per section 1 above. Don't also maintain a separate cached copy of the repo you're sitting in — read the working tree directly, same as any other drafting target.

## 3. Product-code context repos: ephemeral, shallow, per run

Repos read only for this specific ticket's technical context (resolved via
`shared/repo-map-lookup.md`) don't need a persistent cache — there's nothing to keep
fresh, since each run cares about a specific, current state, not history.

1. Shallow clone into a scratch directory, not a sibling of anything persistent: `git clone --depth 1 <repo-url> "$(mktemp -d)/<repo-name>"`.
2. Read what you need. Don't keep it around after the run finishes — this is disposable, not a cache.
3. **Clone several repos in parallel, not serially**, if a ticket needs more than one for context. A shallow clone of even a large repo is fast (`docsite-cloudbees-ci` takes under 10 seconds), but several one after another adds up for no reason.

## Access failures: never skip silently, never guess

When the credentials in use can't read a repo, the clone fails with what looks like a generic git error, usually a 404, because GitHub doesn't reveal that a private repo exists. **Don't treat it as a transient failure to retry, don't skip the repo silently, and never guess what it contains.** Name the repo and say access may be needed: "Could not access `<repo>`. This may need an access grant." `docsite-cloudbees-cd` and `docsite-cloudbees-common` are private, not readable org-wide, so they're the most likely cause.

What happens next depends on the repo:

| Repo you can't read | What to do | Why |
|---|---|---|
| Standards: `docsite-usage`, `docsite-global` | **Stop the run.** | You can't draft or review to BeeWrite without BeeWrite. |
| `docsite-cloudbees-common` (shared CI and CD/RO partials) | **Stop the run.** | Pages include these partials, so without them you'd be guessing what the page already says. |
| A product-code repo, read for context | **Carry on, and make it the first gap-list item** (`shared/gap-list.md`). | It's the same as a product area with no known repo (`shared/repo-map-lookup.md`). Pipeline step 5 in `skills/draft-docs/SKILL.md` still decides whether there's enough left to draft. |

The docs repo you're drafting into can't be unreadable: you're running inside it.

In `skills/research/SKILL.md`, which only gathers context, report any repo you couldn't read and carry on with the rest.

## What this is not

Not a general "keep the whole workspace pulled" instruction. The standards
cache is the only thing with any persistence at all, and it exists because
those specific repos are read on every run, not because this skill manages
repo hygiene generally.

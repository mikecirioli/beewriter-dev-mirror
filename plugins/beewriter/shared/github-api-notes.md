# GitHub API notes

Gotchas that apply whenever a skill writes to GitHub through `gh`. Each one fails quietly or misleadingly, so follow them every time.

- **`gh pr edit --body` fails on repos with legacy Projects (classic) metadata**, with `GraphQL: Projects (classic) is being deprecated...` (for example on `docsite-cloudbees-unify`). The edit doesn't apply and leaves nothing to clean up. Update the body through REST instead: `gh api repos/OWNER/REPO/pulls/N --method PATCH --input payload.json`, with a `{"body": "..."}` JSON file.
- **Send array fields as real JSON, not `gh api -f`/`-F` bracket syntax, on every endpoint.** On `pulls/N/reviews`, `-f 'comments[][path]=...'` returns success and a review ID but creates a review with no inline comments. On `pulls/N/requested_reviewers`, `-f 'reviewers[]=...'` fails with a 422. A clean exit code doesn't mean the array landed. Build the full payload as a JSON file and submit it with `gh api ... --input payload.json` whenever an endpoint takes an array.

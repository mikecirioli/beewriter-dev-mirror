# Examples: a manifest, not copies

These are real, live pages in `docsite-cloudbees-unify`. Read each listed file directly from the repo before drafting the matching page type. They're listed rather than copied here so they can't go stale when the live page changes.

**Covered:** how-to, explanation, and reference. There are no tutorial examples yet; see `skills/draft-docs/profiles/unify-diataxis/generate-tutorial.md` for how to draft tutorials without them.

## How-to

| File | Notes |
|---|---|
| `docs/modules/platform-administration/pages/how-to-guides/manage-organizations.adoc` | Clean. Good match of admonition to severity (NOTE, IMPORTANT, WARNING). |
| `docs/modules/platform-administration/pages/how-to-guides/configure-saml-single-sign-on.adoc` | Clean overall. One debatable call: it uses `CAUTION` for an irreversible action, where `WARNING` fits the style guide's severity split better. Don't copy that choice. |
| `docs/modules/platform-integration/pages/how-to-guides/configure-source-code-management.adoc` | Clean. An overview table, then a repeated "To integrate with X:" section per SCM provider. |
| `docs/modules/release-orchestration/pages/how-to-guides/deploy-to-kubernetes.adoc` | Clean. Shows the pattern for action-heavy pages: action reference wrapped in a how-to, with inputs pulled in by `include::` and worked usage examples. |

## Explanation

| File | Notes |
|---|---|
| `docs/modules/release-orchestration/pages/explanation/understanding-release-orchestration.adoc` | **Read this one first.** Tight, with a useful ASCII hierarchy diagram and a clear "why we separated X from Y" section. Close to a model answer for `skills/draft-docs/profiles/unify-diataxis/generate-explanation.md`. |
| `docs/modules/platform-administration/pages/explanation/understanding-organizations.adoc` | Clean. |
| `docs/modules/platform-administration/pages/explanation/understanding-components.adoc` | Structurally clean, but the opening restates "components connect code to platform features" across several paragraphs. Don't copy that redundancy. |
| `docs/modules/unify-ai/pages/explanation/understanding-the-mcp-server.adoc` | Clean and thorough. Longer, and covers more reference-like ground (tool catalog, security) than the release-orchestration page: a valid, broader style of explanation. |

## Reference

| File | Notes |
|---|---|
| `docs/modules/platform-administration/pages/reference/rbac-permissions-reference.adoc` | Clean. A permissions table plus a predefined-roles section, consistently formatted. |
| `docs/modules/edge-runners/pages/reference/edge-runner-api-reference.adoc` | Clean. The same Endpoint, Parameters, Request Headers, Response, Example pattern for every operation. A good API-reference model. |
| `docs/modules/unify-ai/pages/reference/mcp-tool-reference.adoc` | Clean. Organised by category with a consistent definition-list pattern. Deliberately austere, as reference should be. |

## The `:diataxis-type:` attribute

Every page above sets `:diataxis-type:` (`how-to`, `explanation`, or `reference`) near the top. Every new page must too: each `generate-*.md` sets it, and `skills/review-docs/SKILL.md` checks it against the page-type decision.

## Maintaining this list

To add an example, it must:

- carry no `// DOCS WRITER VERIFY:`, `TODO` or `FIXME` markers
- follow the title convention for its type
- have the required sections (for example, a Related pages section)
- follow every heading with explanatory text.

Avoid modules with known defects. The `continuous-integration` module and parts of `application-security` aren't used for this reason. Keep notes to what a drafter should copy or avoid.

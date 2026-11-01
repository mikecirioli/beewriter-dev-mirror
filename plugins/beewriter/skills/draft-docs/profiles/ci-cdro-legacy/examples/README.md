# Examples: a manifest, not copies

These are real, live pages in `docsite-cloudbees-ci` and `docsite-cloudbees-cd`. Read each listed file directly from the repo before drafting the matching page type. They're listed rather than copied here so they can't go stale when the live page changes.

They're only judged against BeeWrite, not Unify's Diataxis rules. This profile has no Tutorial type and doesn't use Unify's strict type separation or title exemptions.

## Anchor syntax

`[#id]`, `[id=id]` and `[[id]]` are all valid AsciiDoc. BeeWrite's `links.adoc` prefers `[#id]` for new content but doesn't deprecate `[[id]]`. Several CD/RO examples below use `[[id]]`. That's cosmetic, not a defect: don't flag it in existing pages, and use `[#id]` in new ones.

## Concept framing before a procedure is correct

Several CI procedures open with a short concept or explanation section before their steps. That's the house pattern (BeeWrite's "Restate the problem or process" in `best-practices.adoc`), not type mixing. Copy it.

## CI

| File | Notes |
|---|---|
| `docs/modules/kubernetes-install-guide/pages/gateway-api-install.adoc` | **The strongest of the set. Read this one first.** |
| `docs/modules/pipelines/pages/cloudbees-pipeline-explorer-plugin.adoc` | Clean. |
| `docs/modules/mcp-router/pages/oauth.adoc` | Clean. |
| `docs/modules/mcp-router/pages/claude-code.adoc` | Clean. |
| `docs/modules/secure/pages/service-accounts-casc.adoc` | Clean. |
| `docs/modules/secure/pages/service-accounts-get-started.adoc` | Clean. "Get started with…" is a valid verb-first title, not on the banned list (*Use, Work with, Overview, Introduction, About*). |
| `docs/modules/pipelines/pages/cloudbees-pluggable-storage.adoc` | Clean. Concept framing before the procedure (see above). |
| `docs/modules/secure/pages/cloudbees-mask-secrets.adoc` | Clean. Concept framing before the procedure. |
| `docs/modules/kubernetes-install-guide/pages/gateway-api-namespace-topologies.adoc` | Clean. Concept framing before the procedure. |
| `docs/modules/kubernetes-install-guide/pages/gateway-api-migrate-ingress.adoc` | Clean. Concept framing before the procedure. |
| `docs/modules/cloudbees-unify-integration/pages/ci-integration-data-transmission.adoc` | Clean. Reference-shaped; a secondary Reference model (see below). |

## CD/RO

| File | Type | Notes |
|---|---|---|
| `docs/modules/plan/pages/pipelines-releases.adoc` | | **Clean, with no caveats.** |
| `docs/modules/architecture/pages/index.adoc` | Concept | `[[id]]` anchors. |
| `docs/modules/plan/pages/pre-installation-checklist.adoc` | Concept | `[[id]]` anchors. |
| `docs/modules/credentials/pages/index.adoc` | Concept | Clean. |
| `docs/modules/install-k8s/pages/installation.adoc` | Procedure | Mixes `[[id]]` and `[#id]` in the same file. Don't copy that; pick one per page. |
| `docs/modules/maintain-cdro/pages/server-backups.adoc` | Procedure | `[[id]]` anchors. |
| `docs/modules/maintain-cdro/pages/collect-logs.adoc` | Procedure | `[[id]]` anchors. |
| `docs/modules/maintain-cdro/pages/start-stop-servers-agents.adoc` | Procedure | Good cross-module xref, consistent Windows/Linux/macOS structure, proper code blocks. `[[id]]` anchors, and two gerund headings ("Stopping the…", "Starting the…"). Don't copy the gerunds. |
| `docs/modules/pipelines/pages/stage-gate-rules.adoc` | Procedure | Descriptive anchors and cross-references that resolve. One stale link (`#_pipeline_editor` should be `#pipeline-editor`), a typo ("Release Orchestreation") and two double spaces. Don't copy those. |
| `docs/modules/applications-microservice/pages/index.adoc` | Procedure | Procedure-shaped (verb-first title, numbered steps, Prerequisites), but its `:page-category:` says `reference, automation`. Use it as a procedure model; don't copy its page category. |

## Reference

| File | Notes |
|---|---|
| `docs/modules/secure/pages/cjoc-permissions.adoc` (CI) | **The primary CI Reference model.** A pure definition list of permissions with one-line entries and no cross-references. |
| `docs/modules/mcp-router/pages/mcp-tool-reference.adoc` (CI) | Clean. More narrative than `cjoc-permissions.adoc`; use it when a page needs more than a bare definition list. |
| `docs/modules/install-trad/pages/remote-agent-permissions.adoc` (CD/RO) | **The CD/RO Reference model.** A permissions table (action, object, required privilege), one page-only xref, and `:page-category: reference` matching the content. |

## Landing

CI and CD/RO currently use different landing-page shapes. CD/RO is moving to CI's shape, so **every new landing page uses CI's shape, whichever repo it's in.** CD/RO's current shape is only for recognising and amending existing pages. See `skills/draft-docs/profiles/ci-cdro-legacy/generate-landing.md`.

| File | Notes |
|---|---|
| `docs/modules/pipelines/pages/intro.adoc` (CI) | **The example for any new landing page.** Uses `:renderer: section-landing-page` (and no `abbr.adoc` include, unlike every other page type here), with a YAML `quickLinks:` and `cards:` block inside a `[source,yaml,role="renderer"]` literal. |
| `docs/modules/dashboards-built-in/pages/index.adoc` (CD/RO) | **The current CD/RO shape, for amending existing pages only.** Standard header, an overview paragraph, one IMPORTANT admonition, and a flat list of `xref:` links. |

## Don't use as examples

| File | Why |
|---|---|
| `docs/modules/pipelines/pages/stages-and-gates.adoc`, `entry-and-exit-gates.adoc` | Cross-reference fragments built from full heading text that don't match any anchor (for example `#Creating` aimed at `Create_a_rule`). A systematic pattern, not one bad link. |
| `docs/modules/properties/pages/intrinsic-properties.adoc` | Structurally a strong reference page, but its self-references point at `index.adoc#project` and similar instead of its own sections. |

Links in these pages may since have been fixed. They're excluded because the pattern is easy to copy, not because of their current state.

## Maintaining this list

Check any new example for cross-references that don't resolve, especially fragments built from heading text. That's the most common defect in these repos (see `skills/draft-docs/profiles/ci-cdro-legacy/analyse.md`). Keep notes to what a drafter should copy or avoid.

---
name: standards
description: Answer questions about CloudBees documentation standards (BeeWrite style, terminology, AsciiDoc syntax, and the Antora contribution rules) from the current source, with the rule and where it lives. Use when the user asks what BeeWrite or the docs style guide says about something, how to write or format something in CloudBees docs, which word or attribute to use, or whether something is allowed.
---

# Answer questions about the docs standards

File paths in this skill are relative to the BeeWriter plugin root, two folders up from this file.

## Steps

1. **Get a current copy** of the standards: `shared/freshness-check.md` section 2 (`docsite-usage` and `docsite-global`, cached and refreshed when more than 7 days old).
2. **Find the rule.** Start with `shared/beewrite-core.md` for where everything lives:
   - style, structure and terminology: `cloudbees-beewrite-standards/modules/ROOT/pages/`
   - AsciiDoc syntax: `cloudbees-beewrite-standards/modules/syntax/pages/`
   - Antora structure (headers, attributes, summaries, page categories, partials and the situational pages): `docs/modules/contribution/pages/`
   - product attributes: `docsite-global`
3. **Answer** with:
   - the rule, quoted or closely paraphrased
   - the file it's in, so the person can check it
   - an example of right and wrong, if the source has one
   - any exception, such as Unify's Diataxis exceptions or rules that differ between Unify and CI/CD-RO.

## If the standards don't cover it

Say so plainly, and don't invent a rule. If similar pages in the docs repo handle it consistently, you can describe that as the current practice, clearly labelled as practice, not a rule. If the standards contradict each other, quote both and say which file each is in.

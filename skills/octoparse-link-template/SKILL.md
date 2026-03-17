---
name: octoparse-link-template
description: Help users design Octoparse template chains. Use this skill whenever the user asks which Octoparse templates should be linked together, whether one template's output can feed another template's input, how to enrich data across listing/detail/review/contact templates, or when a template seems insufficient and the user needs downstream templates.
---

# Octoparse Link Template

Use this skill to determine whether one Octoparse template can feed another template.

This skill supports two entry modes:
1. Goal-first: the user describes a data goal and needs a recommended template chain.
2. Template-first: the user names a template and wants to know which downstream templates can use its output.

## Output contract

Always provide:
- Recommended chain
- Field mapping
- Why this chain works
- Risks and limitations
- Possible enrichments

## Evidence priority

Use sources in this order:
1. Local template docs:
   - TEMPLATE.md
   - INPUT.md
   - OUTPUT.md
   - LIMITATIONS.md
2. Stable template index in `references/stable-templates.json`
3. Template input metadata from MCP / template detail tools
4. Official template detail pages
5. Inference from template descriptions when no stronger source exists

Clearly label inferred conclusions as inferred.

## Decision process

1. Identify whether the request is goal-first or template-first.
2. Normalize template names if the user names them loosely.
3. Check the stable template index first.
4. Determine required fields for each candidate downstream template.
5. Determine whether the upstream template can provide those fields directly.
6. If direct linking is not possible, check whether an intermediate template is needed.
7. Return the best chain with field mapping and risks.

## Important linking rules

Read `references/linking-rules.md` before making linking decisions.

## Output field inference

If OUTPUT.md is missing, use `references/output-inference-rules.md`.
When output fields are inferred rather than documented, explicitly say so.

## Constraints

- Do not assume that similar field names are interchangeable.
- Distinguish:
  - listing page URL
  - place details page URL
  - website URL
  - email
- Do not claim a template can produce a field unless it is documented or strongly supported by template evidence.
- Prefer stable MCP-supported templates when there are multiple valid options.

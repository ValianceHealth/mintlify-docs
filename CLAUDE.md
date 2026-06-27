# HealthProximate Documentation — Claude instructions

This is the **public** documentation site for **HealthProximate** (the product) by
**Valiance Health** (the company), built on [Mintlify](https://mintlify.com). It is the
Stage 1 public documentation footprint: a credible, customer- and auditor-friendly help
center. The full internal API reference stays private behind controlled access.

## Working relationship
- You can push back on ideas — this can lead to better documentation. Cite sources and explain your reasoning when you do so.
- ALWAYS ask for clarification rather than making assumptions.
- NEVER lie, guess, or make up anything.

## Project context
- Format: MDX files with YAML frontmatter
- Config: `docs.json` for navigation, theme, and settings
- Components: Mintlify components (`Card`, `Steps`, `Accordion`, `ParamField`, callouts)
- For Mintlify product knowledge (components, configuration, writing standards), install the Mintlify skill: `npx skills add https://mintlify.com/docs`

## Terminology
- The product is **HealthProximate**; the company is **Valiance Health**.
- Refer to the five core capabilities as **workflows**: entity resolver, dashboard, analytics, predictions, simulation.

## Content strategy
- Document just enough for user success — not too much, not too little.
- Prioritize accuracy and usability.
- Make content evergreen when possible.
- Search for existing content before adding anything new. Avoid duplication unless it is done for a strategic reason.
- Check existing patterns for consistency.
- Start by making the smallest reasonable changes.

## Content boundaries (public-safe — important)
This is a **public** site. Review every page for internal references and endpoint
leakage before considering it done. Do **not** add:
- The full API schema / Swagger, or internal / administrative / operator endpoints
- Tenant-specific or customer-specific names, data, or examples
- Internal file paths, serializer / view names, or implementation internals
- Unstable / experimental routes
- Secrets, API keys, or credentials

It is fine — and intended — to state that detailed internal API references remain
access-controlled and private. `api/overview.mdx` already communicates this split.

## Verified product values (use these exactly; do not invent enums)
- **Analytics metrics:** `revenue`, `hospital_revenue`, `profit`, `margin`, `cost`, `discount`, `los`, `time`, `readmission_30`
- **Analytics view types:** `detail`, `avg`, `sum`
- **Predictions metrics:** `price`, `cost`, `time`, `profit`
- **Predictions gender:** `M`, `F`, or unknown/blank
- **Predictions age:** numeric `0`–`120`, or legacy age bands
- **Predictions secondary conditions:** OMOP concept IDs (not a fixed enum)
- **Simulation:** new/unseen item estimation is **not** supported — do not overclaim it.

## Support contact
- The canonical public support address is **admin@valiancehealth.ai** (used throughout the site and in `docs.json`). Confirm the preferred public alias before any launch.

## docs.json
- Refer to the [docs.json schema](https://mintlify.com/docs.json) when editing site config and navigation.

## Frontmatter requirements for pages
- `title`: Clear, descriptive page title
- `description`: Concise summary for SEO/navigation

## Writing standards
- Second-person voice ("you").
- Prerequisites at the start of procedural content.
- Test all code examples before publishing.
- Match the style and formatting of existing pages.
- Workflow pages follow one consistent structure: overview, when to use, inputs, steps, outputs, notes/caveats, support.
- Include both basic and advanced use cases.
- Language tags on all code blocks.
- Alt text on all images.
- Relative paths for internal links.

## Git workflow
- NEVER use `--no-verify` when committing.
- Ask how to handle uncommitted changes before starting.
- Create a new branch when no clear branch exists for changes.
- Commit frequently throughout development.
- NEVER skip or disable pre-commit hooks.

## Do not
- Skip frontmatter on any MDX file.
- Use absolute URLs for internal links.
- Include untested code examples.
- Make assumptions — always ask for clarification.

## Local preview
Install the Mintlify CLI and preview from the repo root (where `docs.json` lives):
```bash
npm i -g mint
mint dev
```
View at `http://localhost:3000`. Note: pages have not necessarily been rendered by the
CLI in every environment — run `mint dev` as part of review.

## Background and planning artifacts
This site implements the plans under `.hermes/` (planning/passover material, **not
published**):
- `.hermes/plans/2026-06-26-product-documentation-compliance-plan.md`
- `.hermes/plans/2026-06-26-mintlify-public-docs-ia.md`
- `.hermes/plans/2026-06-26-mintlify-implementation-plan.md`
- `.hermes/imports/healthproximate-stage1-draft/` — the imported Stage 1 source draft and its `DRAFT-OVERVIEW.md` (content provenance, public/private rationale, open TODOs).

Open items still to confirm with product/security owners: SLAs, onboarding sign-offs,
the public OpenAPI subset (Stage 2), the preferred public support alias, and hosting
shape (`valiancehealth.com/docs` vs `docs.valiancehealth.com`).

## Compliance and tracking (Linear)
- This work supports the **Product Documentation** compliance control (Vanta `product-documentation`) — it provides the public service description, customer documentation, and visible support path while the full internal API reference stays private.
- Tracking issue: **VAL-190** on the **Valiance Health** (`VAL`) Linear team. The Linear MCP server is connected — use it to read/update the relevant issues rather than guessing status.
- Once public docs are live, the evidence is public URLs + screenshots (docs home, onboarding, FAQ, support, API overview) attached to the Vanta document.

> A condensed mirror of these instructions lives in `AGENTS.md` for non-Claude agents.
> Keep the two in sync when the project-specific facts above change.

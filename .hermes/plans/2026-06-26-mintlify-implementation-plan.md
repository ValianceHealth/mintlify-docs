# HealthProximate Public Documentation — Mintlify Implementation Plan

## Goal
Launch a Mintlify-based public documentation site for HealthProximate that:
- satisfies the Vanta **product documentation site** requirement quickly,
- gives customers and prospects a credible help center and onboarding surface,
- provides a polished **public API** presence,
- preserves the existing **private** `/api/docs` setup behind Tailscale/WAF for full internal/deep technical reference.

---

## Decision
We will plan around **Mintlify** as the public docs platform.

### Why Mintlify
- fast path to a polished public docs/help-center experience
- supports Markdown/MDX content in repo
- supports API docs via OpenAPI when ready
- lower infra/setup burden than Docusaurus
- better near-term fit for compliance optics and customer-facing presentation

### What remains private
The current full `/api/docs` should remain restricted.

Keep private:
- complete OpenAPI/Swagger
- internal/admin/operator endpoints
- sensitive implementation details
- unstable/experimental routes
- tenant-specific examples

---

## Target outcome
We will have a public docs site with these functions:
1. **Help center**
2. **Getting started / onboarding**
3. **Workflow guides**
4. **FAQ**
5. **Support page**
6. **Public API overview**
7. **Release notes**

This is the minimum credible public documentation footprint for compliance and customer confidence.

---

## Recommended hosting model
Preferred options:
- `docs.valiancehealth.com`
- or `valiancehealth.com/docs`

### Recommendation
Prefer **`valiancehealth.com/docs`** if the goal is a tighter public-company/docs experience.

Prefer **`docs.valiancehealth.com`** if you want cleaner separation and easier future docs operations.

Either is acceptable for compliance as long as it is public, stable, and clearly part of the official documentation surface.

---

## Stage 1 — Compliance fast path

### Objective
Get a credible public documentation surface live as quickly as possible.

### Required public pages
- `/docs`
- `/docs/getting-started`
- `/docs/workflows/entity-resolver`
- `/docs/workflows/dashboard`
- `/docs/workflows/analytics`
- `/docs/workflows/predictions`
- `/docs/workflows/simulation`
- `/faq`
- `/support`
- `/docs/api/overview`
- `/release-notes`

### Why this is enough for stage 1
This set covers:
- service description
- user guidance
- onboarding/help content
- support availability
- public technical guidance

That lines up well with the Vanta need without forcing public exposure of the full backend schema.

---

## Stage 1 information architecture

### Top nav
- Overview
- Getting Started
- Workflows
- API
- FAQ
- Support
- Release Notes

### Suggested Mintlify page tree
```text
index.mdx
getting-started/
  index.mdx
  onboarding-checklist.mdx
  first-steps.mdx
workflows/
  entity-resolver.mdx
  dashboard.mdx
  analytics.mdx
  predictions.mdx
  simulation.mdx
api/
  overview.mdx
faq.mdx
support.mdx
release-notes/
  index.mdx
```

---

## Page-by-page content plan

### 1. Docs home (`index.mdx`)
Purpose:
- primary product documentation landing page

Sections:
- What HealthProximate is
- Who it is for
- Key capabilities
- Quick links to workflows
- API overview link
- FAQ link
- Support link

### 2. Getting started (`getting-started/index.mdx`)
Purpose:
- first-stop onboarding page

Sections:
- Who this guide is for
- What access users need
- Initial product orientation
- Recommended first workflow
- Where to get help

### 3. Onboarding checklist (`getting-started/onboarding-checklist.mdx`)
Purpose:
- very practical stage-1 onboarding asset

Sections:
- Access prerequisites
- Data/access expectations
- First screens to review
- First outputs users should validate
- When to contact support

### 4. First steps (`getting-started/first-steps.mdx`)
Purpose:
- bridge between onboarding and detailed workflow guides

Sections:
- How to choose between main workflows
- Common user journey
- Tips for interpreting outputs

### 5. Workflow pages
#### `workflows/entity-resolver.mdx`
Sections:
- What it does
- Why it matters
- Inputs
- Outputs
- Step-by-step usage
- Common questions/caveats

#### `workflows/dashboard.mdx`
Sections:
- What the dashboard shows
- How to navigate it
- Key views and interpretation notes
- Common next actions

#### `workflows/analytics.mdx`
Sections:
- Purpose of analytics
- Filters and key inputs
- Metrics available
- View types
- Interpreting results
- Caveats

Verified details to include:
- Metrics: `revenue`, `hospital_revenue`, `profit`, `margin`, `cost`, `discount`, `los`, `time`, `readmission_30`
- View types: `detail`, `avg`, `sum`

#### `workflows/predictions.mdx`
Sections:
- What predictions are for
- Required inputs
- Metrics available
- Demographic inputs
- How to interpret output
- Caveats/limitations

Verified details to include:
- Metrics: `price`, `cost`, `time`, `profit`
- Gender: `M`, `F`, or unknown/blank
- Age: numeric `0-120` or legacy age bands
- Secondary conditions: OMOP concept IDs, not a simple fixed enum

#### `workflows/simulation.mdx`
Sections:
- What simulation is for
- Input assumptions
- What outputs mean
- How to compare scenarios
- Known limitations

Important caveat:
- avoid overclaiming “new/unseen item estimation” if not fully backed by current backend support

### 6. API overview (`api/overview.mdx`)
Purpose:
- polished public API landing page without exposing everything

Sections:
- What the API is for
- How access works at a high level
- Common use cases
- Public vs private documentation split
- How to request integration help

### 7. FAQ (`faq.mdx`)
Sections:
- What HealthProximate helps with
- Which workflow to use when
- How onboarding works
- How support works
- How API access is handled

### 8. Support (`support.mdx`)
Sections:
- Support contact path
- What to include in a request
- Product issue reporting guidance
- Integration help guidance
- Escalation expectations if defined

### 9. Release notes (`release-notes/index.mdx`)
Sections:
- Recent updates
- Product improvements
- Documentation changes
- API-related changes when relevant

---

## Content source mapping

## Primary sources already available

### Existing repo docs
Use as seed material:
- `healthproximate/docs/agent-app-guide.md`
- `healthproximate/docs/api/sunway-docs.md`
- `healthproximate/docs/api/agent-api-guide.md`
- `healthproximate/docs/api/multipart-upload-guide.md`

### Slack how-to guide
Use as human-readable workflow skeleton for:
- entity resolver
- dashboard
- analytics
- predictions
- simulation

### Public website content
Use the current public site sparingly for:
- company/product description language
- links to privacy/security pages
- alignment with public-facing tone

---

## Public API plan

### Stage 1 API approach
Do **not** publish the full current schema.

Instead publish:
- API overview page
- possibly a few manual curated endpoint examples
- authentication explanation at high level
- support/integration request path

This gives a public developer surface without oversharing.

### Stage 2 API approach
Move to a polished Mintlify API reference using a **sanitized OpenAPI subset**.

Include only:
- stable customer-facing endpoints
- safe example requests/responses
- customer-relevant models
- supported auth pattern
- error behaviors worth documenting publicly

Exclude:
- admin/internal routes
- operator routes
- unstable endpoints
- internal parameters/notes
- anything that raises disclosure risk without customer benefit

---

## Recommended repo/content model

Use repo-managed docs content as the source of truth.

### Suggested structure
Create a dedicated docs location, for example:
```text
valiancehealth-docs/
  mint.json or docs.json
  index.mdx
  getting-started/
  workflows/
  api/
  faq.mdx
  support.mdx
  release-notes/
```

Alternative:
- keep docs inside an existing repo if preferred, but a dedicated docs repo may be cleaner operationally.

### Recommendation
For speed, use whichever repo will be easiest to deploy quickly.

For long-term clarity, I would lean toward a **dedicated public docs repo** or a clear docs subdirectory with a clean ownership model.

---

## Staged rollout plan

### Stage 1 — fast compliance launch
Deliver:
- docs shell/navigation
- onboarding pages
- 5 workflow pages
- FAQ
- support page
- API overview
- release notes page

Acceptance criteria:
- pages are public and reachable
- docs look polished and coherent
- support path is explicit
- onboarding/use guidance is clear
- Vanta can be shown URLs/screenshots as evidence

### Stage 2 — polished public API
Deliver:
- curated developer docs
- better examples
- auth/concepts/errors pages
- sanitized OpenAPI-based reference if feasible

Acceptance criteria:
- developer-facing public docs are useful without leaking internal breadth
- public/private split is intentional and documented

### Stage 3 — help-center maturity
Deliver:
- troubleshooting pages
- searchable knowledge base refinement
- richer onboarding tracks by user type
- support workflow improvements / maybe support portal later

Acceptance criteria:
- docs become a real customer enablement surface, not just compliance evidence

---

## Vanta evidence plan

Once public docs are live, collect:
- public URLs
- screenshots of docs home, onboarding, FAQ, support, API page
- optional PDF export or archive copy
- link/upload to the Vanta `product-documentation` document

This should materially improve the current evidence gap.

---

## Risks and guardrails

### Risk: exposing too much publicly
Mitigation:
- keep full `/api/docs` private
- publish curated/manual API content first
- review every public page for internal references and endpoint leakage

### Risk: docs become stale
Mitigation:
- use repo-managed MDX
- assign owners
- add docs updates to relevant product/release workflow where possible

### Risk: stage 1 becomes too ambitious
Mitigation:
- prioritize simple but polished pages over completeness
- focus on the 5 workflows + support + FAQ + API overview first

---

## Recommended immediate next steps

1. Choose hosting shape:
   - `docs.valiancehealth.com` vs `valiancehealth.com/docs`
2. Decide repo location for Mintlify content
3. Draft Stage 1 page skeletons in MDX
4. Draft `api/overview.mdx` manually before attempting public OpenAPI generation
5. Publish and use URLs/screenshots for Vanta evidence

---

## Best next artifact
The next best artifact after this plan is:
- a **Mintlify starter content pack** with the actual page skeletons/files for Stage 1

That can then be handed to Claude Code for implementation in repo.

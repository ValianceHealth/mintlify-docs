# ValianceHealth / HealthProximate — Mintlify Public Docs IA

## Goal
Define a Mintlify-friendly public documentation structure that:
1. satisfies Vanta product-documentation expectations quickly,
2. gives prospects/customers a polished public API surface,
3. keeps sensitive/internal/full API docs private behind the existing gated `/api/docs` setup.

---

## Recommended docs model

Use a **2-tier documentation model**.

### Tier 1 — Public Mintlify site
Audience:
- prospects
- customers evaluating integration
- auditors reviewing evidence
- implementation partners

Content:
- product overview
- getting started
- workflow guides
- FAQ
- support
- release notes
- curated public API overview/reference

Properties:
- polished
- indexed/public
- marketing-safe
- no internal/admin endpoints
- no tenant-specific examples

### Tier 2 — Private developer docs
Audience:
- internal engineers
- approved implementation partners
- deeper technical customer support where appropriate

Content:
- full OpenAPI/Swagger
- internal endpoints
- admin/operator flows
- debugging notes
- internal auth/ops details
- sensitive schemas/fields where disclosure is unnecessary publicly

Properties:
- remain behind Tailscale / WAF / allowlist
- treated as restricted implementation docs, not the public documentation site

---

## What Mintlify can take

Best-fit formats for this project:
- `*.mdx` or `*.md` for guides/help center/onboarding/FAQ/support pages
- OpenAPI for curated public API reference pages
- manual API pages where a generated schema page is too raw or too revealing

Recommendation:
- default to **MDX** for most pages
- add a **sanitized OpenAPI spec** only for endpoints we intentionally want public

---

## Suggested information architecture

### Top-level navigation
1. Overview
2. Getting Started
3. Workflows
4. API Reference
5. FAQ
6. Support
7. Release Notes

---

## Suggested page tree

```text
/docs
  index.mdx
  getting-started/
    overview.mdx
    onboarding-checklist.mdx
    first-workflow.mdx
  workflows/
    entity-resolver.mdx
    dashboard.mdx
    analytics.mdx
    predictions.mdx
    simulation.mdx
  api/
    overview.mdx
    authentication.mdx
    core-concepts.mdx
    errors-rate-limits.mdx
    public-reference/        # generated from sanitized OpenAPI OR manual API pages
  faq.mdx
  support.mdx
  security-and-privacy.mdx
  release-notes/
    index.mdx
```

---

## Stage 1 (fast compliance + credible public presence)

Deliver these first:

### 1. `/docs/index`
Purpose:
- high-level product documentation landing page
- links to guides, API overview, support, FAQ

Minimum sections:
- what HealthProximate does
- who it is for
- major product capabilities
- quick links to guides
- support contact path

### 2. `/docs/getting-started/overview`
Purpose:
- basic onboarding page for new customer/users

Minimum sections:
- what users need before starting
- typical first login/use path
- where to begin in the product
- how to get support

### 3. Workflow pages
Create from the Slack guide + repo docs:
- `/docs/workflows/entity-resolver`
- `/docs/workflows/dashboard`
- `/docs/workflows/analytics`
- `/docs/workflows/predictions`
- `/docs/workflows/simulation`

Each page should include:
- what the feature is for
- who uses it
- key inputs
- key outputs
- how to use it step by step
- interpretation notes / caveats
- links to support

### 4. `/docs/api/overview`
Purpose:
- polished API landing page

Minimum sections:
- what the API is for
- who can get access
- authentication at a high level
- common use cases
- how public docs differ from full/private implementation docs
- contact path for integration support

### 5. `/faq`
Minimum sections:
- who should use which workflow
- how to request support
- how data access/integration works at a high level
- where to find API help
- expected onboarding path

### 6. `/support`
Minimum sections:
- support email / intake path
- what to include in a support request
- severity expectations / response framing if available
- integration help request path

### 7. `/release-notes`
Even if light initially, this helps credibility and audit maturity.

---

## Public API recommendation

Build a **curated public API**, not a dump of the current full schema.

### Public API should include
- stable customer-facing endpoints only
- clean endpoint descriptions
- example requests/responses
- authentication overview
- error model
- rate-limit / usage expectations if applicable
- data model concepts customers need to understand

### Public API should exclude
- internal/admin endpoints
- operator-only routes
- experimental or unstable routes
- internal notes/debug params
- tenant-specific examples
- implementation details that increase attack surface without helping customers

### Good public API structure
1. Overview
2. Authentication
3. Core concepts
4. Common workflows
5. Endpoint reference
6. Errors
7. Support / access requests

---

## Content sources already available

Use these as seed content:

### From backend repo
- `healthproximate/docs/agent-app-guide.md`
- `healthproximate/docs/api/sunway-docs.md`
- `healthproximate/docs/api/agent-api-guide.md`
- `healthproximate/docs/api/multipart-upload-guide.md`

### From Slack guide
Use as human-friendly product workflow copy for:
- entity resolver
- dashboard
- analytics
- predictions
- simulation

### Verified values already extracted
- Analytics metric: `revenue`, `hospital_revenue`, `profit`, `margin`, `cost`, `discount`, `los`, `time`, `readmission_30`
- Analytics view type: `detail`, `avg`, `sum`
- Predictions metric: `price`, `cost`, `time`, `profit`
- Predictions gender: `M`, `F`, or unknown/blank
- Predictions age: `0-120` or legacy age bands
- Predictions secondary conditions: OMOP concept IDs, not a simple enum

---

## Recommended authoring approach in Mintlify

### For guides/help center pages
Use hand-written MDX pages.

Why:
- better editorial control
- easier to keep audit/customer wording clean
- easier to avoid exposing raw internal details
- supports screenshots, callouts, examples, and FAQ blocks

### For API reference
Choose one of these:

#### Option A — sanitized OpenAPI spec
Best if:
- there is already a good schema generation path
- we can derive a safe subset
- we want the polished API explorer/reference UX

#### Option B — manual API pages
Best if:
- the current schema is too broad/internal
- we need fine-grained editorial control first
- stage 1 should move fast without schema curation work

### Recommendation
- **Stage 1:** manual API overview + selected manual endpoint pages
- **Stage 2:** sanitized OpenAPI-backed public reference

---

## Staged rollout

### Stage 1 — Compliance fast path
Goal: get Vanta-credible public documentation live quickly.

Deliver:
- docs home
- getting started
- 5 workflow pages
- FAQ
- support page
- API overview page
- release notes page

Evidence for Vanta:
- public URLs
- screenshots/PDF export
- optionally upload/export into Vanta document evidence

### Stage 2 — Public developer polish
Deliver:
- curated public API reference
- better examples
- stronger onboarding flow
- security/privacy cross-links
- changelog discipline

### Stage 3 — Full help center maturity
Deliver:
- searchable knowledge base
- support intake workflow/portal
- role-based onboarding guides
- troubleshooting guides
- integration playbooks

---

## Suggested public/private split language

Use wording like:

> HealthProximate provides public product documentation and curated developer guidance for customer-facing integration workflows. Detailed implementation references and restricted/internal endpoints remain available only through controlled access channels.

This is auditor-friendly and also explains why the public API is intentionally curated.

---

## Implementation note

Best technical fit appears to be:
- host Mintlify docs at `docs.valiancehealth.com` or `valiancehealth.com/docs`
- keep public docs repo-managed as Markdown/MDX
- treat the current gated `/api/docs` as the private deep technical tier

If you want one coherent customer experience, `valiancehealth.com/docs` is probably the cleanest external presentation.

---

## Next artifact to create

From here, the next useful artifact is:

1. a page-by-page content outline for each Stage 1 page, and then
2. a Mintlify starter content set (`index.mdx`, `faq.mdx`, `support.mdx`, `api/overview.mdx`, workflow pages)

That would be enough to hand to Claude Code for implementation or content drafting.

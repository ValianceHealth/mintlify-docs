# Product documentation site compliance plan

## Goal
Stand up an auditor-satisfactory, publicly accessible product documentation presence for Valiance Health / HealthProximate quickly, while preserving the current security posture of the full `/api/docs` Swagger UI and avoiding unnecessary public disclosure.

## Why this matters in Vanta
The open Vanta document `product-documentation` (`Product documentation site`) is currently `Needs document`.

The Vanta document currently has:
- no uploaded files
- no linked URLs
- control mappings:
  - `external-service-impact-notifications` / GOV-6 — system changes externally communicated
  - `service-description-communicated` / PRM-3 — service description communicated
  - `support-system-available` / GOV-12 — external-facing support system exists

This means a credible first pass should cover three things at once:
1. product/service description
2. accessible end-user / customer documentation
3. visible support contact path

## Current-state findings

### Public website
Observed on `https://valiancehealth.com`:
- public marketing site exists
- public pages exist for:
  - `/security`
  - `/privacy-policy`
  - `/terms-of-service`
  - `/blog`
- public pages do **not** currently exist for:
  - `/faq`
  - `/support`
  - `/help`
  - `/docs`

### Backend API docs (`healthproximate`)
In `healthproximate/app/urls.py`:
- `/api/schema/` exists
- `/api/docs/` exists

The repo explicitly documents a two-layer gate:
1. AWS WAF allowlist limited to approved Tailscale App Connector egress
2. app-layer Tailnet-only mixin returning `404` when bypassed

Relevant evidence:
- `healthproximate/app/urls.py:660-674`
- `healthproximate/app/tests/test_spectacular_views.py:175-203`

Conclusion:
- full Swagger is intentionally private and this is reasonable
- this private Swagger should **not** be the only documentation artifact used to satisfy the public-facing documentation request

### Existing internal/customer-style docs already in repo
In `healthproximate/docs/` there is already reusable material, including:
- `docs/agent-app-guide.md`
- `docs/api/sunway-docs.md`
- `docs/api/multipart-upload-guide.md`
- `docs/api/agent-api-guide.md`

Notable detail:
- `sunway-docs.md` already contains a FAQ section and support section, so there is existing seed content that can be adapted into a public help center.

### Frontend app (`healthproximate-v3`)
`healthproximate-v3` appears to be the product frontend/dashboard app, not a documentation site.
Current structure includes:
- auth routes
- dashboard routes
- upload, analytics, simulation, AI, API usage/keys pages

There is no obvious public help-center / FAQ / onboarding route in the current frontend app.

### Existing guide from Slack
The Slack link itself could not be read in-browser because Slack sign-in is required, but the guide contents were later pasted into chat and are now usable as source material.

The pasted guide is a strong seed for the first public onboarding/help-center content because it already covers the core HealthProximate workflows:
- entity resolver
- dashboard
- analytics
- predictions
- simulation

It also aligns well with existing repo documentation, especially `healthproximate/docs/agent-app-guide.md`, which already fills in several of the missing `<TO_FILL_IN>` items from the Slack notes.

Useful verified enum/details pulled from `agent-app-guide.md` for the first docs draft:
- **Analytics metric**: `revenue`, `hospital_revenue`, `profit`, `margin`, `cost`, `discount`, `los`, `time`, `readmission_30`
- **Analytics view type**: `detail`, `avg`, `sum`
- **Predictions metric**: `price`, `cost`, `time`, `profit`
- **Predictions gender**: effectively `M`, `F`, or unknown/blank
- **Predictions age**: either numeric age `0-120` or legacy age bands:
  - `Less than 2`
  - `2-5`
  - `6-12`
  - `13-19`
  - `20-24`
  - `25-44`
  - `45-65`
  - `Over 65`
- **Predictions secondary conditions**: not an enum; they are resolved OMOP concept IDs

This means stage-1 docs do not need to start from zero; they can be assembled from:
1. the pasted Slack how-to
2. `healthproximate/docs/agent-app-guide.md`
3. selected API docs already present under `healthproximate/docs/api/`

## Recommended documentation strategy

## Principle
Do **not** make the full `/api/docs` public.
Instead use a two-tier model:

### Tier A — public documentation (safe, compliance-friendly)
Public site should contain:
- product overview
- onboarding / getting started
- feature guides
- FAQ
- support contact / support intake
- API overview
- curated API reference for approved public endpoints only
- release notes / changelog summary

### Tier B — restricted developer docs (full detail)
Keep these gated:
- full Swagger `/api/docs`
- internal/hidden endpoints
- tenant-specific examples
- operational/admin endpoints
- `/val/*` or other intentionally undocumented routes
- low-level schemas that reveal more than needed

This preserves the current secure posture while giving auditors and customers a legitimate public documentation surface.

## Fast path for compliance (stage 1)
Target: satisfy Vanta quickly with a credible, live, public documentation footprint.

### Deliverables
1. Public `/docs` or `/help` landing page on `valiancehealth.com`
2. Public `Getting Started` page
3. Public `FAQ` page
4. Public `Support` page
5. Public `API overview` page
6. Public `Release notes / product updates` page or blog category
7. Vanta evidence package linking the public pages

### Minimum content required per page

#### 1. Docs landing page
Include:
- what HealthProximate / Valiance products do
- who each module is for
- links to all core docs sections
- "last updated" dates

#### 2. Getting Started / onboarding
Start with a simple operator/customer onboarding page, not a full in-app wizard.
Include:
- who to contact to start
- access prerequisites
- data onboarding prerequisites
- expected implementation steps
- what credentials/information customers must prepare
- what success looks like after setup

#### 3. FAQ
Seed from current repo docs and common customer questions:
- how access works
- supported file formats / integrations
- API key issuance / rotation
- where data is stored
- regions
- support channels
- security / PHI posture (high level)
- what is public docs vs private customer-specific docs

#### 4. Support page
Quickest acceptable version:
- support email alias
- response expectation window
- categories of request
- what to include in a ticket/email
- security escalation path

A basic support email alias + contact form is enough for stage 1 if it is live and public.
A full portal is not required for the audit-first milestone.

#### 5. API overview page
Do **not** dump Swagger publicly.
Instead publish:
- base API purpose
- auth model at high level
- request/response conventions
- rate limit / support expectations if applicable
- a short list of supported public integration flows
- sample request snippets for approved endpoints only
- note that full implementation docs are available to approved customers/developers

#### 6. Release notes / product updates
Use either:
- a docs section with dated release notes, or
- a filtered blog/category for product updates

This helps GOV-6 by showing customer-facing change communication.

## Recommended page architecture

### Public information architecture
- `/docs`
  - overview
  - getting-started
  - faq
  - support
  - api`
  - release-notes
  - security-and-compliance` (optional cross-link to existing security page)

### Later customer-only information architecture
- authenticated docs or portal
  - implementation guides
  - tenant-specific setup
  - advanced API examples
  - troubleshooting
  - integration runbooks
  - full Swagger / schema access

## Recommended content sources to reuse

### Reuse from existing repo docs
Start from:
- `healthproximate/docs/agent-app-guide.md`
  - strong base for feature/workflow explanations
- `healthproximate/docs/api/sunway-docs.md`
  - already has quick start, FAQ, support, error handling
- `healthproximate/docs/api/multipart-upload-guide.md`
- `healthproximate/docs/api/agent-api-guide.md`

### Reuse from existing website
Cross-link existing pages:
- security
- privacy policy
- terms of service
- blog

### Missing source to ingest
- the Slack guide `F0BBS0SNTGA`
  - should be exported and normalized into markdown
  - likely a good source for onboarding/how-to content

## Staged implementation plan

## Stage 0 — audit-first framing (1-2 days)
Goal: prepare content inventory and evidence path.

Tasks:
1. choose docs host pattern:
   - easiest: add `/docs` section to `valiancehealth.com`
   - alternate: `docs.valiancehealth.com`
2. define public-vs-private boundary for documentation
3. select initial 5-7 pages
4. normalize Slack guide into markdown
5. identify support email alias / owner
6. decide what API content is safe for public publication

Acceptance:
- approved sitemap
- approved public/private content boundary
- owner for support + docs upkeep

## Stage 1 — quick compliance launch (3-5 days)
Goal: put a real public documentation footprint live and upload it to Vanta.

Tasks:
1. publish docs landing page
2. publish getting started page
3. publish FAQ page
4. publish support page
5. publish API overview page with curated examples
6. publish release notes page or customer-updates index
7. add links from main website footer/nav where appropriate
8. capture screenshots + URLs and attach/link in Vanta `product-documentation`

Acceptance:
- public URL(s) resolve without login
- docs are clearly customer-facing
- support contact path is public
- Vanta doc has URL link(s) and/or screenshot evidence attached

## Stage 2 — stronger customer help center (1-2 weeks)
Goal: make it genuinely useful, not just audit-minimal.

Tasks:
1. expand onboarding into role-based setup guides
2. add troubleshooting articles
3. add integration guides
4. add release notes cadence/process
5. add contact / request forms with routing
6. add searchable docs navigation
7. create content templates and review workflow

Acceptance:
- customer can self-serve common setup and support questions
- docs have owners and update cadence
- support flow is clearer than email-only

## Stage 3 — full rollout / mature docs program (2-6 weeks)
Goal: production-grade documentation program.

Tasks:
1. authenticated customer portal or help center
2. public vs authenticated docs split
3. curated OpenAPI publishing workflow from source annotations
4. docs analytics + feedback widgets
5. changelog automation from release pipeline
6. support portal integration (Zendesk/Freshdesk/Linear/Jira Service Management/etc.)
7. formal docs governance: owner, review SLA, versioning

Acceptance:
- clear self-serve + ticketing path
- customer-specific technical material protected behind auth
- public docs remain safe and polished

## Advice on public API docs without overexposure

## What should remain private
Keep private:
- full Swagger UI
- raw schema for all endpoints
- hidden/internal endpoints
- admin/backoffice endpoints
- queue/agent/operator endpoints
- tenant-specific payloads/examples
- anything revealing architecture or internal service layout beyond what customers need

## What can be made public safely
Safe public content usually includes:
- high-level API capability summary
- integration prerequisites
- auth pattern description
- lifecycle for requesting access
- curated examples for stable external endpoints
- error-handling guidance
- FAQ and support escalation

## Best pattern
Use a curated developer portal generated from an allowlist, not from the full schema.

Practical options:
1. keep `/api/docs` fully gated
2. create a public markdown/docs site from hand-selected pages
3. optionally generate a **public OpenAPI subset** for only approved external endpoints
4. provide full Swagger only to approved customers/partners behind auth or network restriction

This gives you:
- compliance-friendly public docs
- lower accidental disclosure risk
- cleaner customer experience than raw Swagger

## Suggested templates / scaffold

## Good first scaffold shape
Use a docs framework that supports:
- markdown docs
- left-nav hierarchy
- search
- versioning later
- easy embedding into current site or subdomain

Practical choices:
- Mintlify — fast for API/product docs, polished out of the box
- Docusaurus — flexible, good if you want docs-as-code in repo
- Nextra — good if the marketing site is already Next.js-based
- Fern / Scalar / Redocly combo — if you later want stronger API-doc workflow

## Recommended initial template sections
- Overview
- Getting Started
- Authentication & Access
- Core Workflows / Use Cases
- API Overview
- FAQ
- Troubleshooting
- Support
- Release Notes
- Security & Compliance

## Suggested quick-win content pack
Build the first content pack from:
- product overview from `valiancehealth.com`
- onboarding steps from the Slack guide
- FAQ + support text from `sunway-docs.md`
- workflow explanations from `agent-app-guide.md`
- curated API examples from existing external-safe endpoints

## Files / systems likely to change in implementation
Depending on chosen host approach:
- website repo / CMS powering `valiancehealth.com`
- possibly `healthproximate-v3` if docs are embedded there
- markdown docs source repo or `/docs` directory
- Vanta `product-documentation` document links/uploads
- support email alias / form destination config

## Open questions
1. Which codebase powers `valiancehealth.com` today?
2. Do you want docs under the main domain (`/docs`) or a subdomain (`docs.`)?
3. Which support email alias should be public?
4. Which API endpoints are explicitly safe to publish publicly?
5. Can the Slack guide be exported into markdown or PDF?
6. Do you want stage 1 to be static pages only, or include a basic support form?

## Recommended next move
Best immediate move:
1. decide docs host (`/docs` on main domain is simplest)
2. export the Slack guide
3. create the stage-1 sitemap and page skeletons
4. populate them from repo docs
5. publish and attach to Vanta

## Validation / evidence checklist
Before claiming Vanta-ready, verify:
- docs URL loads publicly without auth
- FAQ URL loads publicly
- support URL loads publicly
- onboarding/getting-started URL loads publicly
- API overview URL loads publicly
- release notes/update page loads publicly
- Vanta `product-documentation` has either public links or screenshots/uploads attached
- support contact path is visible on the docs site

# HealthProximate Public Docs — Mintlify Stage 1 Starter Pack

This directory is a **draft starter content pack** for the public HealthProximate
documentation site, built with [Mintlify](https://mintlify.com). It implements
**Stage 1** of the documentation compliance plan: a credible, public, auditor- and
customer-friendly documentation footprint.

> **Status: draft.** This is starter content, not a production deployment. It is not
> wired into hosting, CI, or the marketing site yet. Review and approve before
> publishing externally.

## Why this exists

The plans under `.hermes/plans/` call for a public documentation surface that satisfies
the Vanta `product-documentation` requirement (service description, customer
documentation, and a visible support path) while keeping the full internal API
reference (`/api/docs`) private behind the existing Tailscale/WAF gating.

This pack is the "Stage 1 starter content set" those plans identify as the next
artifact to produce.

## Source plans

- `.hermes/plans/2026-06-26-product-documentation-compliance-plan.md`
- `.hermes/plans/2026-06-26-mintlify-public-docs-ia.md`
- `.hermes/plans/2026-06-26-mintlify-implementation-plan.md`

## Source material mined for content

- `healthproximate/docs/agent-app-guide.md` — the five core workflows and verified
  enum values (analytics/predictions metrics, view types, gender, age, secondary
  conditions).
- `healthproximate/docs/api/sunway-docs.md` — secure upload API, FAQ/support seed, and
  the customer-facing support contact.
- `healthproximate/docs/api/agent-api-guide.md` — conversational/analytical query
  (agent chat) capabilities at a high level.
- `healthproximate/docs/api/multipart-upload-guide.md` — large-file upload capability
  and the support contact.

## File tree

```text
mintlify-stage1/
  docs.json                       # Mintlify site config + navigation
  index.mdx                       # Docs landing page
  getting-started/
    index.mdx                     # Onboarding overview
    onboarding-checklist.mdx      # Practical setup checklist
    first-steps.mdx               # How to choose a workflow
  workflows/
    entity-resolver.mdx
    dashboard.mdx
    analytics.mdx
    predictions.mdx
    simulation.mdx
  api/
    overview.mdx                  # Public API overview (curated, high-level)
  faq.mdx
  support.mdx
  release-notes/
    index.mdx
  README.md                       # This file
```

## About `docs.json`

`docs.json` is the **current Mintlify configuration format** (it superseded the older
`mint.json`). The config here uses the `docs.json` schema and `$schema` pointer. If the
deploying Mintlify version still expects `mint.json`, the same structure can be ported
with minimal changes.

## Conventions used

- Every page has Mintlify frontmatter (`title`, `description`).
- Workflow pages follow one consistent structure: **overview, when to use, inputs,
  steps, outputs, notes/caveats, support**.
- Mintlify components (`Card`, `Steps`, `Accordion`, `ParamField`, callouts) are used
  for a polished feel.
- `{/* TODO ... */}` MDX comments mark where exact business/process details (SLAs,
  onboarding sign-offs, the public OpenAPI subset) still need to be confirmed. They do
  not render on the published page.

## Public / private boundary (important)

This content was deliberately written for a **public** audience:

- **Included:** product concepts, UI workflows, customer-relevant verified enums
  (metrics, view types, demographics), a high-level API model, the secure upload
  request shape (already publicly documented), and the support path.
- **Excluded:** the full API schema / Swagger, internal and administrative endpoints,
  internal file paths and serializer/view names, tenant-specific organization names and
  examples, in-process/internal agent implementation details, and any low-level schema
  that would widen the attack surface without customer benefit.

The [API Overview](api/overview.mdx) explicitly states that detailed and restricted
implementation references are available only through controlled access channels.

## Verified values embedded (per the brief)

- **Analytics metrics:** `revenue`, `hospital_revenue`, `profit`, `margin`, `cost`,
  `discount`, `los`, `time`, `readmission_30`
- **Analytics view types:** `detail`, `avg`, `sum`
- **Predictions metrics:** `price`, `cost`, `time`, `profit`
- **Predictions gender:** `M`, `F`, or unknown/blank
- **Predictions age:** numeric `0`–`120`, or legacy age bands
- **Predictions secondary conditions:** OMOP concept IDs (not a fixed enum)
- **Simulation:** new/unseen item estimation is explicitly noted as **not** supported.

## Support contact

The customer-facing support address used throughout
(**admin@valiancehealth.ai**) is taken from the existing upload API docs
(`sunway-docs.md`, `multipart-upload-guide.md`). Note: `sunway-docs.md` also mentions
`support@healthproximate.com` in one FAQ answer, but its canonical Support section uses
`admin@valiancehealth.ai`, so that is the address standardized on here. Confirm the
preferred public alias before launch.

## How to use this draft

1. **Review** every page for accuracy and public-safety with product and security owners.
2. **Resolve** the `{/* TODO */}` items (SLAs, onboarding sign-offs, public API subset).
3. **Preview locally** with the Mintlify CLI (e.g. `npx mint dev` from this directory)
   to confirm navigation and rendering.
4. **Decide hosting** — `valiancehealth.com/docs` vs `docs.valiancehealth.com` — and
   move/deploy the approved content to the chosen docs repo/location.
5. **Capture evidence** (public URLs + screenshots) and attach to the Vanta
   `product-documentation` document.

## Validation status

These files have **not** been built or rendered by the Mintlify CLI in this
environment (the CLI is not installed here). They are authored to the documented
Mintlify `docs.json`/MDX conventions. Run a local `mint dev` preview as part of review.

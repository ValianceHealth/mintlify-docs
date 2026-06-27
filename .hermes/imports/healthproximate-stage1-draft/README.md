# Imported: HealthProximate Stage 1 Docs Draft (operator note)

This directory holds the **imported Stage 1 starter content pack** for the public
HealthProximate Mintlify documentation site. It was brought into this repo as a
review-friendly import — it is staged content, **not** part of the live site yet.

## What this is

- A copy of the `mintlify-stage1` draft produced during planning (originally authored
  under the planning repo's `.hermes/drafts/mintlify-stage1`).
- The draft's own original README has been preserved here as
  [`DRAFT-OVERVIEW.md`](DRAFT-OVERVIEW.md) — read it for the full description of the
  draft's scope, sources, conventions, verified enum values, and public/private
  boundary. This file (`README.md`) is only the operator note about the import itself.
- The matching planning documents are imported alongside this draft under
  [`../../plans/`](../../plans/):
  - `2026-06-26-product-documentation-compliance-plan.md`
  - `2026-06-26-mintlify-public-docs-ia.md`
  - `2026-06-26-mintlify-implementation-plan.md`

## What this is NOT (current status)

- **Not integrated** into the repo root Mintlify site. The root `docs.json`,
  `index.mdx`, and `quickstart.mdx` were intentionally left untouched by this import.
- **Not deployed, built, or validated** by the Mintlify CLI in this environment.
- The `docs.json` inside this directory is the **draft's** standalone config — it is a
  reference for the intended navigation, not the live site configuration.

Treat everything under `healthproximate-stage1-draft/` as source material to be mapped
into the live docs, not as already-published pages.

## Next steps (to integrate)

1. **Review** every page for accuracy and public-safety with product and security
   owners; resolve the `{/* TODO */}` markers in the MDX files.
2. **Map content into live docs pages**: move/adapt the pages under
   `getting-started/`, `workflows/`, `api/`, plus `faq.mdx`, `support.mdx`, and
   `release-notes/` into the repo root docs structure.
3. **Merge navigation into root `docs.json`**: fold the draft's navigation groups into
   the live `docs.json` rather than replacing it.
4. **Preview locally** with the Mintlify CLI (`npx mint dev` from the repo root) to
   confirm navigation and rendering before publishing.
5. **Capture evidence** (public URLs + screenshots) for the Vanta
   `product-documentation` requirement once the content is live.

See `DRAFT-OVERVIEW.md` for the detailed how-to-use guidance from the original authors.

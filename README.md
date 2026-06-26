# HealthProximate Documentation

Public product documentation and help center for **HealthProximate** by **Valiance Health** — the healthcare cost, revenue, and operations analytics platform. This site is built with [Mintlify](https://mintlify.com).

This repository contains the **Stage 1** public documentation footprint: a credible, public, auditor- and customer-friendly documentation surface (service description, customer-facing workflow guides, a public API overview, FAQ, and a visible support path). The full internal API reference remains private behind controlled access.

## Structure

- `docs.json` — site configuration and navigation
- `index.mdx` — documentation landing page
- `getting-started/` — onboarding overview, checklist, and first steps
- `workflows/` — the five core workflows: entity resolver, dashboard, analytics, predictions, simulation
- `api/overview.mdx` — public API overview and the public/private documentation boundary
- `faq.mdx`, `support.mdx` — help center
- `release-notes/` — what's current
- `.hermes/` — planning artifacts and the imported Stage 1 source draft (not published)

## Public / private boundary

This site is intended for a **public** audience. It deliberately excludes the full API schema, internal/administrative endpoints, tenant-specific details, internal file paths, and secrets. Detailed implementation references remain access-controlled. See `api/overview.mdx` for how this is communicated to readers.

## Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mint) to preview documentation changes locally:

```
npm i -g mint
```

Run the following command at the root of the repository, where `docs.json` is located:

```
mint dev
```

View the local preview at `http://localhost:3000`.

## Troubleshooting

- If the dev environment isn't running: run `mint update` to ensure you have the most recent CLI.
- If a page loads as a 404: make sure you are running in a folder with a valid `docs.json`.

## Resources

- [Mintlify documentation](https://mintlify.com/docs)
- [Valiance Health](https://valiancehealth.com)

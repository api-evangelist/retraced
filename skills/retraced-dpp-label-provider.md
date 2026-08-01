---
name: Retrieve Digital Product Passport data (DPP / label provider)
description: Fetch product, supply-chain, certificate, and material-composition data to build a Digital Product Passport or QR label.
api: openapi/retraced-openapi-original.json
operations:
  - GET /api/v2/styles/{id}
  - GET /api/v2/supply-chains/{id}
  - GET /api/v2/certificates/
  - GET /api/v2/certificates/{id}
  - GET /api/v2/material-headers/
  - GET /api/v2/companies/{id}/esg/
---

# Digital Product Passport / label provider

Use this skill as a DPP or label integrator to assemble the data behind a product passport.

## Auth
Header `companyapikey: <your key>`. Base URL `https://publicapi.retraced.com/api/v2`.

## Steps
1. **Resolve the product** — `GET /api/v2/styles/{id}` for the style identity and codes.
2. **Pull the supply chain** — `GET /api/v2/supply-chains/{id}` for multi-tier structure (fiber to finish).
3. **Look up certificates** — `GET /api/v2/certificates/` (filterable) and `GET /api/v2/certificates/{id}`
   for certified-materials validation.
4. **Get material composition** — `GET /api/v2/material-headers/` and its lines for percentages
   and countries of origin.
5. **Company ESG (optional)** — `GET /api/v2/companies/{id}/esg/` for energy-source / ESG data (ESG 2.1.6.1).

## Rules
- Read-only flow: all GET; safe for connected/read agent access (see agentic-access/retraced-agentic-access.yml).
- Use `page`/`limit`/`include` on list endpoints.
- Errors use the custom JSON envelope — see errors/retraced-problem-types.yml.

---
name: Manage products (styles) in Retraced
description: Create, update, query, and archive products via the unified Retraced /styles endpoint.
api: openapi/retraced-openapi-original.json
operations:
  - POST /api/v2/styles/
  - GET /api/v2/styles/
  - GET /api/v2/styles/{id}
  - PUT /api/v2/styles/{id}
  - POST /api/v2/styles/archive
  - POST /api/v2/styles/unarchive
  - GET /api/v2/style-types/
  - POST /api/v2/style-properties/
---

# Manage products (styles)

Use this skill to manage products (called *styles*) in the Retraced Public API v2.

## Auth
Send every request with header `companyapikey: <your key>` (create keys in the Retraced
Platform under Developers HQ > API Keys). Base URL `https://publicapi.retraced.com/api/v2`
(use `https://publicapi.staging.retraced.com` for testing).

## Steps
1. **List style types** — `GET /api/v2/style-types/` to find the `styleTypeId` your product should use.
2. **Create the product** — `POST /api/v2/styles/` with the product body (reference the `styleTypeId`).
3. **Query products** — `GET /api/v2/styles/` with `page`/`limit`/`sort`/`order` plus filters
   (e.g. `name`, `codeId`, `brands`, `suppliers`, `isArchived`, `include`). Fetch one with
   `GET /api/v2/styles/{id}`.
4. **Update** — `PUT /api/v2/styles/{id}` with the full updated body.
5. **Archive / unarchive** — `POST /api/v2/styles/archive` or `.../unarchive` (soft state, not delete).

## Rules
- Pagination is page-number based (`page`, `limit`, `order`, `sort`) — see conventions/retraced-conventions.yml.
- No idempotency key is supported; do not retry non-GET calls blindly.
- Errors return a custom JSON envelope `{statusCode, code, message, ...}` — see errors/retraced-problem-types.yml.

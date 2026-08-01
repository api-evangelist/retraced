---
name: Manage orders in Retraced Order Hub
description: Create and manage purchase/sales orders and their line items in the Retraced Order Hub.
api: openapi/retraced-openapi-original.json
operations:
  - POST /api/v2/orders/
  - GET /api/v2/orders/
  - GET /api/v2/orders/{id}
  - PATCH /api/v2/orders/{id}
  - DELETE /api/v2/orders/{id}
  - GET /api/v2/order-lines/
  - GET /api/v2/order-lines/{lineId}
  - GET /api/v2/attachment-templates/
---

# Manage orders (Order Hub)

Use this skill to manage purchase/sales orders and their lines.

## Auth
Header `companyapikey: <your key>`. Base URL `https://publicapi.retraced.com/api/v2`.

## Steps
1. **Create an order** — `POST /api/v2/orders/` with the order header body.
2. **List / fetch** — `GET /api/v2/orders/` (with `page`/`limit`/filters) or `GET /api/v2/orders/{id}`.
3. **Update** — `PATCH /api/v2/orders/{id}` for partial changes.
4. **Read lines** — `GET /api/v2/order-lines/` (filter by order) and `GET /api/v2/order-lines/{lineId}`;
   line numbers are auto-generated.
5. **Delete** — `DELETE /api/v2/orders/{id}` (respect soft- vs hard-delete semantics from the Orders guide).
6. **Attachment templates** — `GET /api/v2/attachment-templates/` for available attachment templates.

## Rules
- No idempotency support — avoid blind retries on POST/PATCH/DELETE.
- Errors return the custom JSON envelope — see errors/retraced-problem-types.yml.
- See the Orders & Order Lines guide: https://publicapi.retraced.com/api/v2/guides

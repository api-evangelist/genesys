---
name: Inspect routing queues and members
description: List Genesys Cloud routing queues and the agents assigned to a queue.
api: openapi/genesys-platform-api-openapi-original.json
operations: [getRoutingQueues, getRoutingQueue, getRoutingQueueMembers]
---

# Inspect routing queues and members (Genesys Cloud)

## Auth
- OAuth 2 Bearer token against the regional base host (`https://api.mypurecloud.com`).
- Required scopes: `routing:readonly` (or `routing`).

## Steps
1. `getRoutingQueues` — `GET /api/v2/routing/queues` to list queues.
   Page with `pageNumber` / `pageSize`; read `entities`, `total`, `pageCount`.
2. `getRoutingQueue` — `GET /api/v2/routing/queues/{queueId}` for a single queue's configuration.
3. `getRoutingQueueMembers` — `GET /api/v2/routing/queues/{queueId}/members` to list assigned agents.

## Rules
- Page-number pagination: response carries `entities`, `pageSize`, `pageNumber`, `total`, `pageCount`.
- On `429`, honor `Retry-After`.
- Log the `ININ-Correlation-Id` header for traceability.

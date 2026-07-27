---
name: Query conversation analytics
description: Authenticate to Genesys Cloud and query conversation detail and aggregate analytics.
api: openapi/genesys-platform-api-openapi-original.json
operations: [getUsersMe, postAnalyticsConversationsDetailsQuery, postAnalyticsConversationsAggregatesQuery]
---

# Query conversation analytics (Genesys Cloud)

Use the Genesys Cloud Platform API to pull contact-center conversation metrics.

## Auth
- Obtain an OAuth 2 access token from `https://login.mypurecloud.com/oauth/token`
  (client_credentials for server-to-server; authorization_code + PKCE for user context).
- Send `Authorization: Bearer <token>` on every request against the regional base host
  (e.g. `https://api.mypurecloud.com`).
- Required scopes: `analytics:readonly` (or `analytics`).

## Steps
1. `getUsersMe` — `GET /api/v2/users/me` to confirm the token resolves and note the org region.
2. `postAnalyticsConversationsDetailsQuery` — `POST /api/v2/analytics/conversations/details/query`
   with an `interval` and optional segment/media filters to retrieve conversation detail records.
   Page with `paging.pageSize` / `paging.pageNumber`.
3. `postAnalyticsConversationsAggregatesQuery` — `POST /api/v2/analytics/conversations/aggregates/query`
   with `interval`, `groupBy`, and `metrics` to retrieve aggregated metrics (e.g. tHandle, nOffered).

## Rules
- Respect rate limits: on `429`, honor the `Retry-After` header.
- Capture the `ININ-Correlation-Id` response header for support/tracing.
- Errors return a JSON envelope with `status`, `code`, `message`, `contextId`.

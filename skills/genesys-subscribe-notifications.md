---
name: Subscribe to real-time notifications
description: Open a Genesys Cloud notifications channel and subscribe to real-time event topics.
api: openapi/genesys-platform-api-openapi-original.json
operations: [postNotificationsChannels, postNotificationsChannelSubscriptions, getNotificationsChannels]
---

# Subscribe to real-time notifications (Genesys Cloud)

Stream real-time events (conversations, presence, routing, analytics) over a websocket channel.

## Auth
- OAuth 2 Bearer token against the regional base host (`https://api.mypurecloud.com`).
- Scopes depend on the topics subscribed (e.g. `conversations`, `presence`, `routing`).

## Steps
1. `postNotificationsChannels` — `POST /api/v2/notifications/channels` to create a channel;
   the response returns a `connectUri` websocket URL. Connect a websocket client to it.
2. `postNotificationsChannelSubscriptions` — `POST /api/v2/notifications/channels/{channelId}/subscriptions`
   with a list of `{ "id": "v2.users.{userId}.conversations" }` topics to add subscriptions.
3. `getNotificationsChannels` — `GET /api/v2/notifications/channels` to review active channels.

## Rules
- Channels expire; reconnect and re-subscribe on socket close or channel expiry.
- Use `PUT /api/v2/notifications/channels/{channelId}/subscriptions` (putNotificationsChannelSubscriptions)
  to replace the full subscription set.
- Available topics are listed at developer.genesys.cloud/notificationsalerts/notifications/available-topics.
- On `429`, honor `Retry-After`; errors carry a `contextId` in the JSON envelope.

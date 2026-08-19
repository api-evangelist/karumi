---
name: Review demo sessions and read a transcript
description: List a Karumi organization's demo sessions with filters, then open one session and read its full transcript.
api: openapi/karumi-public-api-openapi.json
operations:
  - list_sessions_sessions_get
  - get_session_sessions__session_id__get
generated: '2026-08-13'
method: generated
source: openapi/karumi-public-api-openapi.json
---

# Review demo sessions and read a transcript

Karumi's Public API is read-only. This skill covers the two operations that do the work.

## Authentication

Send the organization API key on every request:

```
X-Api-Key: <KARUMI_API_KEY>
```

The OpenAPI does **not** declare a `securitySchemes` entry — the key is modelled as an
optional `x-api-key` header parameter — but the server enforces it. Without the header the
API returns `401 {"detail": "Missing X-Api-Key header"}`. Keys are minted and revoked from
the Karumi workspace, or with the `create_api_key` / `revoke_api_key` MCP tools.

Base URL: `https://api.karumi.ai/api/v1`

## Steps

1. **List sessions** — `list_sessions_sessions_get` (`GET /sessions`).
   Optional query filters: `project_id` (uuid), `status`, `start_date` and `end_date`
   (RFC 3339 date-times). Paginate with `limit` (1..500, default 100) and `offset`
   (default 0).
   The response is `PaginatedSessions`: `items`, `total`, `limit`, `offset`. Use `total`
   to decide whether to page; there is no cursor and no `Link` header, so increment
   `offset` by `limit` until `offset + len(items) >= total`.
   Each `PublicSession` carries `id`, `project_id`, `status`, `created_at`,
   `duration_seconds`, `email`, `summary`, `intent_rate`, `intent_name`, `goals`, and the
   free-form `labels`, `metadata` and `tracked_journeys` objects.

2. **Open one session** — `get_session_sessions__session_id__get`
   (`GET /sessions/{session_id}`), passing the `id` from step 1.
   The response is `PublicSessionWithMessages`: everything in `PublicSession` plus
   `messages[]` (`PublicTranscriptMessage`: `id`, `speaker`, `content`, `created_at`) and
   `recording_url`.

3. **Read the transcript** — iterate `messages` in `created_at` order. `speaker`
   distinguishes the prospect from the demo agent.

## Rules

- Never widen a date window to "get more data" without saying so — `start_date`/`end_date`
  are the only way a caller controls scope, and sessions contain prospect email addresses
  and verbatim conversation content.
- `email` on a session and `visitor_email` on an event are personal data. Do not copy them
  into summaries, tickets or CRM notes unless the user explicitly asked for identified
  output.
- Do not assume `project_id` and a target's `id` are the same value. `PublicTarget` has
  **both** `id` (string) and `project_id` (uuid); the session filter takes `project_id`.
- `labels`, `metadata` and `tracked_journeys` are untyped free-form objects. Read them
  defensively; the contract guarantees nothing about their shape.

## Errors

- `401 {"detail": "Missing X-Api-Key header"}` — the key header is missing or invalid. Do
  not retry without fixing the credential.
- `422 {"detail": [{"loc": [...], "msg": "...", "type": "..."}]}` — a parameter failed
  validation. `detail` is an **array** here and a **string** on other errors, so type-check
  it before reading. Common causes: a non-UUID `project_id` or `session_id`, a malformed
  `start_date`/`end_date`, or `limit` outside 1..500.
- `404 {"detail": "Not Found"}` — no such session in this organization.
- Karumi publishes no rate limits and returns no `RateLimit-*` or `Retry-After` headers.
  Back off conservatively on your own schedule; there is no runtime signal to read.

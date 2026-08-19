---
name: Pull session insights, events and recordings
description: For a Karumi demo session, retrieve the derived insights with their evidence, the meeting event stream, and the session recording.
api: openapi/karumi-public-api-openapi.json
operations:
  - get_session_insights_sessions__session_id__insights_get
  - list_meeting_events_sessions_meeting_events_get
  - download_session_recording_sessions__session_id__recording_get
generated: '2026-08-13'
method: generated
source: openapi/karumi-public-api-openapi.json
---

# Pull session insights, events and recordings

Base URL `https://api.karumi.ai/api/v1`. Every request needs `X-Api-Key: <KARUMI_API_KEY>`.
Start from a `session_id` obtained with `list_sessions_sessions_get`.

## Steps

1. **Get the insights** — `get_session_insights_sessions__session_id__insights_get`
   (`GET /sessions/{session_id}/insights`). Returns `PublicSessionInsights`, a set of
   `PublicInsight` objects: `key` (the stable identifier), `name`, `category`, `status`,
   `confidence` (number, nullable), `value` (free-form object), `summary`, and `evidence[]`
   (`PublicInsightEvidence`).

2. **Get the event stream** — `list_meeting_events_sessions_meeting_events_get`
   (`GET /sessions/meeting-events`). Returns `PaginatedSessionEvents` of
   `PublicSessionEvent`: `id`, `session_id`, `project_id`, `event_type`, `url`,
   `visitor_email`, `metadata`, `created_at`. Filter client-side on `session_id` when you
   want one session's events, and page with `limit`/`offset` as in
   `list_sessions_sessions_get`.

3. **Fetch the recording** — `download_session_recording_sessions__session_id__recording_get`
   (`GET /sessions/{session_id}/recording`). This operation downloads the recording rather
   than returning JSON. `get_session_sessions__session_id__get` also exposes
   `recording_url` on `PublicSessionWithMessages`; prefer that field when you only need to
   hand a link to a human.

## Rules

- Always report `confidence` alongside an insight. An insight with a low or null
  `confidence` is a hypothesis, not a finding, and must not be restated as fact.
- Cite `evidence` when you surface an insight. If `evidence` is empty, say so.
- `value` is an untyped object. Do not assume a shape; render what is there.
- Recordings and `visitor_email` are personal data about a named prospect. Fetch a
  recording only when the user asked for it, and do not redistribute the download.
- There is no "list insights across sessions" operation. To analyse a cohort you must loop
  session by session — page with `list_sessions_sessions_get` first, and keep the loop
  bounded, because Karumi publishes no rate limits to tell you when you are going too fast.

## Errors

- `401 {"detail": "Missing X-Api-Key header"}` — fix the credential; do not retry blind.
- `404 {"detail": "Not Found"}` — unknown `session_id`, or no recording for that session.
- `422` — validation failure; `detail` is an array of `{loc, msg, type}`.

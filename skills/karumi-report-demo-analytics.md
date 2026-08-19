---
name: Report demo engagement analytics by target
description: List Karumi targets (demo projects), pull their journeys, and report aggregate plus time-series engagement analytics.
api: openapi/karumi-public-api-openapi.json
operations:
  - list_targets_targets_get
  - get_target_targets__target_id__get
  - get_analytics_analytics_get
  - get_analytics_timeline_analytics_timeline_get
generated: '2026-08-13'
method: generated
source: openapi/karumi-public-api-openapi.json
---

# Report demo engagement analytics by target

Base URL `https://api.karumi.ai/api/v1`. Every request needs `X-Api-Key: <KARUMI_API_KEY>`.

## Vocabulary warning

What this API calls a **target** is what Karumi's MCP server and product UI call an
**agent** — a demo project. Both are keyed by `project_id`. Say "demo project" to a human
rather than picking a side.

## Steps

1. **List targets** — `list_targets_targets_get` (`GET /targets`). Each `PublicTarget` has
   `id` (string), `name`, `description`, `project_id` (uuid) and `created_at`.

2. **Expand one target** — `get_target_targets__target_id__get`
   (`GET /targets/{target_id}`). Returns `PublicTargetWithJourneys`, adding `journeys[]`
   (`PublicUserJourney`: `id`, `name`, `description`, `is_goal`, `is_tracked`, `order`).
   Journeys have no standalone collection — this is the only way to enumerate them.

3. **Pull aggregate analytics** — `get_analytics_analytics_get` (`GET /analytics`).
   Returns `PublicAnalytics`: `total_sessions`, `avg_duration_seconds`,
   `total_goals_reached`, the four `PublicAnalyticsDistribution` blocks
   (`minutes_distribution`, `rating_distribution`, `status_distribution`,
   `intent_distribution`), plus `repeat_visitors[]` and `version_comparison[]`.

4. **Pull the time series** — `get_analytics_timeline_analytics_timeline_get`
   (`GET /analytics/timeline`). Returns `PublicTimelineAnalytics` made of
   `PublicTimelineDataPoint` values. Use this, not step 3, whenever the user asks about a
   trend or a change over time.

5. **Tie it back to sessions** — join analytics to the session list with
   `list_sessions_sessions_get?project_id=<project_id>` when the user wants the underlying
   conversations behind a number.

## Rules

- Report `total_goals_reached` against the journeys where `is_goal` is true. A goal count
  is meaningless without naming which journeys were flagged as goals.
- `is_tracked` decides what appears in a session's `tracked_journeys`. An untracked journey
  produces no session-level signal, so do not report it as zero engagement — report it as
  not tracked.
- Distributions are buckets, not percentages. Do not convert to a percentage without
  stating the denominator you used.
- `avg_duration_seconds` is nullable. Say "not reported" rather than rendering 0.
- Analytics parameters (date window, project scoping) are declared per operation in the
  spec — read them from `openapi/karumi-public-api-openapi.json` rather than assuming the
  same filter names as `/sessions`.

## Errors

- `401 {"detail": "Missing X-Api-Key header"}`.
- `422` with `detail` as an array of `{loc, msg, type}` — check which parameter `loc` names.
- `404 {"detail": "Not Found"}` on an unknown `target_id`.

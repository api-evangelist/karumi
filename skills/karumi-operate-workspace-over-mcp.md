---
name: Operate a Karumi workspace over MCP
description: Connect to Karumi's hosted MCP server and operate the workspace — discover agents and sessions, search transcripts, manage audiences and journeys, and handle API keys — with the right confirmation discipline on write tools.
api: mcp/karumi-mcp.yml
operations:
  - list_organizations
  - list_agents
  - list_audiences
  - create_audience
  - update_journey_script
  - list_api_keys
  - create_api_key
  - revoke_api_key
generated: '2026-08-13'
method: generated
source: https://www.karumi.ai/mcp-documentation
---

# Operate a Karumi workspace over MCP

Karumi's MCP server is where the *write* surface lives. The Public REST API is read-only,
so anything that changes a workspace happens here.

## Connect

- Endpoint: `https://api.karumi.ai/mcp/` — this is the URL Karumi names as the `resource`
  in its own `/.well-known/oauth-protected-resource` document, and the one that answers.
- **Do not use `https://mcp.karumi.ai`.** It is the URL printed on Karumi's connector
  documentation page, but it has no DNS A record and cannot be reached (verified
  2026-08-13). If a user reports the documented connector failing to connect, this is why.
- Auth: OAuth 2.0 authorization code with explicit user consent. An unauthenticated call
  returns `401 {"error": "unauthorized"}` with
  `WWW-Authenticate: Bearer resource_metadata="https://api.karumi.ai/.well-known/oauth-protected-resource"`.
  Follow that pointer to the authorization server rather than hard-coding endpoints.
- Access is scoped to the organizations the authenticating user belongs to. There are no
  Karumi-specific OAuth scopes — the token is all-or-nothing across the 37 tools.

## Orient before acting

1. `list_organizations` — confirm which organization you are operating in. If the user
   belongs to several, name the one you mean in the request; never guess.
2. `list_agents` / `get_agent` — find the demo project (agent) by name; it is identified by
   a project UUID.
3. `list_audiences`, `list_journeys`, `list_start_pages`, `list_knowledge` — read the
   current state of whatever you are about to change.

## Read tools (24, no confirmation)

`list_organizations`, `list_agents`, `get_agent`, `get_agent_analytics`, `list_sessions`,
`get_session_detail`, `get_session_summaries`, `get_recording_status`, `search_transcripts`,
`semantic_search`, `list_leads`, `list_companies`, `list_audiences`, `get_audience`,
`list_journeys`, `get_journey`, `list_start_pages`, `get_start_page`, `list_knowledge`,
`list_knowledge_spaces`, `list_voices`, `list_qa_questions`, `list_qa_answers`,
`answer_question`, `list_api_keys`.

Use `search_transcripts` for an exact phrase and `semantic_search` for a theme. Neither has
a REST equivalent — this is the only way to search across conversations.

## Write and destructive tools (13, confirmation required)

`create_audience`, `update_audience`, `delete_audience`, `update_journey_script`,
`record_journey`, `update_start_page`, `duplicate_start_page`,
`update_agent_system_prompt`, `add_knowledge_file`, `update_qa_answer`, `delete_qa_answer`,
`create_api_key`, `revoke_api_key`.

Rules for all of them:

- State the exact object (by name **and** id) and the exact change before you call. "Update
  the audience" is not a confirmation prompt; "delete audience 'LinkedIn Q3' on agent
  Acme Demo" is.
- Karumi publishes **no idempotency contract**. A retried `create_audience` or
  `duplicate_start_page` can create a duplicate. On a timeout or ambiguous failure, call the
  matching `list_*` tool to check whether the write landed before retrying — never retry
  blind.
- `update_agent_system_prompt` changes how the demo agent behaves in front of every future
  prospect. Show the current prompt, show the proposed prompt, and get explicit approval.
- `delete_audience` and `delete_qa_answer` are destructive with no documented undo.
- `create_api_key` mints a credential for the read-only Public API. Treat the returned key
  as a secret: never echo it into a transcript, a summary, a file or a message. Prefer
  `list_api_keys` to check what already exists before minting another.
- `revoke_api_key` will break any live integration using that key. Identify the key and
  confirm which integration depends on it first.

## Data handling

Sessions, transcripts, leads and companies are prospect data. Summarise in aggregate by
default; only surface names, email addresses or verbatim quotes when the user has asked for
identified output.

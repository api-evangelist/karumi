# Karumi

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Karumi is an agentic demo platform that delivers personalized, AI-powered product demonstrations during live video calls. Its AI agent runs live, interactive demos 24/7 across landing pages, in-app surfaces, and outbound email, adapting each demonstration to the prospect and navigating the product in-browser in real time. It supports multiple languages, logs transcripts, analysis, and next steps into the CRM, and targets B2B SaaS go-to-market teams looking to engage high-intent leads at peak interest instead of waiting days for a human demo. Karumi publishes a read-only Public API over session, transcript, insight, target and analytics data (OpenAPI 3.1.0, X-Api-Key auth) and a hosted, OAuth-protected MCP server exposing 37 tools for operating the platform from an MCP client. Karumi is a Y Combinator (Fall 2025) company founded by Pablo Omenaca (CEO) and Toni Lopez (CTO), both formerly of StackAI (YC W23).

**Areas:** Company · AI Agents · Product Demos · Sales Enablement · Go-To-Market · Software-as-a-Service · Conversational AI · Video · Y Combinator · MCP · Agent-Native · Analytics

## Karumi on APIs.io

Everything profiled for Karumi is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/karumi/](https://apis.io/providers/karumi/)** — or go straight to one of the APIs or properties below.

### APIs (4)

- [Karumi MCP Server](https://apis.io/apis/karumi/karumi-mcp-server/) — Hosted, remote MCP server that exposes a Karumi workspace to any MCP-compatible client. 37 published tools cover organizations, agents, sessions,…
- [Karumi Analytics API](https://apis.io/apis/karumi/karumi-analytics-api/) — The Analytics API from Karumi — 2 operation(s) for analytics.
- [Karumi Sessions API](https://apis.io/apis/karumi/karumi-sessions-api/) — The Sessions API from Karumi — 5 operation(s) for sessions.
- [Karumi Targets API](https://apis.io/apis/karumi/karumi-targets-api/) — The Targets API from Karumi — 2 operation(s) for targets.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [karumi](https://apis.io/servers/karumi/karumi/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Karumi Agentic Access](https://apis.io/agentic-access/karumi/karumi-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Karumi Public Api Overlay](https://apis.io/overlays/karumi/karumi-public-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Karumi Authentication](https://apis.io/security/karumi/karumi-authentication/)
- [Karumi Domain Security](https://apis.io/security/karumi/karumi-domain-security/)
- [Karumi Trust Center](https://apis.io/security/karumi/karumi-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Karumi Scopes](https://apis.io/scopes/karumi/karumi-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Karumi Plans Pricing](https://apis.io/plans/karumi/karumi-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Karumi Rate Limits](https://apis.io/rate-limits/karumi/karumi-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.karumi.ai/)
- [Documentation](https://api.karumi.ai/api/v1/docs)
- [API reference](https://api.karumi.ai/api/v1/redoc)
- [Pricing](https://www.karumi.ai/pricing)
- [Sign up](https://app.karumi.ai/)
- [Blog](https://www.karumi.ai/blog)
- [Compliance](https://trust.delve.co/karumi)
- [Terms of service](https://www.karumi.ai/terms)
- [Privacy policy](https://www.karumi.ai/privacy)

## API Evangelist rating

**Kin Score 43.1** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 68.3 |
| Contract quality | 43.5 |
| Contract governance | 4.5 |
| Operational transparency | 0.0 |
| Developer ergonomics | 32.7 |
| Access clarity | 77.6 |

**Agent readiness 60.0** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | na |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | na |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | na |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 36.8** — AI & Biometrics

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/karumi/](https://apis.io/providers/karumi/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Karumi: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/karumi/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).

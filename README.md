# Light

Light is an agentic accounting and financial-operations platform positioned as an alternative to
traditional ERPs and fragmented finance stacks — a multi-entity general ledger and consolidation
engine with accounts payable, accounts receivable, spend management and corporate cards,
contracts and subscription billing, purchase orders and expense reimbursement.

Backed by: balderton-capital, seedcamp — https://light.inc/

## API

- **Developer docs**: https://docs.light.inc/getting-started/introduction
- **Base URL**: https://api.light.inc
- **Spec**: OpenAPI 3.0.1 — 183 operations, 136 paths, 226 schemas, 28 resource groups
- **Auth**: API key as HTTP Basic (`Authorization: Basic <key>`) or OAuth 2.0 bearer JWT
  (authorization-code flow, Auth0-backed, refresh-token rotation)
- **Rate limits**: 300 req/min per key or token; 100,000 req/day per organization
- **Idempotency**: `X-Idempotency-Key` header on 14 write operations
- **Pagination**: `cursor` + `limit` (or `offset`), with a `field:operator:value` filter grammar

## Artifacts

| Artifact | Method |
|---|---|
| `openapi/` | searched — `docs.light.inc/openapi-public.json` |
| `llms/` | searched — verbatim `docs.light.inc/llms.txt` |
| `mcp/` | searched — live MCP server verified at `docs.light.inc/mcp` |
| `authentication/` | searched — docs publish an OAuth 2.0 flow the spec omits |
| `conventions/` | searched — idempotency, pagination, filtering, error envelope, uploads |
| `rate-limits/` | searched |
| `errors/` | searched — custom envelope (not RFC 9457) + live-probed variant |
| `lifecycle/` | searched — versioning + the one deprecated operation |
| `conformance/` | searched — standards posture + published compliance program |
| `security/` | probed — domain security, trust/compliance surface |
| `well-known/` | probed — verified absence, all paths 404 |
| `data-model/` | derived — 26 entities and their relationship graph |
| `overlays/` | generated — adds the missing `servers[]`, OAuth scheme, runtime semantics |
| `skills/` | generated — 4 Agent Skills grounded in verified operationIds |
| `agentic-access/` | generated — `x-agentic-access` contracts for 183 operations |

## Notable gaps

No status page, changelog, deprecation policy or SLA. No `/.well-known/` documents (including
no `security.txt` and no RFC 8414 metadata despite operating OAuth). No published SDKs, CLI,
GitHub organization or Postman collection. No webhook or event surface. The published OpenAPI
declares no `servers[]` and models 179 of 183 responses as a bare `default`.

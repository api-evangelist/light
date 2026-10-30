# Light

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

Light is an agentic accounting and financial-operations platform positioned as an alternative to traditional ERPs and fragmented finance stacks. It combines a multi-entity general ledger and consolidation engine with accounts payable, accounts receivable, spend management and corporate cards, contracts and subscription billing, purchase orders and expense reimbursement. The Light API is a REST API over HTTPS returning camelCase JSON, covering 183 operations across 28 resource groups — invoice payables and receivables, credit notes, customer credits, journal entries, ledger accounts, bank accounts and transactions, cards and card transactions, contracts, purchase orders, products, vendors, customers and users. Authentication is either an API key sent as HTTP Basic or an OAuth 2.0 access token, access is governed by the same roles as user accounts, and writes on 14 operations accept an X-Idempotency-Key header. Light also publishes a live Model Context Protocol server over its documentation and markets a Claude MCP integration against the live ledger.

**Areas:** Accounting · Finance · ERP · Accounts Payable · Accounts Receivable · General Ledger · Spend Management · Invoicing · Corporate Cards · Expense Management · Financial Operations · Agents

## Light on APIs.io

Everything profiled for Light is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/light/](https://apis.io/providers/light/)** — or go straight to one of the APIs or properties below.

### APIs (28)

- [Light Authorization API](https://apis.io/apis/light/light-authorization-api/) — The Authorization API from Light — 2 operation(s) for authorization.
- [Light v1 - Accounting Documents API](https://apis.io/apis/light/light-v1-accounting-documents-api/) — The v1 - Accounting Documents API from Light — 1 operation(s) for v1 - accounting documents.
- [Light v1 - Attachments API](https://apis.io/apis/light/light-v1-attachments-api/) — The v1 - Attachments API from Light — 4 operation(s) for v1 - attachments.
- [Light v1 - Bank Accounts API](https://apis.io/apis/light/light-v1-bank-accounts-api/) — The v1 - Bank Accounts API from Light — 4 operation(s) for v1 - bank accounts.
- [Light v1 - Card Balance Accounts API](https://apis.io/apis/light/light-v1-card-balance-accounts-api/) — The v1 - Card Balance Accounts API from Light — 4 operation(s) for v1 - card balance accounts.
- [Light v1 - Card Customers API](https://apis.io/apis/light/light-v1-card-customers-api/) — The v1 - Card Customers API from Light — 1 operation(s) for v1 - card customers.
- [Light v1 - Card Transactions API](https://apis.io/apis/light/light-v1-card-transactions-api/) — The v1 - Card Transactions API from Light — 9 operation(s) for v1 - card transactions.
- [Light v1 - Cards API](https://apis.io/apis/light/light-v1-cards-api/) — The v1 - Cards API from Light — 4 operation(s) for v1 - cards.
- [Light v1 - Companies API](https://apis.io/apis/light/light-v1-companies-api/) — The v1 - Companies API from Light — 1 operation(s) for v1 - companies.
- [Light v1 - Contracts API](https://apis.io/apis/light/light-v1-contracts-api/) — The v1 - Contracts API from Light — 10 operation(s) for v1 - contracts.
- [Light v1 - Credit Notes API](https://apis.io/apis/light/light-v1-credit-notes-api/) — The v1 - Credit Notes API from Light — 10 operation(s) for v1 - credit notes.
- [Light v1 - Custom Properties API](https://apis.io/apis/light/light-v1-custom-properties-api/) — The v1 - Custom Properties API from Light — 4 operation(s) for v1 - custom properties.
- [Light v1 - Customer Credits API](https://apis.io/apis/light/light-v1-customer-credits-api/) — The v1 - Customer Credits API from Light — 12 operation(s) for v1 - customer credits.
- [Light v1 - Customers API](https://apis.io/apis/light/light-v1-customers-api/) — The v1 - Customers API from Light — 4 operation(s) for v1 - customers.
- [Light v1 - Entities API](https://apis.io/apis/light/light-v1-entities-api/) — The v1 - Entities API from Light — 1 operation(s) for v1 - entities.
- [Light v1 - Exchange API](https://apis.io/apis/light/light-v1-exchange-api/) — The v1 - Exchange API from Light — 2 operation(s) for v1 - exchange.
- [Light v1 - Expenses API](https://apis.io/apis/light/light-v1-expenses-api/) — The v1 - Expenses API from Light — 8 operation(s) for v1 - expenses.
- [Light v1 - Invoice Approvals API](https://apis.io/apis/light/light-v1-invoice-approvals-api/) — The v1 - Invoice Approvals API from Light — 1 operation(s) for v1 - invoice approvals.
- [Light v1 - Invoice Payables API](https://apis.io/apis/light/light-v1-invoice-payables-api/) — The v1 - Invoice Payables API from Light — 17 operation(s) for v1 - invoice payables.
- [Light v1 - Invoice Receivables API](https://apis.io/apis/light/light-v1-invoice-receivables-api/) — The v1 - Invoice Receivables API from Light — 11 operation(s) for v1 - invoice receivables.
- [Light v1 - Journal Entries API](https://apis.io/apis/light/light-v1-journal-entries-api/) — The v1 - Journal Entries API from Light — 3 operation(s) for v1 - journal entries.
- [Light v1 - Ledger accounts API](https://apis.io/apis/light/light-v1-ledger-accounts-api/) — The v1 - Ledger accounts API from Light — 1 operation(s) for v1 - ledger accounts.
- [Light v1 - Ledger Transactions API](https://apis.io/apis/light/light-v1-ledger-transactions-api/) — The v1 - Ledger Transactions API from Light — 1 operation(s) for v1 - ledger transactions.
- [Light v1 - Products API](https://apis.io/apis/light/light-v1-products-api/) — The v1 - Products API from Light — 3 operation(s) for v1 - products.
- [Light v1 - Purchase Orders API](https://apis.io/apis/light/light-v1-purchase-orders-api/) — The v1 - Purchase Orders API from Light — 9 operation(s) for v1 - purchase orders.
- [Light v1 - User Comments API](https://apis.io/apis/light/light-v1-user-comments-api/) — The v1 - User Comments API from Light — 2 operation(s) for v1 - user comments.
- [Light v1 - Users API](https://apis.io/apis/light/light-v1-users-api/) — The v1 - Users API from Light — 5 operation(s) for v1 - users.
- [Light v1 - Vendors API](https://apis.io/apis/light/light-v1-vendors-api/) — The v1 - Vendors API from Light — 2 operation(s) for v1 - vendors.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Light API documentation](https://apis.io/servers/light/light-api-documentation/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Light Agentic Access](https://apis.io/agentic-access/light/light-agentic-access/)

#### Collections (28)

Postman and Open Collection request collections.

- [Light Authorization API](https://apis.io/collections/light/open-light-authorization-api/)
- [Light Authorization v1 - Accounting Documents API](https://apis.io/collections/light/open-light-v1-accounting-documents-api/)
- [Light Authorization v1 - Attachments API](https://apis.io/collections/light/open-light-v1-attachments-api/)
- [Light Authorization v1 - Bank Accounts API](https://apis.io/collections/light/open-light-v1-bank-accounts-api/)
- [Light Authorization v1 - Card Balance Accounts API](https://apis.io/collections/light/open-light-v1-card-balance-accounts-api/)
- [Light Authorization v1 - Card Customers API](https://apis.io/collections/light/open-light-v1-card-customers-api/)
- [Light Authorization v1 - Card Transactions API](https://apis.io/collections/light/open-light-v1-card-transactions-api/)
- [Light Authorization v1 - Cards API](https://apis.io/collections/light/open-light-v1-cards-api/)
- [Light Authorization v1 - Companies API](https://apis.io/collections/light/open-light-v1-companies-api/)
- [Light Authorization v1 - Contracts API](https://apis.io/collections/light/open-light-v1-contracts-api/)
- [Light Authorization v1 - Credit Notes API](https://apis.io/collections/light/open-light-v1-credit-notes-api/)
- [Light Authorization v1 - Custom Properties API](https://apis.io/collections/light/open-light-v1-custom-properties-api/)
- [Light Authorization v1 - Customer Credits API](https://apis.io/collections/light/open-light-v1-customer-credits-api/)
- [Light Authorization v1 - Customers API](https://apis.io/collections/light/open-light-v1-customers-api/)
- [Light Authorization v1 - Entities API](https://apis.io/collections/light/open-light-v1-entities-api/)
- [Light Authorization v1 - Exchange API](https://apis.io/collections/light/open-light-v1-exchange-api/)
- [Light Authorization v1 - Expenses API](https://apis.io/collections/light/open-light-v1-expenses-api/)
- [Light Authorization v1 - Invoice Approvals API](https://apis.io/collections/light/open-light-v1-invoice-approvals-api/)
- [Light Authorization v1 - Invoice Payables API](https://apis.io/collections/light/open-light-v1-invoice-payables-api/)
- [Light Authorization v1 - Invoice Receivables API](https://apis.io/collections/light/open-light-v1-invoice-receivables-api/)
- [Light Authorization v1 - Journal Entries API](https://apis.io/collections/light/open-light-v1-journal-entries-api/)
- [Light Authorization v1 - Ledger accounts API](https://apis.io/collections/light/open-light-v1-ledger-accounts-api/)
- [Light Authorization v1 - Ledger Transactions API](https://apis.io/collections/light/open-light-v1-ledger-transactions-api/)
- [Light Authorization v1 - Products API](https://apis.io/collections/light/open-light-v1-products-api/)
- [Light Authorization v1 - Purchase Orders API](https://apis.io/collections/light/open-light-v1-purchase-orders-api/)
- …and 3 more published on APIs.io

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Light Openapi Overlay](https://apis.io/overlays/light/light-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Light Authentication](https://apis.io/security/light/light-authentication/)
- [Light Domain Security](https://apis.io/security/light/light-domain-security/)
- [Light Trust Center](https://apis.io/security/light/light-trust-center/)

#### Rate limits (1)

Published request limits.

- [Light Rate Limits](https://apis.io/rate-limits/light/light-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://light.inc/)
- [Documentation](https://docs.light.inc/getting-started/introduction)
- [Getting started](https://docs.light.inc/getting-started/introduction)
- [API reference](https://docs.light.inc/api-reference/customers/001-overview)
- [Sign up](https://light.inc/book-a-demo)
- [Support](https://light.inc/help)
- [Blog](https://light.inc/blog)
- [Compliance](https://light.inc/soc-2)
- [Terms of service](https://light.inc/terms)
- [Privacy policy](https://light.inc/privacy)

## API Evangelist rating

**Kin Score 46.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 39.7 |
| Contract governance | 18.2 |
| Operational transparency | 21.1 |
| Developer ergonomics | 58.9 |
| Access clarity | 50.0 |

**Agent readiness 36.6** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 26.8** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/light/](https://apis.io/providers/light/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Light: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/light/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).

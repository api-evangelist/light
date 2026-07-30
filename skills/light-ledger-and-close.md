---
name: Post journal entries and reconcile the ledger in Light
description: >-
  Read the Light chart of accounts, post and reverse journal entries, load bank transactions
  and reconcile balances across company entities during close.
api: openapi/light-openapi-original.json
base_url: https://api.light.inc
operations:
  - getCurrentCompany
  - getCompanyEntities
  - getLedgerAccounts
  - listLedgerTransactionLines
  - listAccountingDocuments
  - createJournalEntry
  - updateJournalEntry
  - archiveJournalEntry
  - getBankAccountsForCompany
  - createBankAccount
  - createBankTransactions
  - listBankTransactions
  - getBankAccountBalance
  - upsertBankAccountBalance
  - getRate
  - getRates
generated: '2026-07-19'
method: generated
source: openapi/light-openapi-original.json
---

# Ledger, bank reconciliation and close

## Authenticate

`Authorization: Basic YOUR_API_KEY` or `Authorization: Bearer YOUR_ACCESS_TOKEN`, over HTTPS.

## 1. Establish scope

`getCurrentCompany` returns the company for the credential. `getCompanyEntities` lists the
legal entities inside it. **Almost every posting requires a `companyEntityId`** — Light is
multi-entity and multi-book, and posting to the wrong entity is a real accounting error.
Resolve the entity explicitly; never guess or default to the first one.

## 2. Read the ledger

- `getLedgerAccounts` — the chart of accounts.
- `listLedgerTransactionLines` — paginated ledger lines; filter by `accountId` and date to
  build trial balances.
- `listAccountingDocuments` — every posted document (bills, credit notes, journal entries,
  card transactions, bank payments) in one paginated feed.

## 3. Journal entries

`createJournalEntry` and `updateJournalEntry` both accept `X-Idempotency-Key` — send one.
`updateJournalEntry` modifies **draft** entries only; only fields present in the body are
modified and fields explicitly set to `null` are cleared.

`archiveJournalEntry` (also idempotency-key aware) archives drafts directly, but for a
**posted** entry it reverses the entry and marks it archived. That reversal is a ledger write.

## 4. Bank accounts

`createBankAccount` creates the bank account **and** its linked chart-of-accounts entry in a
single transaction. The ledger account code must be a unique 6-digit integer within the
company's chart of accounts — pre-check with `getLedgerAccounts` to avoid a `CONFLICT`.

`upsertBankAccountBalance` sets the opening balance. Only one balance per bank account exists;
subsequent calls update it rather than adding another.

## 5. Load bank transactions

`createBankTransactions` inserts in batch:
- **Maximum 500 transactions per request.**
- Duplicates (same `transactionId` for the same bank account) are **silently skipped**, which
  makes the load naturally idempotent on `transactionId`. A smaller-than-expected created
  count means duplicates were filtered, not that the call failed.

Read back with `listBankTransactions` (paginated, includes the balance) and `getBankTransaction`.

## 6. Reconcile

`getBankAccountBalance` returns two numbers as of a date (`asOf`, defaulting to today):
- **bank balance** — opening balance plus all bank transactions on or before `asOf`.
- **ledger balance** — the sum of ledger transaction lines.

The difference between them is the reconciliation gap to investigate.

## 7. Multi-currency

`getRate` returns a rate between a base and target currency for a given date; `getRates`
returns rates for one currency against all available currencies. Use the transaction-date rate
for consolidation, not today's.

## Rules

- Pagination is `cursor` + `limit` (or `offset`); filter with `field:operator:value`
  (`eq, ne, in, not_in, gt, gte, lt, lte`, `|` between multi-values) and sort with
  `field:direction`.
- 300 requests/minute per key, 100,000/day per organization — a full-ledger export must be
  paced. Honour `Retry-After` on `429`.
- Errors: `{name, type, errors[]}`. `UNPROCESSABLE_CONTENT` means an accounting precondition
  failed (unbalanced entry, missing entity or currency).
- Nothing posted is ever deleted — it is reversed. Prefer the reverse/reset operations.

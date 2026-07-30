---
name: Manage cards, card spend and expense reimbursement in Light
description: >-
  Issue and freeze vendor/employee cards in Light, code and post card transactions with
  receipts, and submit employee expenses for reimbursement.
api: openapi/light-openapi-original.json
base_url: https://api.light.inc
operations:
  - listCardBalanceAccounts
  - getCardBalanceAccount
  - getCardBalanceAccountTotalSpend
  - generateCardBalanceAccountStatement
  - createCard
  - listCards
  - getCard
  - freezeCard
  - unfreezeCard
  - listCardTransactions
  - getCardTransaction
  - updateCardTransaction
  - updateCardTransactionLine
  - batchUpdateCardTransactions
  - generateUploadUrlForCardTransaction
  - postCardTransaction
  - resetCardTransaction
  - listExpenses
  - createExpenseLineItem
  - generateUploadUrl
  - submitReimbursement
generated: '2026-07-19'
method: generated
source: openapi/light-openapi-original.json
---

# Cards, card spend and expenses

## Authenticate

`Authorization: Basic YOUR_API_KEY` or `Authorization: Bearer YOUR_ACCESS_TOKEN`, over HTTPS.

## 1. Find the funding account

`listCardBalanceAccounts` then `getCardBalanceAccount` for balance detail.
`getCardBalanceAccountTotalSpend` returns total spend over a date range.
`generateCardBalanceAccountStatement` produces a period statement — it runs a fresh provider
sync inline, so it reflects the latest activity and is slower than a plain read. Dates are UTC
day boundaries and all response timestamps are UTC.

## 2. Issue a card

`createCard` accepts `X-Idempotency-Key` — **always send one.** Card issuance is a physical,
money-moving side effect and a blind retry can mint a second card.

Set metadata type `VENDOR` for vendor cards or `EMPLOYEE` for employee cards.

## 3. Freeze and unfreeze

`freezeCard` blocks transactions; `unfreezeCard` re-enables them. Both accept
`X-Idempotency-Key`. For physical cards, unfreezing also confirms the cardholder has physical
possession of the card — do not call it on the cardholder's behalf without that confirmation.

## 4. Code and post card transactions

`listCardTransactions` (paginated) and `getCardTransaction` to read.
`updateCardTransaction` and `updateCardTransactionLine` to code a single transaction;
`batchUpdateCardTransactions` to code many in one call.

Attach a receipt with `generateUploadUrlForCardTransaction`, then PUT the file to the returned
pre-signed URL. `getAttachedCardTransactionReceiptDocument` reads it back, `removeReceipt`
detaches it.

`postCardTransaction` writes the transaction to the ledger. `resetCardTransaction` reverses a
posted transaction's ledger entries and returns it to an editable state — this is the correct
way to fix a mis-coded posted transaction.

## 5. Employee expenses

`listExpenses` and `getExpense` (which includes all line items). Build an expense with
`createExpenseLineItem` / `updateExpenseLineItem` / `deleteExpenseLineItem`.
Attach a receipt via `generateUploadUrl` then PUT to the pre-signed URL;
`getAttachedDocument_1` returns the receipt as a PDF download.

`submitReimbursement` submits **all** pending expenses for the current user for administrator
review — it is not scoped to one expense. Confirm intent before calling it.
`cancelExpense` cancels an expense.

Per-user reimbursement settings live on `getUserReimbursementConfig` /
`upsertUserReimbursementConfig`; `getLatestReimbursement` returns the most recent one.

## Rules

- Cards and posting move real money. Send `X-Idempotency-Key` on `createCard`, `freezeCard`
  and `unfreezeCard`. Note that `postCardTransaction` does **not** accept it — check state
  with `getCardTransaction` before retrying.
- 300 requests/minute per key, 100,000/day per organization. Batch with
  `batchUpdateCardTransactions` rather than looping single updates.
- Errors: `{name, type, errors[]}`; `CONFLICT` typically means the transaction is already posted.
- Enum values are not exhaustive — handle unknown values gracefully.

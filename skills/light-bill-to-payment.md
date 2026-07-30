---
name: Record and pay a vendor bill in Light
description: >-
  Create a vendor invoice payable in Light with line items and a document, route it through
  approval, post it to the ledger and record payment.
api: openapi/light-openapi-original.json
base_url: https://api.light.inc
operations:
  - listVendors
  - createVendor
  - createInvoicePayableDetails
  - createInvoicePayableLineItem
  - createInvoicePayableDocumentUploadUrl
  - submitInvoicePayableForApproval
  - approveInvoicePayable
  - postInvoicePayable
  - markInvoicePayableAsPaid
  - listInvoicePayablePayments
  - reverseInvoicePayableClearing
generated: '2026-07-19'
method: generated
source: openapi/light-openapi-original.json + https://docs.light.inc/examples/create-invoice-payable
---

# Record and pay a vendor bill

Light is an accounting system of record. Every step below writes to a real general ledger, so
prefer the explicit reversal operations over retrying blindly.

## Authenticate

Send one of these on every request over HTTPS (plain HTTP fails):

- API key: `Authorization: Basic YOUR_API_KEY`
- OAuth access token: `Authorization: Bearer YOUR_ACCESS_TOKEN`

Follow redirects **and forward the Authorization header** — some endpoints redirect.
The key's roles determine what it may do; a 403 means the role is missing, not the key.

## 1. Resolve the vendor

Call `listVendors` with `searchTerm` to find an existing vendor before creating one.
Only call `createVendor` when there is no match — duplicate vendors corrupt AP reporting.

## 2. Create the bill

Call `createInvoicePayableDetails` (POST `/v1/invoice-payables`). Supply `vendorId`,
`amount`, `currency`, `invoiceNumber` and `companyEntityId`. You may pass `lineItems` inline
in this single request instead of calling `createInvoicePayableLineItem` per line.

`processingMode` selects how Light handles the document:
- `DATA_ONLY` — trust the payload as given.
- `AI_PARSE_AND_MERGE` — let Light parse the attached document and merge the result.

This operation does **not** accept `X-Idempotency-Key`. Guard against duplicates yourself by
searching `listInvoicePayables` with `filter=invoiceNumber:eq:<number>,vendorId:eq:<id>`
before creating.

## 3. Attach the source document

Call `createInvoicePayableDocumentUploadUrl` to get a short-lived pre-signed URL, then PUT the
PDF to that URL. Do not store or reuse the signed URL — request a fresh one each time.

## 4. Approve

Call `submitInvoicePayableForApproval`, then `approveInvoicePayable` (or
`declineInvoicePayable`). Check the current approval state with `getInvoicePayableApprovals`.

To skip the approval workflow entirely, call `postInvoicePayable` — it posts a bill in
`IN_DRAFT` straight to the ledger. Use this only when the caller is explicitly authorized to
bypass approvals.

## 5. Pay

Call `markInvoicePayableAsPaid` with:
- `paymentOption=FULL` to clear the remaining outstanding balance, or
- `paymentOption=PARTIAL` to record an installment.

The invoice transitions to `PAID` or `PARTIALLY_PAID`.

## 6. Reconcile and reverse

`listInvoicePayablePayments` returns every clearing against the bill — bank payments and
credit notes — each with a `type` discriminator (`BP` or `CN`) and an `accountingDocumentId`.
Reversed clearings are excluded.

To undo a payment, pass that `accountingDocumentId` and `type` to
`reverseInvoicePayableClearing`. Never attempt to "delete" a posted document.

## Rules

- **Rate limits**: 300 requests/minute per key and 100,000/day per organization. On `429`,
  wait `Retry-After` seconds and back off exponentially. Watch `X-RateLimit-Remaining`
  before batch runs.
- **Errors** come back as `{name, type, errors[{type, message, path, context}]}` — not RFC 9457.
  Read `errors[].path` to find the offending field. `CONFLICT` usually means the document is
  already posted; `UNPROCESSABLE_CONTENT` means an accounting precondition is unmet.
- **Enums are not exhaustive.** Handle unknown enum values gracefully; never match exhaustively.
- **PATCH semantics**: fields sent as `null` clear the value; omitted fields are unchanged.

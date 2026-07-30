---
name: Invoice a customer and collect cash in Light
description: >-
  Create a sales invoice in Light, open and send it, record payment, and apply a customer
  credit when the invoice must be reduced.
api: openapi/light-openapi-original.json
base_url: https://api.light.inc
operations:
  - listCustomers
  - createCustomer
  - listProducts
  - createInvoice
  - createInvoiceLine
  - openInvoiceReceivable
  - sendInvoiceReceivableEmail
  - generateInvoiceReceivableDocument
  - recordInvoicePayment
  - listInvoiceReceivablePayments
  - resetInvoiceReceivable
  - createCustomerCredit
  - postCustomerCredit
  - linkCustomerCreditToInvoice
generated: '2026-07-19'
method: generated
source: openapi/light-openapi-original.json
---

# Invoice a customer and collect cash

## Authenticate

`Authorization: Basic YOUR_API_KEY` or `Authorization: Bearer YOUR_ACCESS_TOKEN`, over HTTPS.

## 1. Resolve the customer and products

`listCustomers` with `searchTerm` first; `createCustomer` only on no match.
`createCustomer` and `updateCustomer` both accept `X-Idempotency-Key` — send a stable UUID
per logical create to make retries safe.

Use `listProducts` to resolve `productId` values for invoice lines.

## 2. Create the invoice

Call `createInvoice` (accepts `X-Idempotency-Key`) with `customerId`, `companyEntityId` and
`currency`. Add lines with `createInvoiceLine`, amend with `updateInvoiceLine`, remove with
`deleteInvoiceLine`. The invoice is editable only while in draft.

## 3. Open it

`openInvoiceReceivable` assigns the invoice number, locks the invoice for editing, and
optionally emails it or submits it to e-invoicing. The request body is optional — omit it to
open with defaults (no email sent).

To email separately afterwards, call `sendInvoiceReceivableEmail`.

## 4. Get the PDF

`generateInvoiceReceivableDocument` is asynchronous. Poll it until `status` is `READY`, then
download from the returned `url`. That signed URL is temporary — do not store and reuse it;
call the endpoint again for a fresh one.

## 5. Record payment

`recordInvoicePayment` enters a payment. If the total paid equals the invoice total the status
becomes `PAID`; otherwise `PARTIALLY_PAID`. `listInvoiceReceivablePayments` lists payments
against the invoice.

## 6. Credit the customer

To reduce what a customer owes:

1. `createCustomerCredit` (accepts `X-Idempotency-Key`), add lines with
   `createCustomerCreditLine`.
2. `postCustomerCredit` to write it to the ledger, or `postAndSendCustomerCredit` to post and
   email it in one call. `submitCustomerCreditEInvoice` submits e-invoicing for a posted credit.
3. `linkCustomerCreditToInvoice` applies it to a sales invoice.

To undo, use `unlinkCustomerCreditFromInvoice`. If the credit was already `CLEARED` or
`PARTIALLY_CLEARED`, unlinking reverses the clearing entries in the ledger.

**Do not use `unlinkCustomerCredit` — it is deprecated.** Use
`unlinkCustomerCreditFromInvoice` instead.

## 7. Undo

`resetInvoiceReceivable` returns an invoice to draft. `archiveInvoiceReceivable` and
`unarchiveInvoiceReceivable` archive and restore it.

## Rules

- 300 requests/minute per key, 100,000/day per organization; honour `Retry-After` on `429`.
- Errors: `{name, type, errors[]}` with `type` in
  `BAD_REQUEST|UNAUTHORIZED|FORBIDDEN|NOT_FOUND|CONFLICT|UNPROCESSABLE_CONTENT`.
- Enum values are not guaranteed exhaustive — degrade gracefully on unknown values.
- On PATCH, `null` clears a field and omission leaves it unchanged.

# Payment & Escrow Specification

Aligned with Pack 1: Payment states `Created → Pending → Successful → Held/Processing → Released / Refunded / Failed`; payment status is set ONLY by server-side verification/webhooks; platform fee stored on Payment.

## 0. Legal and Regulatory Warning (read first — OD-02)
Holding customers' money between payment and job completion can count as a regulated financial activity in Nigeria. Do NOT design the system so that customer funds sit in a founder's personal account or an ordinary company account. Before building the hold/release flow:
1. Ask the chosen payment provider (Paystack, Flutterwave or another CBN-licensed provider) which of their products supports delayed settlement, split payments, or escrow-style holds for marketplaces.
2. Get written advice from a Nigerian fintech/commercial lawyer on whether your design needs a licence or a licensed partner.
3. Record the decision in the Decision Log.
This document specifies the application behaviour assuming a compliant hold mechanism exists. The money-holding mechanism itself is a business/legal decision.

## 1. Payment Models (choose one for MVP)
| Option | Description | Pros | Cons |
|---|---|---|---|
| A. Provider-supported hold/split | Payment provider holds/splits funds and pays out after platform signals release | Best protection, compliant if provider supports | Depends on provider features and approval |
| B. Licensed escrow partner | Third-party escrow/wallet service | Clear compliance | Extra integration and cost |
| C. Pay on completion (no hold) | Customer pays after confirming completion | Simplest, lowest regulatory risk | Weakest provider protection; more off-platform risk |

Proposed default: pursue A; fall back to C for the first pilot if A is not approved in time. The code must isolate this behind a `PaymentGateway` service interface.

## 2. Payment Lifecycle (state machine)
| State | Meaning | Trigger |
|---|---|---|
| Created | Payment record created with server-calculated amounts | Customer clicks "Hire & pay" (`POST /payments/initialize`) |
| Pending | Customer redirected/awaiting provider confirmation | Gateway session started |
| Successful | Gateway confirmed funds received | Verified webhook / server-side verify call |
| Held/Processing | Funds held pending completion; job moves to In Progress | After Successful, under model A/B |
| Released | Net amount released to provider; fee recognised | Customer confirms completion, auto-release timer, or admin decision |
| Refunded | Funds returned (full/partial) to customer | Cancellation per policy, dispute decision |
| Failed | Gateway failed/abandoned/expired | Gateway status |

Allowed transitions only: Created→Pending→Successful→Held/Processing→(Released | Refunded); Pending→Failed; Successful→Refunded (e.g., hire cancelled before start). Any other transition is rejected and logged.

## 3. Calculations (server-side only)
- `amount` = job `agreedPrice` (NGN, stored in minor units — kobo — as integers to avoid floating-point errors).
- `platformFee` = round(amount × feeRate); feeRate from config, snapshotted at payment creation.
- `providerNet` = amount − platformFee.
- Processor charges: decide who bears them (OD-01); record in a `processorFee` field.
- Never accept amount, fee or currency from the client.

## 4. Flows
**Hire & pay**
1. Customer selects application → server creates Contract (status pending payment) and Payment (Created).
2. Server initialises gateway transaction with reference; returns the authorization URL (or checkout parameters) to the app.
3. The app opens the gateway checkout in a secure in-app browser or WebView (OD-24); the customer pays there. The app only observes the return/redirect signal for display purposes.
4. Gateway webhook hits `POST /payments/webhook`: verify signature, check amount/currency/reference match, then update to Successful (idempotently).
5. Job moves to Provider Selected/In Progress per Pack 1 states; both parties notified.

**Completion & release**
1. Provider submits completion (job: Submitted for Completion).
2. Customer confirms → job Completed → release flow.
3. If customer is silent for the auto-release window (OD-10, default 72h) and no dispute opened → auto-confirm and release.
4. Dispute opened → payment flagged, release blocked until resolution (doc 07).

**Payout**
Provider needs verified payout details (bank account with name check). Payout via gateway transfer API or settlement. Failures create a retry task and notify admin. Target payout timing: OD-14.

**Refund**
Full/partial refund through the gateway refund API by authorised admin action or by automatic policy (cancellation before start). Record who, when, why.

## 5. Webhook Requirements
- Verify provider signature header using the webhook secret; reject otherwise.
- Idempotency: store processed event IDs/references; duplicates are acknowledged (HTTP 200) without re-processing.
- Verify transaction server-side via gateway API where available before trusting payload.
- Compare amount, currency and reference with the stored Payment.
- Respond quickly; do heavy work asynchronously.
- Log every webhook with raw payload hash and outcome.

## 6. Data and Audit
Proposed schema additions to Payment: `reference` (unique), `feeRateApplied`, `processorFee`, `providerNet`, `currency` (default NGN), `heldAt`, `releasedAt`, `refundedAt`, `refundAmount`, `failureReason`, `gatewayEventIds[]`.
Add `PaymentEvent`/AuditLog entries for every state change: actor, from→to, timestamp, reason, IP/user agent where relevant.
Never store card numbers, CVV or full bank credentials. Use gateway tokens/references only.

## 7. Failure Handling
| Case | Behaviour |
|---|---|
| Customer closes page after paying | Webhook still updates; client polls `GET /payments/:id` |
| Webhook delayed | Reconciliation job verifies pending payments periodically |
| Webhook arrives before client returns | Fine; server state is authoritative |
| Amount mismatch | Mark flagged, do not progress, alert admin |
| Payout failure | Retry with backoff; admin alert; provider notified |
| Duplicate payment attempt | Unique reference per payment; block second active payment for same contract |

## 8. Reconciliation
Daily job compares internal Payment records with gateway transaction list; mismatches go to an admin review queue.

## 9. Acceptance Criteria
- Payment never becomes Successful from a frontend callback alone.
- Invalid signature webhook → rejected, logged.
- Duplicate webhook → no double state change or double payout.
- Tampered amount request → ignored; server amount used.
- Release only possible when job is Completed (or admin decision) and no open dispute.
- All transitions create audit entries.
- Amounts stored as integers (kobo).

## 10. Mobile-Specific Payment Rules
- The app never decides that a payment succeeded. After returning from checkout it shows "Confirming payment..." and polls or listens for the server state.
- Use an idempotency key (generated per hire attempt) when initialising payments, so a retry after a dropped connection does not create a second payment.
- If the app is killed or loses network mid-payment, on next launch the Payment screen reloads state from the server and resumes.
- Only load the gateway's official checkout URL/domain in the WebView; block navigation to other domains.
- Deep link/redirect from the gateway back to the app must carry only a reference, never an amount or status the server trusts.
- Public keys only in the app bundle; secret keys stay on the server.
- Money actions are never optimistic and never queued while offline.
- Receipts are viewable in the app (and optionally emailed).
- Check Apple App Store and Google Play payment policy applicability for your service types (see doc 03 and doc 21).
- Test on real devices: slow network, switching networks during payment, user cancel, app switch to banking apps, 3-D Secure/bank-authorisation screens, and return to the app.

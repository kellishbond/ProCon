# Business Model & Monetization — ProCon

Pack 1 principle: begin with ONE simple, transparent transaction-fee model. Never hide fees.

## 1. Revenue Model for MVP
**Service fee on completed, paid jobs.**

| Item | Proposed default (OD-01) |
|---|---|
| Fee rate | 10% of the agreed job price (configurable) |
| Charged to | Provider, deducted from payout |
| Customer fee | None at MVP (optionally a small payment-processing pass-through later) |
| Minimum fee | Configurable (e.g., a flat floor) so tiny jobs are not loss-making |
| When earned | Only when the job reaches Completed and funds are released |
| Refunds | Platform fee is not earned on fully refunded jobs |

Founders must confirm the rate after interviews and after calculating payment-processor charges. The processor's own fee (a percentage plus possible flat fee) comes out of the platform's margin unless passed on; model this explicitly.

## 2. Fee Transparency Requirements
- Show the fee and provider's net payout on the application screen before the provider submits.
- Show total customer price on the hire screen before payment.
- Show a fee line on receipts and earnings screens.
- Store `platformFee`, `amount` and `currency` on every Payment record (already in Pack 1 schema).
- Fee rate used is snapshotted onto the Payment/Contract so later rate changes do not alter past jobs. (Proposed schema addition: `feeRateApplied`.)

## 3. Unit Economics Worksheet (fill in)
| Line | Value |
|---|---|
| Average job value (NGN) | |
| Platform fee % | |
| Gross fee per job | |
| Payment processing cost per job | |
| Verification cost per verified provider (amortized) | |
| Support/dispute cost per job | |
| Net contribution per job | |
| Jobs needed per month to cover fixed costs | |

## 4. Protecting Revenue (Disintermediation)
Users may take agreed jobs off-platform. Defences, in order of importance:
1. Real value on-platform: payment protection, dispute help, reputation, receipts.
2. Hide direct contact details until hire; block phone numbers/links in pre-hire messages (see doc 05).
3. Reviews and job history only count for on-platform jobs.
4. Rules in Terms of Service about circumventing fees (doc 10), enforced reasonably.
5. Don't make the fee so high that bypassing is attractive.

## 4. Later Revenue Options (post-MVP; see doc 20)
- Provider premium subscription (lead priority, analytics)
- Featured provider / sponsored listings (must be clearly labelled)
- Business plans (team accounts, invoicing, recurring bookings)
- Optional paid verification tiers
- Promoted job posts for customers

Do not build these until the core loop and fee model are validated.

## 5. Pricing Guardrails
- Prices are fixed per job in MVP (OD-08). No hidden add-ons.
- Providers propose `proposedPrice` in applications; the customer's accepted price becomes `agreedPrice`. Changes require both parties' consent and a new recorded agreement.
- Server calculates fees. Client-supplied fees/prices are never trusted.

## 6. Tax Notes (consult an accountant)
Platform fee income, VAT on platform fees, withholding obligations, and the tax treatment of payouts to providers depend on current Nigerian law and the company's setup. Get written advice before launch (see Launch Checklist).

## 7. App Store Payment Rules (verify before launch)
Apple and Google have rules about when digital purchases must use their in-app purchase systems and when other payment methods are allowed (for example, for real-world services consumed outside the app). ProCon collects payment for services performed by third parties, not for digital goods inside the app, but the rules and their exceptions are detailed and change. Before building payments, read the current Apple App Store Review Guidelines (payments section) and Google Play payments policy, decide which category each ProCon service falls into, and record the conclusion in the Decision Log. Do not add subscriptions or digital goods sold in the app (post-MVP premium plans) without re-checking.

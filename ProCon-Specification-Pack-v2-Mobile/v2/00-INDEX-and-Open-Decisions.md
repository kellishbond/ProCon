# ProCon — Specification Pack 2: Index & Open Decisions

> **Mobile pivot applied (D005):** The product is a React Native + Expo app for iOS and Android. Both packs have been updated. See `00-CHANGELOG-Mobile-Pivot.md`.

Pack 2 extends Pack 1 (folders 01–07). Pack 1 remains the source of truth for product scope, schema, API and states. Pack 2 adds business, trust, legal, operations, security and launch documents.

## Contents
| # | Document | Folder |
|---|---|---|
| 01 | Business Requirements Document | 08-BUSINESS |
| 02 | Market & Competitor Analysis | 08-BUSINESS |
| 03 | Business Model & Monetization | 08-BUSINESS |
| 04 | Go-To-Market Strategy | 08-BUSINESS |
| 05 | Trust, Safety & Verification Spec | 09-TRUST-SAFETY |
| 06 | Payment & Escrow Spec | 09-TRUST-SAFETY |
| 07 | Dispute & Refund Policy Spec | 09-TRUST-SAFETY |
| 08 | Marketplace Rules & Community Guidelines | 09-TRUST-SAFETY |
| 09 | Privacy & Data Requirements | 10-LEGAL |
| 10 | Terms of Service Requirements | 10-LEGAL |
| 11 | Admin & Operations Manual | 11-OPERATIONS |
| 12 | Notification Specification | 12-PRODUCT-SPECS |
| 13 | Search & Matching Specification | 12-PRODUCT-SPECS |
| 14 | Analytics & KPI Specification | 12-PRODUCT-SPECS |
| 15 | Security Requirements | 13-SECURITY-RISK |
| 16 | Risk Register | 13-SECURITY-RISK |
| 17 | Launch Checklist | 14-LAUNCH |
| 18 | Requirements Traceability Matrix | 14-LAUNCH |
| 19 | Agent Context / Master Instructions | 15-AGENT |
| 20 | Future Features & Ideas Backlog | 16-BACKLOG |
| 21 | App Store Compliance & Release Plan (new) | 14-LAUNCH |
| — | Mobile App Architecture (new, Pack 1 area) | 04-TECHNICAL |

## How to read "Proposed default" vs "Decided"
- **Decided** = already stated in Pack 1.
- **Proposed default** = a sensible starting value so work is not blocked. Founders must confirm or change it. Implementers must make proposed defaults configurable (config/admin setting), never hard-coded.

## Open Decisions Register
Founders: resolve these, then record each in `07-PROJECT/Product-Decision-Log.md` as D005, D006, ...

| ID | Decision needed | Proposed default | Blocks |
|---|---|---|---|
| OD-01 | Platform commission rate and who pays it | 10% service fee deducted from provider payout; shown before applying and before hiring | Payments phase |
| OD-02 | How funds are held between payment and release ("escrow") | Hold funds through a licensed payment provider/partner; do NOT hold customer money in a founder's personal or ordinary business account | Payments phase, legal |
| OD-03 | Payment provider | Paystack or Flutterwave (pick one after checking split-payment/payout/hold features) | Payments phase |
| OD-04 | Verification provider and levels | Phone + email at signup; optional ID verification (NIN/other) via a third-party verification provider | Trust phase |
| OD-05 | Launch city/region | One city only for physical services; digital services nationwide | GTM |
| OD-06 | Legal entity | Limited company via CAC before taking real payments | Launch |
| OD-07 | Minimum age | 18+ only | ToS, onboarding |
| OD-08 | Pricing model for MVP | Fixed agreed price per job (no hourly, no auctions) | Hiring, payments |
| OD-09 | Cancellation windows and fees | See doc 07 defaults | Disputes |
| OD-10 | Auto-release timer after completion submission | 72 hours of customer silence | Payments |
| OD-11 | SMS/OTP provider | Any reputable Nigeria-capable provider | Auth |
| OD-12 | Maps provider for the app | react-native-maps (Google Maps on Android, Apple Maps on iOS) or Mapbox; abstract behind a service interface; restrict API keys by app ID | Location |
| OD-13 | Off-platform contact policy | Contact details hidden until hire; payments must stay on-platform | Trust, revenue |
| OD-14 | Payout schedule | Release to provider wallet/bank within 1–2 business days after release event | Payments |
| OD-15 | Dispute response SLA | First admin response within 24h; resolution target 5 business days | Ops |
| OD-16 | Provider onboarding fee / verification fee | None at MVP | Monetization |
| OD-17 | Review window | 14 days after completion; double-blind reveal | Reviews |
| OD-18 | Brand name availability | Founders chose "ProCon" (formerly the working name ConnectNaija). Before registering the company or store accounts, check CAC name availability, the Trademarks Registry, domain, social handles and App Store/Google Play name availability. "ProCon" is also an everyday phrase (pros and cons), so expect crowded search results and possible name clashes; consider a distinctive spelling, tagline or logo | Legal, store release |
| OD-19 | Developer accounts: Apple Developer Program and Google Play Console, under a company or personal account | Company account once registered (OD-06); organisation accounts may need a business verification number, so check requirements early. Personal account possible for early testing but check store rules | Store release |
| OD-20 | Admin interface | Separate web admin panel (D007) | Admin phase |
| OD-21 | Minimum supported OS versions | Latest two or three major iOS versions; Android versions covering the large majority of target devices (decide from pilot device data) | QA, build config |
| OD-22 | Launch platforms | iOS and Android together; test priority on low-end Android | Launch |
| OD-23 | App name, bundle ID and package name | Reserve early; cannot easily change after publishing | Setup |
| OD-24 | Payment UI approach in-app | Secure in-app browser/WebView to the gateway checkout; verify store policy for your service types | Payments |
| OD-25 | Dark mode and app languages for MVP | Light mode and English first | Design |

## Consistency rules between Pack 1 and Pack 2
1. Job/Application/Payment states are exactly those in `03-UX/User-Flows.md`. Pack 2 only adds sub-reasons, not new states, unless marked "Proposed addition".
2. Schema additions in Pack 2 are marked "Proposed schema addition" and must be added to `04-TECHNICAL/Database-Schema.md` once approved.
3. If Pack 2 conflicts with Pack 1, stop and report the conflict (see Agent Instructions).

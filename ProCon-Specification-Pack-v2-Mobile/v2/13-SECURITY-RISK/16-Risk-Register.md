# Risk Register

Scoring: Likelihood (L) and Impact (I) each 1–5; Score = L × I. Review weekly. Owner = a founder name to be assigned.

| ID | Risk | Category | L | I | Score | Mitigation | Owner | Status |
|---|---|---|---|---|---|---|---|---|
| R01 | Cold start: not enough providers or customers | Market | 5 | 5 | 25 | Single city, seed supply first, founders post real jobs, narrow categories (doc 04) | | Open |
| R02 | Regulatory issue from holding customer funds | Legal | 3 | 5 | 15 | Use licensed provider/partner; legal advice before payments (doc 06) | | Open |
| R03 | Disintermediation (users go off-platform) | Business | 4 | 4 | 16 | Value on-platform, hide contacts until hire, sensible fee, reviews tied to platform (docs 03, 05) | | Open |
| R04 | Safety incident during physical job | Safety | 2 | 5 | 10 | Verification, address reveal after hire, reports, fast suspension, safety tips, insurance advice (doc 05) | | Open |
| R05 | Fraud: fake providers/customers, stolen identity | Trust | 4 | 4 | 16 | Phone/ID verification, payout name match, flags, admin queue | | Open |
| R06 | Payment bugs (double release, wrong amounts) | Technical | 3 | 5 | 15 | State machine, idempotency, integer kobo, tests, reconciliation (doc 06) | | Open |
| R07 | Data breach / privacy violation | Security/Legal | 2 | 5 | 10 | Security requirements, minimisation, encryption, NDPA compliance (docs 09, 15) | | Open |
| R08 | Disputes overwhelm two founders | Operations | 3 | 4 | 12 | Clear policy, templates, SLAs, auto-release, escrow rules, limit launch volume | | Open |
| R09 | Poor-quality providers harm reputation | Quality | 4 | 4 | 16 | Reviews, minimum standards, removal rules, curated onboarding | | Open |
| R10 | Competitors with funding/head start | Market | 4 | 3 | 12 | Focus on niche/city, trust UX, speed, founder-led onboarding | | Open |
| R11 | Verification vendor cost/failure | Vendor | 3 | 3 | 9 | Tiered verification, fallback manual review, compare vendors | | Open |
| R12 | Scope creep delays MVP | Delivery | 5 | 4 | 20 | MVP must-have list, Decision Log, agent rules, phase gates | | Open |
| R13 | Founder disagreement or one founder leaves | Team/Legal | 3 | 5 | 15 | Written founders' agreement, vesting, IP assignment, decision rules | | Open |
| R14 | Low connectivity/data cost harms UX | Product | 4 | 3 | 12 | Light pages, image compression, offline-tolerant states, mobile-first | | Open |
| R15 | Key vendor outage (payments, SMS, hosting) | Technical | 3 | 4 | 12 | Retries, status monitoring, fallback providers, runbooks | | Open |
| R16 | Review manipulation | Trust | 3 | 3 | 9 | Eligibility rules, double-blind, anomaly flags | | Open |
| R17 | Tax/compliance mistakes on platform fees and payouts | Legal/Finance | 3 | 4 | 12 | Accountant advice, correct invoicing/records | | Open |
| R18 | Unclear unit economics (fee lower than costs) | Business | 3 | 4 | 12 | Worksheet (doc 03), pilot data, adjust fee/fees | | Open |
| R19 | Name/brand conflict or trademark issue ("ProCon" is a common phrase; hard to find in search and may clash with existing names) | Legal | 3 | 3 | 9 | Check CAC, trademark registry, domain, store names (OD-18); use distinctive logo, tagline and "ProCon: Hire Trusted Pros" style store title; confirm before paying for registration | | Open |
| R20 | Misuse for illegal services | Legal/Trust | 2 | 4 | 8 | Prohibited list, flags, takedown process, ToS | | Open |
| R21 | Admin account compromise | Security | 2 | 5 | 10 | MFA, least privilege, audit logs, alerts | | Open |
| R22 | Founders' burnout / low bandwidth | Team | 4 | 4 | 16 | Realistic scope, split responsibilities, weekly cadence | | Open |

## Review Process
1. Weekly: update statuses, add new risks, close mitigated ones.
2. Any score ≥ 15 needs a named owner and an action with a date.
3. Convert major mitigations into Task Board items.
4. Record risk-related choices in the Decision Log.

## Mobile-Specific Risks (added with the mobile pivot)
| ID | Risk | Category | L | I | Score | Mitigation | Owner | Status |
|---|---|---|---|---|---|---|---|---|
| R23 | App store rejection or delay (policy gaps: payments, UGC, account deletion, privacy forms) | Store | 4 | 4 | 16 | Doc 21 checklist, reviewer demo account, early TestFlight/closed-testing submissions, read guidelines before building payments | | Open |
| R24 | Install friction reduces signups | Growth | 4 | 4 | 16 | Smart links, QR codes, in-person onboarding, browse-before-signup, light app | | Open |
| R25 | Android fragmentation and low-end device bugs | Technical | 4 | 3 | 12 | Device matrix, performance budget, test on low-end device, crash monitoring | | Open |
| R26 | Developer account problems (identity/business verification, suspension, fees, lost access) | Store/Legal | 3 | 5 | 15 | Company account, MFA, two founders as admins, keep documents ready | | Open |
| R27 | Push notifications unreliable or denied | Product | 4 | 3 | 12 | Ask at right moment, in-app + email/SMS backups, channel preferences, token cleanup | | Open |
| R28 | Old app versions break after API change | Technical | 3 | 4 | 12 | Backward-compatible API, min-version gate, API versioning, release checklist | | Open |
| R29 | Bad OTA update or release breaks the app | Technical | 3 | 5 | 15 | Staged rollout, preview channel, rollback plan, crash-free monitoring | | Open |
| R30 | Expo/React Native upgrade churn and library incompatibility | Technical | 3 | 3 | 9 | Pin versions, upgrade on a schedule, prefer well-maintained libraries, development builds early | | Open |
| R31 | Secrets or keys exposed in app bundle | Security | 3 | 5 | 15 | No secrets in client, restricted public keys, bundle inspection in release checklist | | Open |
| R32 | Users deny location/notification permissions | Product | 4 | 3 | 12 | Education screens, manual-area fallback, graceful degradation | | Open |
| R33 | Payments policy mismatch with store rules | Store/Legal | 2 | 5 | 10 | Verify guidelines for service types, avoid selling digital goods in-app, record decision | | Open |
| R34 | Mobile data cost and slow networks hurt usage | Product | 4 | 3 | 12 | Small payloads, image compression, caching, pagination | | Open |

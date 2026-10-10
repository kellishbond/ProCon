# Requirements Traceability Matrix (RTM)

Links business requirements (BRD) → Pack 1 features/epics → Pack 2 specs → acceptance/QA coverage. Update when requirements change. "Gap" marks items where Pack 1 has no matching task/epic yet.

| Req ID | Requirement | Pack 1 reference | Pack 2 spec | Task Board epic | Acceptance / QA | Gap? |
|---|---|---|---|---|---|---|
| BR-01 | Four roles | PRD §6; schema User.role | 15 (RBAC), 11 | Epic 2 (RBAC), Epic 9 | Security acceptance | |
| BR-02 | Digital + physical categories, admin-configurable | PRD §5; Category | 13 | Epic 4, Epic 9 | Marketplace QA | |
| BR-03 | Fees visible before commitment | PRD principle 6 | 03, 06, 10 | Epic 8 | New: fee-disclosure UI test | Gap: add task "Fee disclosure UI" |
| BR-04 | Platform fee on completed paid jobs | PRD §12; Payment.platformFee | 03, 06 | Epic 8 | Payment acceptance | |
| BR-05 | Traceable job/payment state changes | NFR auditability | 06, 11, 15 | Epic 8, Epic 9 | Admin: audit records | Gap: AuditLog collection not in schema |
| BR-06 | Verification badges | MVP "Provider verification badges" | 05 | Epic 3 (Verification status), Epic 2 (phone/email verification) | New: verification tests | Gap: verification provider integration task |
| BR-07 | Dispute process | Dispute flow; Dispute model | 07 | Epic 5, Epic 9 | Completion acceptance; QA Admin | Gap: dispute evidence upload, response workflow |
| BR-08 | Admin moderation tools | Admin screens | 11 | Epic 9 | QA Admin | |
| BR-09 | NGN, currency-extensible | PRD out-of-scope multi-currency | 06 | Epic 8 | Payment QA | |
| BR-10 | Native iOS/Android app, low-end devices, slow networks | PRD §1, §10; Mobile-App-Architecture | 12, 13, 21 | Epic 1, Epic 12 | Mobile Device QA | |
| BR-15 | Push notifications with deep links | Mobile-App-Architecture §8 | 12 | Epic 9 | Acceptance: Mobile App; QA push tests | |
| BR-16 | Store policy compliance (block/report, deletion, privacy forms, payments) | PRD §7 | 05 §10, 09, 10, 21 | Epic 10 | Acceptance: Mobile App | Gap: privacy label inventory task added in Epic 10 |
| BR-17 | Forced update / maintenance control | API /app/config | 11, 21 | Epic 2, Epic 11 | QA force-update test | |
| BR-11 | Lawful data processing | NFR secure PI | 09, 10 | None | None | Gap: consent capture, data export/delete, retention jobs |
| BR-12 | Help/support | Public screen: Help/FAQ | 11 | None | None | Gap: support channel/contact form task |
| BR-13 | Marketplace metrics | PRD §11; admin dashboard | 14 | Epic 9 | None | Gap: KPI queries/event tracking |
| BR-14 | Business accounts + milestones | Business flow; BusinessProfile | — | Epic 3 partially | None | Gap: milestones not in schema/API; decide MVP depth |

## Feature-Level Traceability (selected)
| Feature | Pack 1 | Pack 2 | Notes |
|---|---|---|---|
| Registration/login | API /auth/*, Epic 2 | 15 §2, 09 §3, 10 §5 | Add ToS/Privacy consent capture |
| Phone/email verification | Epic 2 P1 | 05, 12 | OTP provider OD-11 |
| Provider profile | Epic 3 | 05 §3, 13 | |
| Job creation | API /jobs, Epic 4 | 13, 05 §6 | Contact-info filtering |
| Job search/distance | Epic 4 | 13 | 2dsphere index |
| Applications | API /jobs/:id/applications | 03 §2 | Fee preview on apply |
| Hire | POST /jobs/:id/hire | 06 | Hire triggers payment initialisation |
| Messaging | Epic 6 | 05 §6, 15 §10, 12 | Pre-hire contact filtering |
| Notifications | Notification model | 12 | Add API endpoints |
| Reviews | Epic 7 | 08 §7 | Double-blind, 14-day window (OD-17) |
| Payments/escrow | Epic 8 | 06 | Hold/release states |
| Disputes | Epic 5 P1, Epic 9 | 07 | |
| Reports/moderation | Report model | 05, 08, 11 | |
| Admin dashboard | API /admin/* | 11, 14 | Extend admin API |
| Security | Tech design Security | 15 | |
| Launch | Epic 10 | 17 | |

## Proposed Pack 1 Updates (apply after founders approve)
**Schema:** AuditLog; PaymentEvent (or fields on Payment); Verification fields; consents/termsAcceptances; notificationPreferences; dispute workflow fields; feeRateApplied/processorFee/providerNet; Contract status values to include "Pending Payment".
**API:** `/notifications*`, `/users/me/notification-preferences`, `/disputes/:id/response`, `/disputes/:id/evidence`, `/verification/*`, `/users/me/data-export`, `/users/me/delete-request`, `/payments/:id/release` (internal/admin), `/admin/audit-logs`, `/admin/verification`.
**Tasks to add:** fee disclosure UI; contact-info message filter; verification integration; audit logging; consent capture; support contact; KPI queries/events; auto-release scheduler; reconciliation job; payout retry job.

## Maintenance
Add a row for each new requirement; mark Gap resolved by linking to a task ID and test case; review before every release.

## Mobile Pivot Updates
The Task Board (Pack 1) was rewritten for the mobile app and now includes epics for push/deep links (Epic 9), safety and store compliance (Epic 10), the admin web panel (Epic 11) and device QA (Epic 12). Schema and API additions for devices, sessions, app config, blocks, uploads and account deletion are in the Database Schema and API Specification. Items previously marked as gaps for BR-05, BR-06, BR-07, BR-11, BR-12 and BR-13 remain open until their tasks are created in the repository.

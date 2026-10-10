# Business Requirements Document (BRD) — ProCon

## 1. Purpose
Define the business goals, stakeholders, constraints and success conditions of ProCon so product, engineering and operations decisions trace back to a business reason.

## 2. Business Problem
Hiring people for digital and physical work in Nigeria relies on referrals, WhatsApp groups and social media. Customers lack verification, price clarity, protection and recourse. Providers lack steady demand, portable reputation and payment security.

## 3. Business Objectives
| ID | Objective | Measure |
|---|---|---|
| BO-1 | Prove the core loop works: post → apply → hire → complete → pay → review | Completed jobs with payment in a pilot city |
| BO-2 | Build a two-sided supply/demand balance | Applications per job ≥ 3; time-to-first-application < 24h (targets to be validated) |
| BO-3 | Establish trust | Dispute rate and average rating tracked from day one |
| BO-4 | Prove monetization | Platform fee collected on completed paid jobs |
| BO-5 | Stay legally compliant | Registered entity, privacy compliance, licensed payment flow |

Numeric targets are starting hypotheses, not commitments. Founders set final targets.

## 4. Stakeholders
| Stakeholder | Interest |
|---|---|
| Founders (2) | Product success, equity, legal exposure |
| Customers | Reliable, safe, fairly priced work |
| Providers | Income, fair fees, reputation |
| Businesses | Repeatable hiring, receipts, accountability |
| Admins/moderators | Tools to resolve disputes and abuse |
| Payment provider / verification vendors | Compliance and integration |
| Regulators (CAC, NDPC, FCCPC, tax authorities) | Registration, data protection, consumer protection, tax |

## 5. Scope
In scope: everything in Pack 1 "MVP Features" and "MVP Must-Have".
Out of scope: everything in Pack 1 "Out of Scope for MVP".

## 6. Business Requirements
| ID | Requirement | Priority |
|---|---|---|
| BR-01 | Support four roles: Customer, Provider, Business, Admin | Must |
| BR-02 | Support digital and physical service categories, admin-configurable | Must |
| BR-03 | Show all fees before a user commits | Must |
| BR-04 | Collect a platform fee on completed paid jobs | Must |
| BR-05 | Keep a traceable record of every job and payment state change | Must |
| BR-06 | Provide verification signals (badges) visible to customers | Must |
| BR-07 | Provide a dispute process with admin decision and audit trail | Must |
| BR-08 | Allow admins to suspend users, remove content, and manage categories | Must |
| BR-09 | Operate in NGN; keep currency field for later expansion | Must |
| BR-10 | Native mobile app for iOS and Android (React Native/Expo), usable on low-end phones and slow networks | Must |
| BR-11 | Collect and process personal data lawfully (privacy notice, consent, retention) | Must |
| BR-12 | Provide help/FAQ and a support contact channel | Should |
| BR-13 | Report key marketplace metrics to founders | Should |
| BR-15 | Push notifications with deep links to relevant screens | Must |
| BR-16 | Comply with Apple App Store and Google Play policies (block/report, in-app account deletion, privacy disclosures, payments policy) | Must |
| BR-17 | Forced-update and maintenance controls so old app versions can be retired safely | Should |
| BR-14 | Support business accounts posting larger projects with milestones | Could (Pack 1 lists milestones in Business Flow; confirm MVP depth) |

## 7. Constraints
- Two-person founding team: scope discipline matters more than breadth.
- Payments handling is regulated; use licensed providers.
- Mixed digital + physical supply makes quality control harder than a pure freelance site.
- Variable internet quality and data cost for users; app size and data usage matter.
- App store review adds release delay and rules the founders do not control.
- Native device features (push, location, camera) depend on user permissions.
- Developer accounts and store listings need a legal identity and, for organisation accounts, business verification.
- Budget unknown; prefer managed services with free/low tiers where safe.

## 8. Assumptions (to validate)
1. Customers will pay through the platform if protection is clear.
2. Providers accept a transparent fee in exchange for jobs and reputation.
3. Starting in one city gives enough local density.
4. Phone-number-based trust signals work for most users.
5. Users are willing to install an app to hire help, rather than using a mobile website.
6. Android devices will be the majority of the pilot audience (verify).

## 9. Success Criteria for MVP Launch
- App approved and live on both stores (or in the testing tracks for a closed pilot).
- A full paid job completes end-to-end without admin intervention.
- A dispute can be opened, reviewed and resolved with audit trail.
- No P0 bugs, no known critical security issues (QA launch gate).
- Legal minimums in doc 17 (Launch Checklist) are complete.

## 10. Open Items
OD-01, OD-02, OD-05, OD-06, OD-18 in `00-INDEX-and-Open-Decisions.md`.

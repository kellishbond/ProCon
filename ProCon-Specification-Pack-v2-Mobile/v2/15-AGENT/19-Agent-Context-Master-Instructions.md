# Agent Context / Master Instructions — ProCon

Read this file first. It orients a coding agent across Pack 1 (folders 01–07) and Pack 2 (folders 08–16).

## 1. What You Are Building
A Nigeria-first **mobile app (React Native + Expo, iOS and Android)** connecting customers and businesses with providers of digital services, skilled trades and local labour, backed by a Node/Express/MongoDB API, a lightweight web admin panel, and a static website for legal/support pages. Core loop to validate:
Customer posts job → providers discover → provider applies → customer hires → payment → work → completion → release → review.

## 2. Source-of-Truth Order
1. `00-INDEX-and-Open-Decisions.md` (open decisions and proposed defaults)
2. `07-PROJECT/Product-Decision-Log.md` (approved decisions)
3. Pack 1: PRD → MVP scope → User flows → Technical design → Database schema → API spec → Task board → Acceptance criteria → QA plan
4. Pack 2 specs for the area you are building (see map below)
If documents conflict, STOP and report: what conflicts, which documents, the smallest decision needed. Do not guess.

## 3. Document Map by Feature
| Building | Read |
|---|---|
| Auth, roles, sessions | PRD §6, Tech §Security, 15, 05 §2 |
| Profiles and verification | Schema, 05, 09 |
| Categories | PRD §5, Schema, 13 |
| Jobs, search, location | User flows, API, 13 |
| Applications and hire | Schema, API, 03 §2, 06 |
| Messaging | API, 05 §6, 15 §10, 12 |
| Payments and fees | 03, 06, 15 §7, Acceptance (Payment) |
| Disputes and refunds | 07, 06 |
| Reviews | Acceptance (Review), 08 §7 |
| Notifications | 12 |
| Admin and moderation | 11, 05 §8, 15 §3 |
| Analytics | 14 |
| Legal/consent UI | 09, 10 |
| Mobile architecture, navigation, push, deep links | `04-TECHNICAL/Mobile-App-Architecture.md`, 12 |
| Store release and compliance | 21, 17 |
| Release | 17 |

## 4. Non-Negotiable Rules
1. Do not invent major requirements; do not silently change architecture (modular monolith backend: Node+Express, MongoDB, REST `/api/v1`; mobile app: React Native + Expo + TypeScript; admin: React+Vite+Tailwind web panel).
2. Never trust client-supplied role, price, fee, or payment status. Compute fees and totals on the server.
3. Payment status changes only via verified, idempotent, signature-checked webhook or server-side verification. Use integer kobo for money.
4. Enforce authorization on every endpoint, including resource ownership (IDOR protection) and state-machine rules for who can trigger which transition.
5. Validate all input server-side with a schema library; whitelist fields; prevent NoSQL operator injection.
6. Create audit log entries for admin actions, financial changes and job/payment state changes.
7. Never hard-code secrets or commit `.env`. Keep `.env.example` updated.
8. Make business parameters configurable (fee rate, auto-release hours, dispute windows, thresholds) via config/admin settings. Proposed defaults come from `00-INDEX`.
9. Keep payment gateway, SMS, email, storage, maps and verification behind service interfaces so vendors can be swapped.
10. Do not expose exact addresses, contact details, emails or ID data in public responses.
11. Add tests for critical logic: state machines, fee calculation, webhooks, authorization, review eligibility.
12. Use only the job, application and payment states defined in Pack 1. Propose additions; do not add silently.
13. Preserve backward compatibility for APIs; do not delete functionality without approval.
14. Keep UI states complete: loading, empty, success, error, permission denied, device-permission denied, offline, force-update.
15. Mobile rules: no cookies; tokens in secure storage; no secrets in the bundle or `EXPO_PUBLIC_*`; API stays backward compatible (old app versions persist); never rely on Expo Go for push, payments, deep links or permissions; money actions are never optimistic or offline-queued; test on iOS and Android.
16. Store compliance is a requirement: report and block users, in-app account deletion, accurate privacy disclosures, reviewer demo account, payments policy check (doc 21).

## 5. Open Decisions to Respect
Treat the OD-xx items in `00-INDEX` as configurable placeholders. Do NOT bake in a specific payment provider, commission rate, verification vendor, or maps vendor in business logic. If you need an answer to proceed, ask for the single smallest decision.

## 6. Implementation Order (extends Pack 1)
1. Repo setup (Expo app + backend + admin panel + website), EAS profiles, linting, CI, env handling, health endpoint, logging, first development builds on Android and iOS
2. Models + indexes (including proposed additions marked approved)
3. Auth, RBAC, rate limiting
4. Profiles, categories
5. Jobs, search, location
6. Applications, hire, job state machine
7. Notifications service (in-app first)
8. Messaging (realtime + persistence + reconnect/sync), contact-info filtering, push notifications and deep links
9. Reviews
10. Payments (gateway interface, webhook, fee calc, hold/release, payout, reconciliation)
11. Disputes and refunds
12. Verification integration
13. Admin panel, moderation, audit logs
14. Analytics events and dashboard
15. Safety/store compliance (report, block, account deletion), app config and force-update
16. Security hardening, device QA, store release (doc 21), launch checklist items
Phase gates follow Pack 1 MVP phases; do not start payments before auth, jobs and state machines have tests.

## 7. Definition of Done (Pack 1 + additions)
Implemented; validated; authorized; tested; UI states handled; no secrets; docs updated; matches acceptance criteria; audit logging present where required; notifications triggered where the catalogue requires; RTM updated (doc 18).

## 8. Working Method
Before coding a feature: list the docs you read, the acceptance criteria you will satisfy, and any gaps. After coding: report files changed, features done, tests run and results, known limitations, and decisions needing human approval. If you find a gap listed in the RTM, propose a task and wait for approval before expanding scope.

## 9. Things Requiring Human (Founder) Approval
Any change to fees, states, money flows, verification meaning, data retention, public data exposure, ToS-impacting behaviour, new vendors, new dependencies with licensing concerns, destructive migrations.

## 10. Style
Readable modular code, consistent naming, small functions, clear error structures (`{ error: { code, message, details } }`), consistent HTTP codes, pagination everywhere, comments only where intent isn't obvious.

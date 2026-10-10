# Changelog — Web App → Mobile App Pivot

Decision D005: ProCon is now a React Native + Expo app for iOS and Android. This file lists what changed so you and your friend can review it.

## Product
- Customer/provider/business experience is mobile-only in MVP; web app moved to post-MVP.
- New MVP requirements: push notifications, camera/photo upload, block and report users, in-app account deletion, forced-update/minimum version, offline tolerance, store compliance.
- Admin moved to a separate lightweight web panel (D007, proposed). A static website holds legal pages, support and deletion info (D008, proposed).

## Pack 1 (updated)
| File | Change |
|---|---|
| PRD | Vision, MVP features, out-of-scope, non-functional requirements, metrics, principles |
| MVP Scope & Roadmap | Phase 0/4 additions (accounts, EAS, store testing), mobile release strategy |
| User Flows | App entry flow, push/permission/payment/offline/force-update/deletion/block flows |
| Wireframe Spec | Rewritten for mobile navigation, tab structure, device-permission and offline states |
| Technical Design | Rewritten: Expo stack, mobile auth (no cookies), API compatibility, push, env/secrets |
| **Mobile-App-Architecture (new)** | Expo Go vs dev builds, structure, navigation, state, realtime, push, performance, security, OTA |
| Database Schema | Added Device, Session, AppConfig, Block and user fields |
| API Specification | Added devices, notifications, app config, uploads, deletion, blocking, sessions; mobile API rules |
| Task Board | Rewritten into 12 mobile-oriented epics |
| Acceptance Criteria / QA Plan | Mobile acceptance and device/network/permission/push tests |
| Agent Instructions | Mobile rules and order |
| Decision Log | D003 superseded; D005–D009 added |
| README | Stack and structure updated |

## Pack 2 (updated)
Index (new open decisions OD-19 to OD-25), BRD (BR-10, BR-15–17), competitor analysis (store checks), monetization (store payment rules), GTM (mobile distribution), trust & safety (block/report/UGC), payments (mobile payment rules), disputes, rules, privacy (device data, store disclosures, deletion), ToS (app terms), operations (release and app-config management), notifications (push rules), search (location UX), analytics (mobile KPIs/events), security (mobile section, secrets in bundle), risk register (R23–R34), launch checklist (Section K), traceability matrix, agent context, backlog.
**New:** `14-LAUNCH/21-App-Store-Compliance-and-Release-Plan.md`.

## Things That Did Not Change
Backend (Node/Express/MongoDB, REST /api/v1), job/application/payment states, roles, fee model, trust and dispute model, legal approach.

## New Decisions for You and Your Friend
OD-19 developer accounts (company vs personal), OD-20 admin as web panel, OD-21 minimum OS versions, OD-22 launch platforms, OD-23 app name/bundle ID, OD-24 payment UI approach, OD-25 dark mode and languages. Confirm D007, D008 and D009.

## Known Limits of This Update
- Store policies and fees change; items marked "verify" must be checked against current official pages.
- Specific library versions and Expo SDK number are not pinned here; choose the latest stable Expo SDK when you initialise the project.

## Rename
The project name changed from ConnectNaija to ProCon (D010). All documents were updated. Name availability is still to be confirmed (OD-18).

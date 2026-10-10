# Agent Implementation Instructions

## Mission
Implement the marketplace described by this documentation pack as a **React Native + Expo mobile app (iOS and Android)** with a Node/Express/MongoDB backend, a lightweight web admin panel and a static website. Treat these documents as the source of truth. Also read `15-AGENT/19-Agent-Context-Master-Instructions.md`.

## Rules
1. Do not invent major product requirements.
2. Do not silently change the architecture.
3. If a requirement conflicts with another document, stop and identify the conflict.
4. Prefer simple, maintainable implementations.
5. Keep frontend and backend responsibilities separate.
6. Never hard-code secrets.
7. Never trust client-supplied role, price or payment status.
8. Validate server-side.
9. Add tests for critical business logic.
10. Preserve backward compatibility when changing APIs.
11. Do not delete existing functionality without explicit approval.
12. Keep code modular and readable.
13. This is a mobile app: no cookies, no web-only APIs (window, localStorage) in the app code. Use secure storage for tokens.
14. Never put secrets in the app bundle or in EXPO_PUBLIC_* variables.
15. Keep the API backward compatible; older app versions stay in the wild.
16. Verify behaviour on both iOS and Android; do not rely on Expo Go for push, payments, deep links or permissions.
17. Money actions are never optimistic or queued offline.
18. Follow Apple App Store and Google Play policy requirements (block/report, account deletion, privacy disclosures).

## Implementation Order
1. Repository/project setup (Expo app, backend, EAS profiles, CI)
2. Database models
3. Authentication/authorization
4. Profiles
5. Categories
6. Jobs
7. Applications
8. Hiring/job lifecycle
9. Messaging
10. Reviews
11. Payments
12. Push notifications and deep links
13. Safety and store compliance (report, block, account deletion)
14. Admin web panel
15. QA/security/device testing
16. Store release (TestFlight, Play testing, production)

## Before Coding a Feature
Read:
- PRD
- MVP scope
- User flows
- Technical design
- Database schema
- API specification
- Relevant task and acceptance criteria
- Mobile architecture (`04-TECHNICAL/Mobile-App-Architecture.md`)
- Relevant Pack 2 spec

## When Unsure
Do not make a large assumption. State:
- What is unclear
- What documents were checked
- The smallest decision required

## Completion
After implementation, report:
- Files changed
- Features implemented
- Tests run (and on which platforms/devices)
- Known limitations
- Any decisions requiring human approval

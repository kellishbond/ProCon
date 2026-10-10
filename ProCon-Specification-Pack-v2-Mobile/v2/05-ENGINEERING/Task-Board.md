# Engineering Task Board (Mobile)

Legend: P0 = MVP blocker, P1 = MVP important, P2 = post-MVP.

## Epic 1 — Project Setup
- P0 Initialize Expo (TypeScript) project with Expo Router
- P0 Initialize backend
- P0 Configure environment handling (app.config.ts, EAS secrets, backend env)
- P0 Configure database
- P0 Configure EAS Build profiles (development, preview, production) and first development build on Android and iOS
- P0 API client with auth header, refresh, timeout, error mapping
- P1 Configure styling system (NativeWind or equivalent), theme, safe areas
- P1 Linting/formatting/type-check and CI
- P1 Error/crash tracking (Sentry or equivalent)
- P1 Admin web panel scaffold (separate app)
- P1 Static website scaffold (legal pages, support, deletion info)

## Epic 2 — Authentication
- P0 Registration with Terms/Privacy acceptance
- P0 Login
- P0 Secure token storage and refresh rotation
- P0 Logout and device session revoke
- P0 Role-based access
- P1 Password reset
- P1 Phone OTP and email verification
- P1 Force-update gate using /app/config

## Epic 3 — Profiles
- P0 Customer profile
- P0 Provider onboarding
- P0 Provider profile
- P0 Photo capture/pick, compress, signed upload
- P1 Portfolio
- P1 Verification status and flow

## Epic 4 — Marketplace
- P0 Categories
- P0 Create job (multi-step with photos)
- P0 Browse jobs (infinite scroll)
- P0 Search/filter
- P0 Provider application
- P0 Customer application review
- P0 Hire provider
- P1 Distance filtering and map view
- P1 Location permission education and manual-area fallback

## Epic 5 — Job Lifecycle
- P0 Job states
- P0 Provider acceptance
- P0 Completion confirmation
- P1 Cancellation
- P1 Dispute (open, respond, evidence upload, view status)

## Epic 6 — Messaging
- P1 Conversations
- P1 Realtime messaging with reconnect and missed-message sync
- P1 Read status
- P1 Image attachments
- P1 Contact-info filtering before hire

## Epic 7 — Reviews
- P1 Customer reviews provider
- P1 Provider reviews customer
- P1 Rating aggregation

## Epic 8 — Payments
- P1 Fee disclosure UI
- P1 Payment initialization with idempotency key
- P1 In-app payment flow (secure in-app browser/WebView) and return handling
- P1 Webhook verification
- P1 Transaction records and receipts
- P1 Platform fee calculation
- P1 Payout/release foundation, auto-release scheduler, reconciliation job

## Epic 9 — Push, Notifications, Deep Links
- P0 Device registration endpoint and token lifecycle
- P1 Push sending service, failure handling, invalid token cleanup
- P1 Notification channels and preferences
- P1 Deep link handling (cold, warm, logged-out)
- P1 In-app notification list with unread badge

## Epic 10 — Safety and Store Compliance
- P0 Report user/job/message/review
- P0 Block user
- P0 In-app account deletion flow and backend processing
- P1 Content filtering/flagging for objectionable content
- P1 Privacy labels / data safety inventory
- P1 Reviewer test accounts and demo data

## Epic 11 — Admin (web panel)
- P0 Admin authentication with MFA
- P0 User management
- P0 Job moderation
- P0 Category management
- P1 Reports, blocks
- P1 Disputes
- P1 Transactions
- P1 Verification queue
- P1 Audit logs
- P1 App config management (minimum version, maintenance mode)

## Epic 12 — QA/Launch
- P0 Unit tests for critical services
- P0 API integration tests
- P0 Authentication/security testing
- P0 Payment webhook tests
- P0 Device testing (iOS, multiple Android incl. low-end)
- P0 Offline/slow-network testing
- P1 End-to-end tests for critical flows
- P1 Performance testing (startup, list scrolling)
- P1 Store listings, screenshots, TestFlight and Play testing tracks
- P1 Production deployment and monitoring

## Definition of Done
A task is complete only when:
1. Code is implemented.
2. Validation/error handling exists.
3. Authorization is enforced.
4. Relevant tests pass.
5. UI handles loading/empty/error/offline states.
6. Works on both iOS and Android (verified on devices or emulators).
7. No secrets are committed or bundled in the app.
8. Backward compatibility with older app versions is preserved.
9. Documentation is updated where necessary.
10. The feature matches acceptance criteria.

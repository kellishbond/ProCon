# PROCON — FULL SPECIFICATION v2 (MOBILE APP: REACT NATIVE + EXPO)


---
# 00-CHANGELOG-Mobile-Pivot.md

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


---
# 00-INDEX-and-Open-Decisions.md

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


---
# 01-PRD/Product-Requirements-Document.md

# Product Requirements Document (PRD)
## Working Product Name: ProCon

### 1. Product Vision
ProCon is a Nigeria-first **mobile app (iOS and Android)** that connects people and businesses that need work done with trusted people who can do it. The platform supports both digital services and physical/local labour.

**Platform decision (D005):** The customer and provider product is a native mobile app built with React Native and Expo. There is no customer-facing web app in the MVP. Admins use a separate lightweight web admin panel (D007), and a small static website hosts legal pages, support and account-deletion information required by the app stores.

### 2. Problem
Finding trustworthy workers in Nigeria often depends on personal referrals, WhatsApp groups, social media, or informal networks. Customers struggle to compare providers, verify identity, agree on scope and price, track work, and resolve disputes. Skilled workers also struggle to consistently find customers and build portable reputations.

### 3. Target Users
- Customers needing one-off or recurring services
- Freelancers and digital professionals
- Skilled tradespeople
- General labour/service workers
- Small businesses and organizations
- Platform administrators

### 4. Core Value Proposition
For customers: discover, compare, hire, communicate with, pay, and review trusted providers.
For providers: create a professional profile, discover jobs, apply, get hired, build reputation, and receive payments.

### 5. Service Categories
Initial categories should include:
- Cleaning
- Plumbing
- Electrical
- Generator/AC services
- Painting
- Carpentry
- Moving/labour
- Beauty/personal care
- Repairs/maintenance
- Events
- Photography/video
- Tutoring
- Writing
- Design
- Software development
- Digital marketing
- Virtual assistance
- Other services

Categories must be admin-configurable.

### 6. User Roles
Customer, Service Provider, Business, Administrator.

### 7. MVP Features
- iOS and Android app (single React Native/Expo codebase)
- Account registration/login
- Role selection
- Customer profile
- Provider profile
- Identity/phone verification foundation
- Service categories
- Job creation
- Job browsing/search
- Location and distance filtering
- Provider applications/offers
- Customer shortlist and hiring
- In-platform job status
- Messaging
- Notifications
- Reviews/ratings
- Admin dashboard
- Basic reporting/moderation
- Payment integration architecture
- Transaction records
- Push notifications (device registration, deep links to the relevant screen)
- Camera/photo upload for profiles, jobs, portfolio and dispute evidence
- Block and report users (also an app store requirement for apps with user-generated content)
- In-app account deletion (app store requirement)
- Forced-update / minimum app version control
- Lightweight web admin panel (admin and moderators only)
- Static website for legal pages, support and account deletion info

### 8. Out of Scope for MVP
- Customer/provider web app (the product is mobile-only in MVP)
- Tablet-optimised layouts
- Complex AI matching
- International expansion
- Full payroll/employment management
- Advanced subscription plans
- Complex auction/bidding algorithms
- Automated background checks beyond supported verification
- Multi-country currencies

### 9. Key User Stories
#### Customer
- As a customer, I want to create an account so I can hire providers.
- As a customer, I want to post a job with category, description, location, budget and timing.
- As a customer, I want to receive applications so I can compare providers.
- As a customer, I want to message a provider before hiring.
- As a customer, I want to confirm completion and review the provider.

#### Provider
- As a provider, I want to create a profile showing my skills, experience, location and pricing.
- As a provider, I want to find jobs relevant to my skills and location.
- As a provider, I want to apply to jobs.
- As a provider, I want to track accepted jobs and payments.
- As a provider, I want reviews to build my reputation.

#### Admin
- As an admin, I want to manage users, jobs, categories, disputes and reports.
- As an admin, I want to moderate suspicious content and accounts.

### 10. Non-Functional Requirements
- Native mobile experience on iOS and Android with a single codebase
- Works acceptably on low-end Android phones and slow/unstable mobile networks (small app size, light screens, image compression, caching, retry)
- Offline tolerance: cached read screens, queued retries for safe actions, clear offline states
- Secure token storage on the device (secure storage, not plain storage)
- Backward-compatible API: old app versions stay in use for weeks, so the API must not break them
- Secure authentication and authorization
- Server-side validation
- Rate limiting on sensitive endpoints
- Auditability of financial/job state changes
- Accessible UI (screen readers, scalable text, sufficient contrast, touch targets)
- Reasonable screen load performance on Nigerian mobile networks and mid/low-range devices
- Compliance with Apple App Store and Google Play policies
- Scalable architecture
- Secure handling of secrets and personal information

### 11. Success Metrics
- App installs and install-to-signup rate
- Registered customers
- Registered providers
- Jobs posted
- Applications per job
- Hire conversion rate
- Completed jobs
- Repeat customers
- Provider retention
- Average rating
- Dispute rate
- Payment success rate
- Platform revenue
- Day-1/Day-7/Day-30 retention
- Crash-free sessions and store rating
- Push notification opt-in rate

### 12. Business Model
Potential models:
- Commission/service fee on completed transactions
- Provider premium subscriptions
- Business plans
- Featured provider listings
- Sponsored placements
- Optional verification fees

The MVP should begin with one simple, transparent transaction-fee model.

### 13. Product Principles
1. Trust before growth.
2. Mobile-native: the app is the product.
3. Simple enough for non-technical users.
4. Location matters for physical services.
5. Payments and job state must be traceable.
6. Never hide important fees.
7. Build Nigeria-first, but avoid architecture that blocks future expansion.
8. Respect the user's data and battery: lightweight screens, compressed images, foreground-only location, minimal background activity.
9. Never break old app versions silently: version the API and support a minimum-version gate.


---
# 02-MVP/MVP-Scope-and-Roadmap.md

# MVP Scope & Roadmap

## Phase 0 — Product Foundation
- Finalize categories
- Finalize user roles
- Confirm payment provider
- Confirm identity verification approach
- Define legal/policy requirements
- Create design system (mobile components, navigation, safe areas, dark mode decision)
- Create Apple Developer and Google Play developer accounts (company account preferred; see Launch Checklist)
- Reserve app name, bundle ID / package name, domain
- Set up Expo project, EAS Build, development builds, and CI

## Phase 1 — Core Marketplace
- Registration/login
- Customer/provider profiles
- Category management
- Job creation
- Job discovery
- Search/filtering
- Applications
- Hiring
- Job status tracking

## Phase 2 — Trust & Communication
- Messaging
- Notifications
- Ratings/reviews
- Provider verification badges
- Report user/job
- Admin moderation

## Phase 3 — Payments
- Payment initiation
- Transaction records
- Payment status webhooks
- Platform fee calculation
- Provider payout workflow
- Refund/dispute foundation

## Phase 4 — Launch Readiness
- Store listings, screenshots, privacy labels / data safety forms, reviewer test accounts
- Internal and closed testing (TestFlight and Google Play testing tracks)
- Security review
- QA on real iOS and low-end Android devices
- Performance testing on slow networks
- Error monitoring
- Analytics
- Production deployment
- Documentation

## Post-MVP
- AI provider matching
- Customer/provider web app
- Tablet layouts
- Recurring bookings
- Provider subscriptions
- Business accounts
- Advanced verification
- Wallets
- Promotional tools
- Multi-country support

## MVP Must-Have
Mobile app shell and navigation, authentication, profiles, jobs, applications, hiring, messaging, push notifications, location filtering, reviews, block/report, account deletion, admin controls and payment foundation.

## MVP Nice-to-Have
AI matching, advanced analytics, subscriptions, web app for customers/providers, tablet support and complex promotional systems.

## Mobile Release Strategy
1. Develop with Expo Go only for early UI work; move to development builds as soon as native modules (push, maps, secure storage config) are needed.
2. Internal testing builds (EAS Build) to founders and a small circle.
3. Closed beta via TestFlight (iOS) and Google Play closed testing (Android). Google may require a minimum tester period for new developer accounts: verify current rules early.
4. Production release to both stores after the Launch Checklist gate.
5. Ship JavaScript-only fixes through over-the-air updates where store policy allows; ship native changes through new store builds.


---
# 03-UX/User-Flows.md

# User Flows

## App Entry Flow (all users)
Install → Splash → (Force-update check) → Onboarding intro → Register/Login → Role selection → Permission education (notifications, location) → Home

## Customer Flow
Home → Register/Login (if needed) → Customer Dashboard → Create Job → Add Category → Description → Budget → Location → Schedule → Review → Publish → Receive Applications → Compare Providers → Message → Hire → Track Job → Confirm Completion → Review → Receipt

## Provider Flow
Home → Register/Login (if needed) → Provider Setup → Skills/Categories → Service Area → Experience → Pricing → Profile → Browse Jobs → Filter by Category/Distance/Budget → View Job → Apply/Offer → Customer Review → Hire → Message → Start Job → Complete → Payment Status → Review

## Business Flow
Register → Business Profile → Post Job/Project → Receive Applications → Shortlist → Interview/Message → Hire → Milestones → Completion → Payment → Review

## Admin Flow
Admin Login → Dashboard → Users/Providers → Jobs → Reports → Disputes → Categories → Transactions → Verification → Moderation → Audit Logs

## Dispute Flow
Customer/Provider opens dispute → Select reason → Attach evidence → Job/payment temporarily flagged → Admin reviews → Decision → Refund/release/other resolution → Audit log

## Important States
Job:
Draft → Published → Receiving Applications → Provider Selected → In Progress → Submitted for Completion → Completed / Cancelled / Disputed

Application:
Submitted → Viewed → Shortlisted → Accepted / Rejected / Withdrawn

Payment:
Created → Pending → Successful → Held/Processing → Released / Refunded / Failed

## Mobile-Specific Flows
**Push notification tap:** Notification → app opens (cold or warm start) → deep link to the relevant screen (job, application, conversation, payment, dispute). If logged out, log in first and then resume the deep link.
**Permission flow:** Show a short in-app explanation before the system permission prompt. If the user denies, offer manual alternatives (choose area manually, skip photos) and a path to system settings.
**Payment flow:** Hire → Review price and fees → Pay (secure in-app browser or gateway view) → Return to app → Show pending state → Update when the server confirms.
**Offline flow:** Show cached content with an offline banner; block money actions; queue safe actions (e.g., drafting a message) for retry.
**Force update:** If app version is below the minimum supported, show a blocking update screen with a store link.
**Account deletion:** Settings → Delete account → Explain consequences (active jobs, payments, retention) → Confirm password/OTP → Deletion request recorded → Confirmation.
**Block/report user:** Profile or conversation menu → Report/Block → Reason → Confirmation.


---
# 03-UX/Wireframe-Specification.md

# Wireframe Specification (Mobile App)

Design for a phone first (portrait). Test on small, low-end Android phones and on iPhones. Tablets are out of MVP scope.

## App Shell
- **Splash and update check** → **Onboarding intro (3 short slides, skippable)** → **Auth**.
- Navigation: React Navigation / Expo Router. Bottom tabs per role, stack screens inside each tab, modals for create/confirm actions.
- Respect safe areas, notches, keyboard avoidance, Android back button and iOS swipe-back.

## Public / Pre-login Screens
1. Splash / force-update gate
2. Onboarding intro
3. Browse categories (read-only preview, optional)
4. Login
5. Registration (with Terms + Privacy acceptance)
6. OTP/email verification
7. Role selection
8. Forgot/reset password
9. Help/FAQ (in-app screen plus link to website)

## Customer App (bottom tabs: Home · My Jobs · Messages · Notifications · Profile)
1. Home (categories, search, nearby/top providers)
2. Create job (multi-step: category → details → photos → budget → location → schedule → review → publish)
3. My jobs (tabs: Open · Active · Completed)
4. Job detail and applications list
5. Provider profile (from application or search)
6. Messages list and chat
7. Active job (status timeline, complete/dispute actions)
8. Hire and payment (price, fee summary, pay)
9. Transaction history and receipt
10. Review/rating
11. Notifications list
12. Profile and settings (edit profile, notification preferences, blocked users, delete account, legal links, app version)

## Provider App (bottom tabs: Jobs · My Work · Messages · Earnings · Profile)
1. Provider onboarding (skills, service area, pricing, photos, portfolio)
2. Verification status and submission
3. Job feed with filters (category, distance, budget) and map toggle
4. Job detail
5. Application form (shows fee and net payout)
6. My applications
7. Active jobs (start, submit completion, dispute)
8. Earnings and payout details
9. Messages and chat
10. Reviews received
11. Notifications
12. Settings (same as customer settings)

## Business App
Same as Customer plus business profile and a project/milestone view if MVP depth is confirmed (BR-14).

## Admin (web panel, not in the mobile app)
Dashboard, Users, Providers, Jobs, Categories, Reports, Disputes, Transactions, Verification, Audit logs, Settings.

## Required UI States (every major screen)
- Loading (skeletons, not blank screens)
- Empty
- Success
- Error with retry
- Permission denied (data or role)
- **Device permission denied** (location, notifications, camera, photos) with explanation and "open settings" action
- **Offline / poor network** banner, cached data, retry
- **Force update required**
- **Maintenance mode**
- Keyboard open (inputs not hidden)
- Small screen and large text (accessibility font scaling)
- Dark mode if adopted (decision needed)
- Android and iOS visual checks

## Mobile Interaction Rules
- Primary action reachable with the thumb; minimum touch target about 44 pt.
- Pull to refresh and infinite scroll with pagination.
- Haptic feedback sparingly (confirmations).
- Image picking with compression and size limits before upload.
- Money screens always show NGN amounts, fee, and net clearly.
- Destructive actions need confirmation.
- Chat: message status (sending, sent, failed/retry), keyboard-aware input, image attachments.

## Design Direction
Simple, trustworthy, Nigerian-first, mobile-native. Prioritize clear calls to action, readable pricing, provider trust indicators (verification badge, rating, completed jobs) and job status. Keep text readable outdoors (high contrast). Keep the visual weight low for slow devices.


---
# 04-TECHNICAL/API-Specification.md

# API Specification

Base path: /api/v1

## Auth
POST /auth/register
POST /auth/login
POST /auth/logout
POST /auth/refresh   (refresh token in request body, not a cookie)
GET /auth/me
POST /auth/verify-otp
POST /auth/forgot-password
POST /auth/reset-password
GET /auth/sessions
DELETE /auth/sessions/:id   (log out a device)

## Users
GET /users/:id
PATCH /users/:id
DELETE /users/me   (account deletion request, app store requirement)
POST /users/:id/block
DELETE /users/:id/block
GET /users/me/blocked

## Providers
POST /providers/profile
GET /providers
GET /providers/:id
PATCH /providers/:id

## Categories
GET /categories
POST /categories (admin)
PATCH /categories/:id (admin)

## Jobs
POST /jobs
GET /jobs
GET /jobs/:id
PATCH /jobs/:id
POST /jobs/:id/cancel

## Applications
POST /jobs/:id/applications
GET /jobs/:id/applications
GET /applications/me
PATCH /applications/:id

## Hiring
POST /jobs/:id/hire
GET /jobs/:id/contract
PATCH /jobs/:id/status

## Messages
GET /conversations
GET /conversations/:id/messages
POST /conversations/:id/messages

## Reviews
POST /jobs/:id/review
GET /providers/:id/reviews

## Payments
POST /payments/initialize
GET /payments/:id
POST /payments/webhook

## Disputes
POST /jobs/:id/disputes
GET /disputes
PATCH /disputes/:id (admin)

## Devices and Push
POST /devices   (register/refresh push token)
DELETE /devices/:id   (on logout)
GET /notifications
PATCH /notifications/:id/read
POST /notifications/read-all
GET/PATCH /users/me/notification-preferences

## App Config
GET /app/config   (public; minimum supported version, latest version, maintenance mode)

## Uploads
POST /uploads/sign   (returns signed upload parameters; type/size limited)

## Admin
GET /admin/dashboard
GET /admin/users
GET /admin/jobs
GET /admin/reports
GET /admin/transactions

## API Rules
- Validate all input.
- Authenticate protected endpoints.
- Enforce role permissions.
- Use consistent HTTP status codes.
- Return stable error structures.
- Paginate list endpoints.
- Never expose password hashes, secrets or sensitive payment data.
- Mobile: do not use cookies for the app; use bearer tokens.
- Mobile: keep v1 backward compatible; add fields, never remove or rename.
- Mobile: support idempotency keys on payment initialization and create endpoints.
- Mobile: accept `X-App-Version`, `X-Platform`, `X-Device-Id` headers and log them.
- Mobile: all list endpoints use pagination suited to infinite scroll (cursor preferred).
- Mobile: keep responses small; support field selection or lean list payloads for slow networks.


---
# 04-TECHNICAL/Database-Schema.md

# Database Schema

## User
- id
- role
- name
- email
- phone
- passwordHash
- status
- verificationStatus
- createdAt
- updatedAt

## ProviderProfile
- userId
- bio
- skills
- categories
- experience
- pricing
- serviceArea
- location
- availability
- portfolio
- ratingAverage
- completedJobs

## BusinessProfile
- userId
- businessName
- description
- industry
- contactDetails
- verificationStatus

## Category
- id
- name
- slug
- parentId
- type (digital/physical/both)
- active

## Job
- id
- customerId
- title
- description
- categoryId
- budgetMin
- budgetMax
- location
- schedule
- status
- attachments
- createdAt
- updatedAt

## Application
- id
- jobId
- providerId
- message
- proposedPrice
- status
- createdAt

## Hire/Contract
- id
- jobId
- customerId
- providerId
- agreedPrice
- status
- startAt
- completionAt

## Message
- id
- conversationId
- senderId
- body
- attachments
- createdAt
- readAt

## Review
- id
- jobId
- reviewerId
- revieweeId
- rating
- comment
- createdAt

## Payment
- id
- jobId
- payerId
- payeeId
- providerReference
- amount
- platformFee
- currency
- status
- createdAt
- updatedAt

## Dispute
- id
- jobId
- openedBy
- reason
- evidence
- status
- resolution
- resolvedBy
- resolvedAt

## Notification
- id
- userId
- type
- title
- body
- readAt
- createdAt

## Report
- id
- reporterId
- targetType
- targetId
- reason
- status
- resolvedBy
- resolvedAt

Indexes should be designed around authentication lookups, job filtering, category filtering, provider location, conversations and payment references.

## Mobile-Driven Additions (D005)

## Device
- id
- userId
- expoPushToken (or native token)
- platform (ios/android)
- appVersion
- osVersion
- deviceId
- notificationsEnabled
- lastSeenAt
- active (false when the push service reports an invalid token)
- createdAt

## Session (device session / refresh token)
- id
- userId
- deviceId
- refreshTokenHash
- createdAt
- lastUsedAt
- expiresAt
- revokedAt

## AppConfig
- platform (ios/android)
- minSupportedVersion
- latestVersion
- maintenanceMode
- message
- updatedAt

## Block
- id
- blockerId
- blockedId
- createdAt

Notes:
- Report (existing) must support targetType values: user, job, message, review, profile.
- User should add: `deletionRequestedAt`, `anonymisedAt`, `notificationPreferences`, `termsAcceptances[]`, `consents[]` (see Pack 2 docs 09, 10, 12).
- Payment, Dispute, Verification and AuditLog additions are specified in Pack 2 docs 05, 06, 07 and 18.


---
# 04-TECHNICAL/Mobile-App-Architecture.md

# Mobile App Architecture (React Native + Expo)

## 1. Why This Choice (D005, D006)
One TypeScript/JavaScript codebase for iOS and Android; push, camera, location and secure storage covered by well-supported Expo modules; EAS handles cloud builds and store submission without owning a Mac for every build; over-the-air updates for JS fixes. Trade-off: some native features need a development build, and store review adds release delay.

## 2. Expo Go vs Development Builds
- **Expo Go** is a ready-made sandbox app for fast early development. It cannot include arbitrary native modules or your own app config, and recent Expo versions limit some features in it (for example, remote push on Android). Use it for early UI work only.
- **Development builds** (EAS Build) are your own app with developer tools. Use them once you rely on push, maps keys, deep links, secure store configuration or any non-Expo native library.
- **Production builds** come from EAS Build and are submitted via EAS Submit.
Rule: never test payments, push, deep links or permissions only in Expo Go.

## 3. Project Structure (suggested)
```
app/                 # Expo Router screens (auth, tabs per role, modals)
src/
  api/               # API client, endpoints, interceptors, error mapping
  features/          # auth, jobs, applications, chat, payments, reviews, profile
  components/        # shared UI
  hooks/
  store/             # light client state (auth session, UI)
  lib/               # push, location, uploads, analytics, config, deep links
  schemas/           # Zod schemas
  theme/
assets/
app.config.ts        # env-driven config
eas.json             # build profiles: development, preview, production
```

## 4. Navigation
Role-based tab navigators (Customer, Provider, Business). Auth stack before login. Deep link map for: job, application, conversation, payment, dispute, review. Handle cold start links, warm links and logged-out links (resume after login). Unknown links go to Home.

## 5. State and Data
- Server data: TanStack Query with sensible stale times, retries with backoff, pagination/infinite queries, optimistic updates only for safe actions (e.g., mark notification read).
- Client state: minimal (session, UI flags). Avoid duplicating server data.
- Persist query cache for read-only offline access to recent jobs, conversations, profile.
- Money actions (hire, pay, release, dispute) are never optimistic and never queued offline.

## 6. Networking
- Single API client with base URL from config, auth header injection, token refresh on 401 (single-flight refresh), request timeouts, retry for idempotent GETs, clear error mapping.
- Send idempotency keys on payment initialization and other create actions that could be retried.
- Compress images before upload; upload directly to storage with backend-signed parameters; show progress and allow retry.

## 7. Realtime Messaging
Socket.IO client connects after login, authenticates with the access token, joins conversation rooms authorised by the server, reconnects with backoff on app foreground/network change, and falls back to REST sync on reconnect (fetch missed messages). Disconnect when the app is backgrounded for a while; rely on push for new-message alerts.

## 8. Push Notifications
Request permission at a meaningful moment (after first job or application), not on first launch. Register the token with `POST /devices` including platform, app version and device ID; refresh on app start; deregister on logout. Handle foreground display, background delivery and tap-to-deep-link. Provide Android notification channels (messages, job updates, payments, marketing). Respect user preferences (doc 12).

## 9. Location and Maps
Foreground location only. Explain why before the system prompt. Provide manual area selection when denied. Never require GPS to use the app. Don't poll location continuously. Strip precise location from public views. Restrict map API keys by app identifier.

## 10. Media
Camera and photo library permissions requested just in time. Compress and resize, strip EXIF location from public images, limit counts and sizes, validate type on the server.

## 11. Performance Budget (starting)
Cold start to interactive: target under about 3 s on a mid-range Android phone; list screens use virtualized lists with pagination; avoid heavy libraries; use image caching and appropriately sized images; measure app size and keep it modest; test with network throttling and on at least one low-end Android device.

## 12. Security on Device
Tokens in secure storage; no secrets in the bundle; validate deep link parameters; do not log tokens or personal data; clear session data on logout; optional root/jailbreak awareness (post-MVP); use HTTPS only; consider certificate pinning later if risk justifies the maintenance cost.

## 13. Versioning and Updates
- Semantic app version plus build number; backend logs versions.
- `GET /app/config` supplies minimum supported version and maintenance mode.
- OTA updates (EAS Update) for JavaScript/asset fixes within the same native runtime; native changes need a new store build. Follow store policies: OTA must not change the app's core purpose or bypass review.
- Release channels: preview (staging API), production.
- Staged rollouts on Google Play; phased release on the App Store.

## 14. Testing
Unit tests (logic, schemas), component tests, API integration tests, end-to-end tests on devices/emulators (e.g., Maestro or Detox) for critical flows: register, post job, apply, hire, pay (sandbox), complete, review. Manual device matrix: iOS current and previous major, Android versions across the supported range (OD-21), small and large screens, low-RAM device, slow network, offline, background/foreground, push cold-start, deep links, permission denial.

## 15. Analytics and Crash Reporting
Event tracking per doc 14 with consent; Sentry or equivalent for crashes, JS errors and performance; attach app version, platform, OS version, device model; scrub personal data.

## 16. CI/CD
Pull request checks: type check, lint, unit tests. EAS Build on tagged commits or on demand for preview builds. EAS Submit to TestFlight and Google Play tracks. Secrets stored in EAS secrets. Keep a release checklist (see doc 21).

## 17. Admin Panel and Static Website
Admin web panel: React + Vite + Tailwind, admin-only login with MFA, talks to `/api/v1/admin/*`. Static website: privacy policy, terms, support contact, account-deletion instructions, app download links.


---
# 04-TECHNICAL/Technical-Design-Document.md

# Technical Design Document (Mobile)

Supersedes the web-based version. See also `04-TECHNICAL/Mobile-App-Architecture.md` for detailed mobile design.

## Recommended Initial Stack
**Mobile app:** React Native with Expo (TypeScript), Expo Router (file-based navigation), EAS Build/Submit/Update, NativeWind (Tailwind-style styling) or equivalent
**Server state and caching:** TanStack Query (React Query), with persistence for offline reads
**Forms and validation:** React Hook Form + Zod (share schemas with the backend where practical)
**Secure storage:** expo-secure-store for tokens
**Push:** expo-notifications (Expo push service over APNs/FCM) with server-side sending
**Location/maps:** expo-location (foreground only) plus react-native-maps or equivalent (decision OD-12)
**Media:** expo-image-picker, expo-image-manipulator (compress), expo-image for display
**Payments:** Paystack or Flutterwave, opened in a secure in-app browser/WebView flow; server verification is authoritative (decision OD-03)
**Realtime:** Socket.IO client (or equivalent) with reconnect handling
**Backend:** Node.js + Express (unchanged), REST `/api/v1`
**Database:** MongoDB (unchanged)
**File storage:** Cloudinary or equivalent, using backend-signed uploads
**Admin:** Separate lightweight web admin panel (React + Vite + Tailwind) talking to admin API routes (D007)
**Static site:** Small website for privacy policy, terms, support, account deletion instructions (required by store listings)
**Crash/error tracking:** Sentry (React Native SDK) or equivalent
**Deployment:** Managed backend hosting; EAS for app builds and OTA updates

## Architecture
Mobile app (iOS/Android)
→ API client (HTTPS, bearer token, retry/backoff)
→ REST API
→ Authentication/Authorization middleware
→ Controllers/Services
→ Database
→ External services (payments, storage, maps, push, SMS, email, verification)

Admin web panel → admin REST routes (same API, admin role only).
Realtime messaging uses a dedicated realtime layer; history is persisted in the database.

## Core Backend Modules
- Auth (including device sessions)
- Users
- Provider Profiles
- Businesses
- Categories
- Jobs
- Applications
- Contracts/Hires
- Messages
- Notifications (in-app + push + email + SMS)
- Devices (push tokens)
- Reviews
- Payments
- Disputes
- Reports and Blocks
- Admin
- Verification
- App Config (minimum version, maintenance flag)
- Uploads (signed upload tokens)

## Mobile Authentication
- No cookies. Short-lived access token in the Authorization header; rotating refresh token stored in secure storage (Keychain on iOS, encrypted storage on Android via expo-secure-store).
- Refresh tokens are tied to a device session record so a lost device or a "log out everywhere" can revoke them.
- Biometric unlock is optional (post-MVP) and only protects local access.

## API Compatibility (critical for mobile)
- Users do not update instantly. Keep `/api/v1` backward compatible; add fields, do not remove or rename them.
- `GET /app/config` returns `minSupportedVersion` per platform, `latestVersion`, `maintenanceMode`, and message text. The app checks it at launch and on resume.
- Send `X-App-Version`, `X-Platform`, `X-Device-Id` headers from the app; log them.
- Introduce `/api/v2` only for breaking changes, and keep v1 until usage drops.

## Security
- Password hashing
- Rotating refresh tokens, hashed server-side
- RBAC
- Input validation
- Rate limiting
- File upload validation (server-signed uploads, type and size limits)
- Webhook signature verification
- Audit logs for privileged/financial actions
- Never put secrets in the app bundle: anything in `EXPO_PUBLIC_*` variables or app config is readable by anyone who downloads the app. Only public identifiers belong there.
- Restrict map and other API keys by bundle ID/package name/signature
- Do not trust client-provided prices, fees, roles or payment status
- CORS/CSRF/CSP apply only to the admin web panel and static site

## Location
Store normalized location data. Foreground location only, with explicit permission and a manual-area fallback. Physical-service jobs/providers support latitude/longitude where consent and product requirements allow. Distance queries are indexed and server-controlled.

## Payments
Never mark a payment successful based only on what the app reports. Payment provider webhooks/server verification are authoritative. The app shows a pending state and refreshes from the server. Check Apple and Google payment policy rules for your service types before launch (see Launch Checklist).

## Push Notifications
Devices register tokens with the backend (`POST /devices`). The backend sends through the push service and records delivery failures; invalid tokens are deactivated. Notifications carry a deep-link target. Push is never the only channel for critical events (in-app plus email/SMS back it up).

## Observability
- Structured logs with request ID and app version
- Crash and error tracking in the app and backend
- Health endpoint
- Basic metrics
- Payment/job audit trail

## Scalability
Begin as a modular monolith. Keep domain boundaries clear so services can be separated later if scale requires it.

## Environments
Development, staging and production for the backend. For the app: development build, preview/internal build (pointing at staging), and production build (pointing at production). Use separate bundle IDs/package names or app variants so staging and production can coexist on a phone.

## Environment and Configuration
Backend: MONGODB_URI, JWT secrets, PAYMENT_SECRET_KEY, PAYMENT_WEBHOOK_SECRET, CLOUDINARY secret, maps server key, EMAIL/SMS credentials, push credentials, verification provider keys.
App (public values only): API base URL, payment public key, maps public key (restricted), Sentry DSN, environment name.
Secrets for builds live in EAS secrets or the backend host's secret store. Never commit real values.


---
# 05-ENGINEERING/Acceptance-Criteria.md

# Acceptance Criteria

## Create Job
Given an authenticated customer, they can create a job with required title, category, description, budget and location. Invalid input is rejected. The new job is visible according to its publication status.

## Apply to Job
Given an authenticated provider, the provider can apply to an eligible job. Duplicate applications are prevented. Customer can view the application.

## Hire
Customer can select an application. The job moves to the correct state. Other applications become unavailable/rejected according to business rules.

## Completion
Provider can submit completion. Customer can confirm or raise a dispute. The platform records timestamps and actors.

## Review
Only eligible participants of a completed job can review. Duplicate reviews are prevented. Rating aggregation updates correctly.

## Payment
Payment status must be based on server-side verification/webhook data. Duplicate webhook events must be idempotent.

## Security
A user cannot access another user's private resources. Provider-only/customer-only/admin-only endpoints enforce role permissions.

## Mobile App
App launches on supported iOS and Android versions. Below the minimum supported version, the user sees a blocking update screen. Tokens are stored in secure storage and cleared on logout. The app works from cached data when offline and clearly blocks money actions. Push token registers after login and is removed on logout. Tapping a push notification opens the correct screen from cold start and warm start. Denying location or notification permission never blocks core use. Users can report and block other users. Users can request account deletion inside the app. No secrets are present in the app bundle.


---
# 05-ENGINEERING/QA-Test-Plan.md

# QA Test Plan

## Authentication
- Valid registration
- Duplicate email/phone
- Wrong password
- Expired/invalid session
- Unauthorized endpoint access
- Role escalation attempts

## Marketplace
- Create valid job
- Reject invalid job
- Search by category
- Search by location
- Filter by budget
- Apply once
- Prevent duplicate application
- Hire provider
- Cancel job

## Messaging
- Send message
- Receive message
- Unauthorized conversation access
- Message persistence
- Realtime delivery

## Payments
- Successful payment
- Failed payment
- Duplicate webhook
- Invalid webhook signature
- Refund/dispute state
- Amount tampering attempt

## Reviews
- Eligible review
- Ineligible review
- Duplicate review
- Rating calculation

## Admin
- Admin-only pages
- Moderation
- Dispute resolution
- Audit records

## UX
- Small and large phone screens (iOS and Android)
- Admin web panel on desktop browsers
- Loading states
- Empty states
- Error states
- Slow network
- Accessibility basics

## Launch Gate
No P0 blocker, no known critical security issue, critical payment flows tested, backups/monitoring configured, production environment variables verified.

## Mobile Device and Platform Tests
- Install and first launch on iOS and several Android versions and screen sizes
- Low-RAM/low-end Android device performance
- Network: offline, slow 3G-like, network switch (Wi-Fi to mobile), airplane mode toggle
- App lifecycle: background/foreground, killed and relaunched, low memory
- Push: permission granted/denied, token refresh, foreground/background/cold-start tap, deep link correctness, logged-out deep link
- Permissions: location, camera, photo library, notifications (grant, deny, revoke in settings)
- Keyboard handling on forms and chat
- Image upload: large images, interrupted uploads, unsupported types
- Payment: sandbox success, failure, user cancels, app killed mid-payment, return to app, delayed webhook
- Force update and maintenance mode screens
- Token expiry and refresh during use; revoke device session
- Account deletion and block/report flows
- Accessibility: screen reader labels, large text, contrast, touch targets
- Release builds (not just Expo Go or dev builds); upgrade from previous app version keeps data and sessions
- API compatibility: previous app version against the new backend

## Mobile Launch Gate additions
Tested on real iOS and low-end Android devices; production build tested (not only development); push tested on production credentials; store policy checklist complete (doc 21).


---
# 05-ENGINEERING/Task-Board.md

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


---
# 06-AGENT/Agent-Implementation-Instructions.md

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


---
# 07-PROJECT/Product-Decision-Log.md

# Product Decision Log

## Decision Template
Date:
Decision:
Context:
Options considered:
Chosen option:
Reason:
Impact:
Owner:

## Initial Decisions

### D001 — Marketplace Scope
Decision: Support both digital services and physical/local services.
Reason: The product's differentiation is connecting customers with people who can perform both laptop-based work and hands-on local work.

### D002 — Architecture
Decision: Start with a modular monolith.
Reason: Faster MVP development and easier deployment while preserving domain boundaries.

### D003 — Mobile First (SUPERSEDED by D005)
Original decision: Responsive web first; native mobile apps after product validation.
Status: Superseded on the mobile pivot.

### D004 — Trust
Decision: Verification, ratings, job history and dispute mechanisms are core product capabilities.
Reason: Trust is a central marketplace problem.

Future decisions should be added here before they become hidden assumptions in code.

### D005 — Native Mobile App Instead of Web App
Date: (fill in)
Decision: The customer/provider/business product is a native mobile app for iOS and Android. No customer-facing web app in the MVP. Supersedes D003.
Context: Founders concluded a mobile app suits the product: phone-first users, push notifications, camera and location, and app-store credibility.
Options considered: responsive web app; PWA; React Native/Expo; fully native Swift/Kotlin; Flutter.
Chosen option: React Native with Expo.
Reason: Single codebase for both platforms, strong JS/React skill fit for the founders, EAS for builds and updates, good library support for push, location, camera and secure storage.
Impact: Changes auth (tokens, no cookies), notifications (push), location/permissions, releases (store review, EAS), testing (devices), compliance (app store rules), and the launch checklist. Docs updated across both packs.
Owner: Founders

### D006 — Expo Workflow
Decision: Use Expo Go only for early prototyping; use development builds (EAS) for real feature work; ship via EAS Build/Submit; OTA updates only for JavaScript/asset fixes.
Reason: Expo Go cannot cover all native needs (push, custom config); builds must match production behaviour.

### D007 — Admin as Web Panel (PROPOSED — confirm)
Decision: Admins and moderators use a separate lightweight web panel, not the mobile app.
Reason: Dispute review, moderation and finance work are easier on a desktop; keeps the mobile app focused on customers and providers.
Alternative: admin screens inside the mobile app (more work, harder for heavy workflows).

### D008 — Static Website (PROPOSED — confirm)
Decision: Maintain a small static website for privacy policy, terms, support and account-deletion information, as required by app store listings.

### D009 — Platforms (PROPOSED — confirm)
Decision: Build for iOS and Android together from one codebase; prioritise testing on low-end Android devices because that matches likely user devices (verify with pilot data).

Future decisions should be added here before they become hidden assumptions in code.

### D010 — Project Name: ProCon
Decision: The product is named ProCon (replacing the working name ConnectNaija).
Reason: Founders wanted a unique name.
Open check: availability (OD-18) must be confirmed with CAC, trademark registry, domain, social handles and the app stores before registration and branding spend.
Impact: All documents updated; reserve app name, bundle ID/package name and domain (OD-23) using the new name once availability is confirmed.


---
# 07-PROJECT/README.md

# ProCon

A Nigeria-first **mobile app (iOS and Android)** connecting customers and businesses with trusted people who can provide digital services, skilled trades and local labour.

## Core Idea
Connect people who need work done with people who can do it.

The marketplace is intentionally broader than a traditional freelance platform.

Examples:
- A business needs a website.
- A family needs a plumber.
- An event needs photographers.
- A homeowner needs painters.
- A company needs cleaners.
- A student needs a tutor.
- Someone needs furniture moved.
- A church needs a keyboard player.
- A business needs a social media manager.

## Documentation
See:
- 01-PRD
- 02-MVP
- 03-UX
- 04-TECHNICAL (includes Mobile-App-Architecture.md)
- 05-ENGINEERING
- 06-AGENT
- 07-PROJECT
- 08-BUSINESS to 16-BACKLOG (Pack 2: business, trust, legal, operations, security, launch, agent context, backlog)
- 00-INDEX-and-Open-Decisions.md and 00-CHANGELOG-Mobile-Pivot.md

## Development Principle
Do not begin by building every possible feature. Validate the core marketplace loop:

Customer posts job → providers discover → provider applies → customer hires → work happens → completion → payment → review.

## Suggested Stack
React Native + Expo (TypeScript), Expo Router, EAS
Node.js + Express
MongoDB
REST API
Realtime messaging
Push notifications (Expo/APNs/FCM)
Paystack/Flutterwave
Cloud storage
Maps/location provider
React + Vite web admin panel
Static website for legal/support pages

## Local Development
Exact commands should be added once the repository is initialized. Expected tools: Node.js, Expo CLI/EAS CLI, Android Studio emulator and/or a physical Android phone, Xcode (Mac) or a physical iPhone with a development build. Use Expo Go only for quick early prototyping.

## Environment
Keep secrets in environment variables or EAS secrets. Never commit .env files containing credentials. Anything bundled in the app (including EXPO_PUBLIC_* values) is public; never put secrets there.

## License
To be determined by the project owner.


---
# 08-BUSINESS/01-Business-Requirements-Document.md

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


---
# 08-BUSINESS/02-Market-and-Competitor-Analysis.md

# Market & Competitor Analysis — ProCon

> Status: first-pass desk research. Competitor details come from brief public listings and press items and were NOT verified in depth. Before investing, founders must install and test each competitor app, read their fees/terms, and record findings in section 6.

## 1. Market Summary
Nigeria has a very large informal workforce of artisans, technicians, freelancers and casual labour. Hiring is mostly by referral, WhatsApp groups, Instagram/Facebook and roadside/word-of-mouth. The recurring pain points are trust, price uncertainty, no-shows, poor workmanship, and no recourse when something goes wrong.

## 2. Competitor Landscape (to be validated)

### A. Nigerian home-service / artisan platforms
| Competitor | What public sources say | Relevance |
|---|---|---|
| Gotwork | Positions itself as a NIN-verified artisan marketplace with address verification, reviews, in-app chat and secure payments | Closest on "verified trust" positioning; study their verification UX and fees |
| Clickafix | Lagos-focused app for artisans (plumbing, electrical, AC, generator, beauty, etc.) | Same physical-service categories |
| TaskMoby | Home-service marketplace for cleaners, plumbers, electricians | Booking-style model |
| Get It Done Now | Lagos handyman platform founded 2018 | Longest-running; study lessons and traction |
| Fundichapchap, Home Triangle, others | Tradesperson booking platforms | Smaller players, check activity |
| wrkman | Repositioning in 2026 around accountability and transparency | Shows trust is the contested ground |
| S-MAHII | AI-assisted artisan marketplace launched mid-2026 with location search and in-app negotiation | Newest; watch features |

### B. Global freelance / services marketplaces
Upwork, Fiverr (digital work, USD-oriented), Thumbtack and TaskRabbit (local services, not Nigeria-focused). Strong on process, weak on Nigerian payment, trust and local context.

### C. Informal alternatives (the real competition)
WhatsApp groups, Instagram/Facebook pages, Jiji-style classifieds, personal referrals, roadside artisans. These cost nothing, so ProCon must offer clear added value: verification, protection, reputation, convenience.

## 3. Where ProCon Can Differentiate
1. One platform for digital AND physical AND casual labour (Pack 1 decision D001). Most competitors specialise.
2. Job-posting + application model (customer posts, providers compete) in addition to browsing providers.
3. Business accounts for repeat hiring.
4. Transparent fees and traceable job/payment history.
5. Portable reputation for providers.

Risk: breadth may dilute quality. Mitigation: launch with a small set of categories per city (see doc 04).

## 4. Competitive Threats
- Existing platforms with funding and head start.
- Disintermediation: users agree on-platform then pay cash off-platform. (See docs 03 and 05.)
- Cold start: no providers means no customers and vice versa.

## 5. Validation Plan (do before building payments)
1. Interview 10–15 potential customers: how do they hire today, what went wrong, what would they pay for protection?
2. Interview 10–15 providers across 3–4 categories: how do they get work, would they accept a fee, what do they fear about online payment?
3. Manually test: post 10 real jobs in a WhatsApp group or Facebook group and measure responses (a "concierge MVP").
4. Install the 4–5 closest competitors; complete a booking; record friction, fees, trust cues, payment flow.
5. Record outcomes as decisions in the Decision Log.

## 6. Competitor Test Log (fill in)
| Competitor | Date tested | Categories | Fee model | Verification | Payment/escrow | Strengths | Weaknesses |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

## 7. Market Sizing
Not estimated here. Do bottom-up in the pilot city: number of target households/businesses × expected jobs per year × average job value × fee rate. Replace guesses with interview data.

## 8. Mobile-Specific Competitor Checks
Because ProCon is a mobile app, also record for each competitor: store rating and review count, approximate download range, last update date, app size, recurring user complaints in store reviews, whether they use push notifications and in-app chat, and how long onboarding takes. Complaints in store reviews are a free source of product requirements.

Informal competition also lives inside the phone: WhatsApp, Instagram and Facebook. The app must beat these on speed to first response, not just on trust.


---
# 08-BUSINESS/03-Business-Model-and-Monetization.md

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


---
# 08-BUSINESS/04-Go-To-Market-Strategy.md

# Go-To-Market Strategy — ProCon

## 1. Principle
Marketplaces fail from thin supply or thin demand. Win one small market completely before expanding.

## 2. Launch Scope (OD-05)
- Pick ONE city for physical/local services (where founders live and can meet providers). Candidates: Port Harcourt, Lagos, Abuja.
- Digital services (design, writing, development, marketing, VA, tutoring) can be nationwide because location is not required.
- Start with 4–6 categories, not all 18. Suggested: Cleaning, Plumbing, Electrical, Generator/AC, Painting, plus 1–2 digital categories. Final choice follows interview data.

## 3. Sequence
**Phase A — Validate (before/while building)**
Interviews and a manual "concierge" test from doc 02. Goal: evidence people will pay and providers will join.

**Phase B — Seed supply first**
- Recruit 30–50 providers in the launch categories personally: associations, estates, church/community networks, trade groups, WhatsApp communities, vocational schools.
- Help them build profiles (onboarding call or in-person). Founders' own networks are the first source.
- Offer reduced or zero fee for the first N jobs (decide N), clearly disclosed.

**Phase C — Create demand**
- Founders post real jobs on behalf of friends/family/businesses to get first transactions.
- Target small businesses and event organizers (repeat need, higher job value).
- Content on Instagram, Facebook, WhatsApp status, TikTok: before/after work, provider spotlights, "how to hire safely."
- Referral incentives (e.g., credit) after fee model is stable.

**Phase D — Measure and tighten**
Review KPIs weekly (doc 14). Fix the weakest link: supply, demand, conversion, completion, repeat.

## 4. Positioning
"Hire trusted people for any job — online or in person — with clear prices and protection."
Trust message first: verified badges, reviews, protected payment, dispute help.

## 5. Channels
| Channel | Use |
|---|---|
| WhatsApp communities/broadcasts | Provider recruitment, job alerts |
| Instagram/Facebook/TikTok | Customer awareness, provider spotlights |
| Local partnerships (estate associations, churches, trade unions, schools, co-working spaces) | Trusted introductions |
| SEO landing pages per category/city | Long-term organic |
| Referrals | After product-market fit |

## 6. Provider Onboarding Checklist
Phone verified, profile photo, category and skills, service area, price range, sample work, agreed to rules (doc 08), payout details (when payments live).

## 7. Customer Activation
First job posted within a day of signup; first hire within a week. Remove friction: short job form, category templates, example budgets.

## 8. Metrics for GTM
Providers signed up vs. activated; jobs posted per week; applications per job; hire rate; repeat customers; cost to acquire each side (even if just founder time).

## 9. Budget and Time
Founders' time is the main cost in phases A–C. Track hours as a cost.

## 10. Expansion Rule
Expand to a new city or category only when: completion rate and rating are healthy, disputes are manageable, and supply in the current market exceeds demand.

## 11. Mobile Distribution Plan
**Install friction is the main new problem.** People must find, download and open the app before they can hire.
- Share install links through WhatsApp, Instagram bios, QR codes at partner locations, and provider business cards.
- Use one smart link (website landing page) that routes to the App Store or Google Play based on device.
- Support deep links so a shared job or provider profile opens in the app (or the store if not installed).
- Keep the app small and the first launch fast; browsing categories before signup reduces drop-off.
- Closed beta first: TestFlight (iOS) and Google Play closed testing (Android). Collect feedback in a WhatsApp group.
- Store listing basics: clear name, short description, screenshots that show the job flow, privacy policy link, support email, consistent keywords for category and city.
- Ask happy users for store ratings after a successful completed job (not at first launch).
- Track installs, install-to-signup, signup-to-first-job; compare with channel.
- Provider onboarding: do it in person with the provider's own phone, because many first-time users need help installing and verifying.
- Data cost: tell users the app is light on data; offer image compression.

## 12. Web Presence
A small website is still needed: landing page with download links, privacy policy, terms, support contact, account-deletion instructions, and SEO pages later.


---
# 09-TRUST-SAFETY/05-Trust-Safety-and-Verification-Spec.md

# Trust, Safety & Verification Specification

Pack 1 decision D004: verification, ratings, job history and disputes are core capabilities.

## 1. Trust Layers
1. Identity signals (verification levels)
2. Reputation (reviews, completed jobs)
3. Transaction protection (payment hold, disputes — docs 06, 07)
4. Behaviour controls (rules, reporting, moderation — doc 08)
5. Admin oversight (audit logs — doc 11)

## 2. Verification Levels
Stored on User.verificationStatus (Pack 1). Proposed enum values and badges:

| Level | Requirement | Badge shown |
|---|---|---|
| L0 Unverified | Account created | none |
| L1 Contact verified | Phone OTP verified and email verified | "Contact verified" |
| L2 ID verified | Government ID check through a third-party verification provider (e.g., NIN-based) matched to name | "ID verified" |
| L3 Enhanced (post-MVP) | Address verification, guarantor, trade certificate, background check where legally supported | "Verified pro" |

MVP requires L1 to apply for or post jobs. L2 is strongly encouraged for providers and required (proposed) before receiving payouts above a configurable threshold. Decide with OD-04.

Rules:
- Badges describe exactly what was checked. Never imply "background checked" if only phone was verified.
- Verification is done by a regulated third-party provider via server-side API. Never accept a client claiming "verified".
- Store minimum data: result, provider reference, timestamp, level. Do not store raw ID numbers or images unless legally required and secured (see doc 09). Treat government ID numbers as highly sensitive.
- Name on ID must reasonably match profile name and payout account name.
- Users can request re-verification; admin can revoke.

Proposed schema additions (User or separate Verification collection):
`verificationLevel`, `verifiedAt`, `verificationProviderRef`, `verificationMethod`, `verificationRevokedAt`, `verificationRevokedReason`.

## 3. Provider Quality Signals
Show on provider cards/profile: verification badge, rating average and count, completed jobs, member since, response time (post-MVP), category/skills, portfolio, service area.
Ratings display "N/A" until at least 1 review; do not show a misleading 0.0.

## 4. Fraud and Abuse Scenarios
| Scenario | Controls |
|---|---|
| Fake provider profiles | Phone/email verification, ID check before payout, admin review queue, reports |
| Stolen/misused identity | Name matching, third-party check, payout-account name match |
| Scam jobs (fake customers) | Rate limits, payment-before-start, report/suspend, admin flags |
| Off-platform payment | Hide contact until hire, message filtering, ToS enforcement |
| Review manipulation | Only eligible participants of a Completed job can review; one review per party per job; double-blind reveal; anomaly flags |
| Payment fraud/chargebacks | Server-verified webhooks, provider fraud tools, hold period, amount checks |
| Harassment/unsafe behaviour | Report button on users/messages/jobs, admin suspension, evidence retention |
| Illegal/prohibited services | Prohibited list (doc 08), keyword flags, admin removal |
| Duplicate/sock-puppet accounts | Unique phone/email, device/IP signals (post-MVP) |

## 5. Physical-Safety Considerations
Physical jobs involve people entering homes/sites. MVP measures:
- Show provider verification level to customer before hire.
- Share provider's name/photo (verified) with the customer; share job address with provider only after hire (precise address) — before hire show approximate area.
- In-app safety tips and a "report a safety concern" action on active jobs.
- Optional (post-MVP): trusted-contact sharing, check-in/check-out, emergency contact button.
- Admin can immediately suspend an account during a safety investigation.

## 6. Contact Information Policy (OD-13)
- Before hire: no phone numbers/emails/links in public job descriptions or pre-hire messages. Detect common patterns (digits strings, "whatsapp", email/URL formats) and warn or block.
- After hire: allow in-app calling/messaging; direct contact details may be revealed if product wants (decide).
- Never block users from reporting.

## 7. Moderation Triggers (automatic flags to admin queue)
Multiple reports against one account; new account with high-value jobs; repeated cancelled jobs; payment failures; message patterns matching scams; rating drop; many applications in short time; mismatch of name vs payout account.

## 8. Account Actions
Warn → restrict (cannot apply/post) → suspend (temporary) → ban (permanent). Each action requires a reason code, admin ID, timestamp, and an audit log entry. Users get a notification and an appeal path (support email/form).

## 9. Acceptance Criteria
- A user with L0 cannot apply or post jobs.
- Only server-side verification updates verification levels.
- Badge text matches verification method.
- Suspended users cannot log in to act or are restricted per status; active contracts are flagged for admin handling.
- All moderation actions create audit log entries.

## 10. Mobile and App Store Safety Requirements
Apps with user-generated content (messages, reviews, profiles, job posts) are expected by the app stores to provide: a way to filter or flag objectionable content, a way for users to report content and users, a way to block abusive users, timely handling of reports, and published contact information. Treat these as MVP requirements, not extras.
- **Block user:** hides the blocked user's profile from search for the blocker, prevents new messages/applications between them, keeps existing contract data for dispute purposes.
- **Report:** reachable from profile, job, message and review screens (Report model).
- **Content flagging:** keyword/pattern flags for abusive or prohibited content go to the admin queue.
- **Reviewer access:** stores will review the app; prepare a demo account and clear in-app rules.
- **Device-level controls:** log out of other devices, revoke sessions on suspension, deactivate push tokens on suspension.
- **Camera/photo uploads:** moderate profile and job images (report path now, automated checks later).


---
# 09-TRUST-SAFETY/06-Payment-and-Escrow-Spec.md

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


---
# 09-TRUST-SAFETY/07-Dispute-and-Refund-Policy-Spec.md

# Dispute & Refund Policy Specification

Aligned with Pack 1 Dispute Flow: open dispute → reason → evidence → job/payment flagged → admin review → decision → refund/release/other → audit log. Job state `Disputed` and Dispute model exist in Pack 1.

## 1. Principles
Fair, evidence-based, fast, documented, consistent. Both parties are heard. Decisions are reasoned and recorded.

## 2. Who Can Open a Dispute
The customer or provider on a job in In Progress, Submitted for Completion, or within 7 days after Completed/Cancelled (window is configurable). Only one open dispute per job.

## 3. Reason Codes (Dispute.reason)
Customer-opened: work not started/no-show; work incomplete; poor quality/not as described; damage or safety issue; provider asked for off-platform payment; extra charges demanded.
Provider-opened: customer unresponsive after completion; customer refuses to confirm; scope changed unfairly; access denied/no-show at site; abuse/harassment; payment problem.
Others: fraud suspicion; other (free text).

## 4. Process and SLAs (OD-15 defaults)
1. **Open** — user selects reason, writes description, attaches evidence (photos, screenshots, chat excerpts auto-attached). Job → Disputed; payment flagged; auto-release paused.
2. **Notify** — other party notified and gets 48 hours to respond with their account and evidence.
3. **Review** — admin reviews timeline, messages, evidence, ratings history. May request more information (clock paused).
4. **Decision** — within 5 business days of the response (or no-response deadline). Admin records decision, reasoning, and amounts.
5. **Execute** — system performs release/refund/partial split, updates states, notifies both.
6. **Close** — dispute closed; optional one appeal within 7 days to a second admin.
First admin acknowledgement target: 24 hours.

## 5. Possible Outcomes (Dispute.resolution)
| Outcome | Effect |
|---|---|
| Release in full to provider | Payment → Released; job Completed |
| Refund in full to customer | Payment → Refunded; job Cancelled |
| Partial split | Part refunded, part released; fee on released portion only |
| Redo/fix period | Dispute paused up to N days for provider to correct work; then re-review |
| No action/dismissed | Dispute closed; original flow resumes |
| Account action | Warning/suspension per doc 05 |

## 6. Cancellation & Refund Defaults (OD-09 — proposed, adjust after interviews)
| Situation | Default result |
|---|---|
| Customer cancels before provider starts, before agreed start time by more than 24h | Full refund |
| Customer cancels within 24h of start | Refund minus a configurable cancellation fee paid to provider (e.g., small %) |
| Provider cancels or no-shows | Full refund to customer; provider reliability counted; repeated issues → account action |
| Job started, then cancelled by mutual agreement | Split by agreement, recorded in-app |
| Job started, unilateral cancel | Goes to dispute |
| Payment failed/expired | No charge; contract not activated |
Platform fee is not retained on fully refunded jobs.

## 7. Evidence Requirements
- Accepted: images, short video, PDFs, chat records, receipts, location/time data if consented.
- Evidence stored securely, access limited to parties and admins; retained per doc 09.
- Admin sees complete message history for the job. Users are told this in the ToS.

## 8. Decision Guidelines for Admins
Check: Was scope agreed in writing in-app? Did both parties communicate in-app? Evidence of delivery? Timeline compliance? Prior behaviour? Prefer proportionate outcomes; avoid all-or-nothing when partial work is evident. Use decision templates; require a reason code and written rationale.

## 9. Anti-abuse
Limit disputes per user per period; flag users with high dispute rates; flag users with repeated losses; penalize false claims.

## 10. Data Model Notes
Pack 1 Dispute has: id, jobId, openedBy, reason, evidence, status, resolution, resolvedBy, resolvedAt.
Proposed additions: `reasonCode`, `description`, `respondentResponse`, `respondentEvidence`, `responseDeadline`, `resolutionAmounts` (refund/release), `adminNotes` (internal), `appealStatus`, `timeline[]`.
Dispute statuses (proposed): Open → Awaiting Response → Under Review → Resolved → Appealed → Closed.

## 11. Acceptance Criteria
- Opening a dispute blocks payment release and auto-release timer.
- Both parties can submit evidence until the deadline.
- Only admins can resolve; all decisions require a reason and create audit logs.
- Resolution amounts never exceed the held amount.
- Users receive notifications at each stage.

## 12. Mobile Notes
- Evidence capture: allow taking photos/video directly in the app, with compression and a size limit; show upload progress and allow retry; store with the dispute record.
- Push and in-app notifications at each dispute stage; email as backup (doc 12). The response deadline countdown must be visible in the app.
- Users who delete their account while a dispute is open: deletion is deferred until the dispute and payment are settled.
- Blocked users can still respond in an existing dispute.


---
# 09-TRUST-SAFETY/08-Marketplace-Rules-and-Community-Guidelines.md

# Marketplace Rules & Community Guidelines

Plain-language rules shown to users at signup and linked from the footer. Legal wording is finalised by a lawyer in the Terms of Service (doc 10). These rules also drive admin moderation (doc 11).

## 1. Core Rules for Everyone
1. Be honest: real name, real photo, accurate skills, accurate job descriptions.
2. One person, one account. Do not share accounts.
3. Be respectful. No harassment, threats, hate speech or discrimination.
4. Keep communication and payment on ProCon for jobs found here.
5. Do not post or request personal contact details publicly or before hire.
6. Follow the law. No illegal services.
7. Do not manipulate reviews (fake, paid, retaliatory, or traded).
8. Protect others' privacy: do not share photos/addresses/personal data without consent.

## 2. Customers Must
Describe jobs accurately, state a realistic budget, respond to providers, provide access/materials as agreed, pay through the platform, confirm completion honestly, and treat providers with respect.

## 3. Providers Must
Show up on time or communicate early, do the work as agreed, price honestly (no surprise charges), use safe practices and valid tools/materials, keep work and certifications accurate, never ask for off-platform payment, and never subcontract identity (the verified person does the work, or disclose helpers).

## 4. Businesses Must
Provide a real business identity, honour milestones/payment terms, and not use the platform to recruit as employees outside its purpose (full employment/payroll is out of scope).

## 5. Prohibited Content and Services (MVP list; legal to finalize)
- Anything illegal in Nigeria
- Weapons, drugs, counterfeit goods
- Sexual/adult services and exploitative content
- Academic dishonesty services (writing exams, impersonating students)
- Fake documents, certificates, IDs; fraud, hacking, phishing
- Gambling, betting-promotion, pyramid/Ponzi schemes, "get rich" schemes
- Services that endanger people (unsafe electrical/gas work by unqualified people, etc.)
- Spam, misleading advertising, and unrelated sales listings
- Any request to work for free "exposure" disguised as a job (review case by case)
- Child labour or anything involving minors in unsafe/inappropriate work

## 6. Prohibited Behaviour
Circumventing fees; pressuring for off-platform payment; creating multiple accounts after a ban; impersonation; spamming applications; scraping; abusing disputes; threatening reviews; sharing malware; attempting to hack/test the platform without permission.

## 7. Reviews
Only for completed on-platform jobs. Reviews must be honest and about the work/behaviour. No personal data, no abuse, no threats. Reviews may be removed if they violate rules. Reviews are revealed after both are submitted or after the review window (OD-17).

## 8. Reporting
Every profile, job, message and review has a "Report" action. Reasons: scam/fraud, harassment, unsafe, inappropriate content, fake profile, off-platform request, other. Reports go to the admin queue (Report model). Reporter identity is not revealed to the reported user.

## 9. Enforcement Ladder
Warning → temporary restriction → suspension → permanent ban. Severe cases (fraud, violence, threats, child safety) skip steps. Users can appeal via support (doc 11).

## 10. Safety Tips (show in-app)
Verify the provider's badge; keep chat in-app; do not pay outside the platform; share exact address only after hire; inspect work before confirming; report concerns immediately; for emergencies contact local emergency services, not ProCon.

## 11. App-Specific Notes
- Rules are shown during signup and available in Settings.
- Users can report and block from profiles, jobs, messages and reviews.
- Photos uploaded from the camera/gallery must not contain other people's private information without consent, nudity, violence or illegal material.
- Using screenshots of conversations as evidence is allowed in disputes; sharing them publicly to harass someone is not.


---
# 10-LEGAL/09-Privacy-and-Data-Requirements.md

# Privacy & Data Requirements

> Not legal advice. Have a Nigerian data-protection lawyer review before launch. The main law referenced is the Nigeria Data Protection Act 2023 (NDPA), regulated by the Nigeria Data Protection Commission (NDPC). Confirm current obligations (registration, audits, thresholds, breach timelines) with a lawyer or the NDPC.

## 1. Roles
ProCon (the company) is the **data controller** for user data. Payment, SMS, verification, hosting and maps vendors are **data processors**; sign data-processing terms with each.

## 2. Personal Data Inventory
| Data | Source | Purpose | Sensitivity |
|---|---|---|---|
| Name, email, phone, password hash | Registration | Account, login, communication | Normal |
| Profile photo, bio, skills, portfolio | Provider/customer | Marketplace display | Normal |
| Location (service area, job address, optional lat/lng) | User | Matching, delivery of service | High |
| Verification result/reference; ID details | Verification provider | Trust | High — minimise |
| Messages and attachments | Users | Job coordination, dispute evidence | Medium–High |
| Payment references, payout bank details (tokens) | Gateway | Payments | High |
| Reviews, ratings | Users | Reputation | Normal |
| Device ID, push token, app version, OS, device model, IP, logs | App/System | Notifications, security, debugging, compatibility | Normal–Medium |
| Device permissions: location, camera/photos, notifications | User choice | Features | High (location) |
| Crash/diagnostic and analytics data | SDKs | Stability, product improvement | Normal–Medium |
| Reports/disputes/evidence | Users/admin | Safety, resolution | High |

Do not collect data without a stated purpose. Do not collect special-category data (health, religion, etc.) unless essential.

## 3. Lawful Basis and Consent
- Contract: needed to run accounts, jobs, payments.
- Legitimate interest: fraud prevention, security, service improvement (document the balance).
- Legal obligation: tax/accounting records, lawful requests.
- Consent: marketing messages, optional precise location, optional analytics/cookies. Must be freely given, specific, withdrawable, and recorded (timestamp, version).
Show a privacy notice at signup and a link in the footer. Version the notice and record acceptance.

## 4. User Rights (build the capability)
Access/copy of data; correction; deletion (subject to legal retention); objection to processing/marketing; withdrawal of consent; data portability where applicable; complaint route. Provide a settings page and a contact email for requests; respond within the legal timeframe (confirm with lawyer).
Proposed endpoints (post-MVP acceptable if manual process exists at launch): `POST /users/me/data-export`, `POST /users/me/delete-request`.

## 5. Retention Schedule (proposed — confirm with lawyer/accountant)
| Data | Retain |
|---|---|
| Account data | While active + a set period after deletion request for legal/dispute needs |
| Financial/transaction records | Per tax/accounting law (commonly multiple years; confirm) |
| Messages | While job exists + dispute window + a set period; then delete/anonymise |
| Dispute evidence | Until resolved + appeal window + a set period |
| Verification data | Keep result and reference; delete raw documents quickly or never store |
| Logs | Short rolling period (e.g., 90 days) |
| Marketing consent records | As long as needed to prove consent |

Deletion = remove or anonymise personal data while keeping legally required financial records and reviews in anonymised form (e.g., "Former user").

## 5b. Data Location and Transfers
Hosting, storage, maps and email vendors may be outside Nigeria. Choose vendors with adequate safeguards; document cross-border transfers and include them in the privacy notice. Confirm NDPA transfer rules with a lawyer.

## 6. Security of Personal Data
See doc 15. At minimum: encryption in transit (HTTPS), encryption at rest where supported, access control by role, least privilege for admins, audit logs for admin access to personal data, secrets in environment variables, backups encrypted.

## 7. Breach Response
Maintain an incident plan: detect, contain, assess, notify the regulator and affected users within the legally required time (confirm timeline with lawyer), document, fix. Assign an incident owner among founders.

## 8. Tracking, SDKs and Cookies
The app does not use cookies; the static website and admin panel may. Use only necessary tracking at MVP plus consent-based analytics. List every SDK (analytics, crash reporting, maps, payments, push) with what data it collects. Avoid selling or sharing data for advertising. Provide a cookie notice on the website.

## 9. Children
18+ only (OD-07). Block signup if age confirmation is declined. Do not knowingly collect children's data; delete if discovered.

## 10. Product Requirements
- Privacy notice + consent checkbox at registration (versioned).
- Data minimisation: public profile shows only needed fields; never expose email/phone/exact address publicly.
- Precise job address visible only to the hired provider.
- Admin access to messages/ID data is restricted and logged.
- Data-subject request tracker (even a simple admin screen/spreadsheet).
- Delete/anonymise workflow documented and tested.
- **In-app account deletion** (Settings → Delete account) that triggers the same backend workflow; the stores expect it, and a web page explaining deletion must also be available.
- **Permission strings** (iOS usage descriptions, Android permission rationale) that honestly state why location, camera, photos and notifications are needed.
- **Store privacy disclosures:** Apple App Privacy ("nutrition label") details and Google Play Data safety form must match the actual data collected, including by third-party SDKs. Keep an internal data inventory (above) as the single source for both.
- **Push token handling:** treat as personal data; delete on logout/account deletion.
- **Local device storage:** no personal data in plain storage; clear on logout.
- Vendor list with purposes and agreements maintained.

## 11. Proposed Schema Additions
`consents[]` (type, version, acceptedAt, ip), `privacyNoticeVersion`, `deletionRequestedAt`, `anonymisedAt`.

## 12. Launch Gate
Privacy notice published, vendors listed, retention/deletion process documented, lawyer review complete, registration/compliance obligations with NDPC checked.

## 13. Mobile Launch Gate additions
Privacy policy URL live and linked in store listings and inside the app; store privacy forms completed from the data inventory; account deletion works in-app and is documented on the website; SDK list reviewed.


---
# 10-LEGAL/10-Terms-of-Service-Requirements.md

# Terms of Service (ToS) Requirements

> This is a requirements outline for the lawyer who drafts the real ToS. It is not the legal text. Final documents must be reviewed by a Nigerian lawyer before launch.

## 1. Documents Needed Before Launch
1. Terms of Service (general)
2. Privacy Notice (doc 09)
3. Marketplace Rules / Community Guidelines (doc 08)
4. Payment, Fees & Refund Terms (docs 03, 06, 07)
5. Provider Terms (additional terms for providers)
6. Cookie Notice
Optional: Business Account Terms; Referral/Promotion Terms.

## 2. Key Topic Checklist
| Topic | Requirement |
|---|---|
| Parties and definitions | Company legal name/registration number; definitions of Customer, Provider, Business, Job, Contract, Platform Fee |
| Platform role | ProCon is a marketplace/intermediary; it does not employ providers and is not a party to the service contract unless stated. Clarify limited responsibility for work quality, with the dispute process as the remedy |
| Eligibility | 18+, legal capacity, accurate information, one account |
| Provider status | Independent contractors, not employees; responsible for tools, taxes, permits, insurance, safety |
| Accounts | Security duties, suspension/termination rights, appeals |
| Verification | What badges mean and don't mean; no guarantee of character or competence |
| Fees | Rates, who pays, when charged, taxes, changes with notice; fee snapshot per job |
| Payments | Payments via licensed processor; how funds are held/released; payout conditions; payout details accuracy; failed payments; chargebacks |
| Cancellations/refunds | Rules from doc 07 |
| Disputes | Process, evidence, admin decision, appeal, binding effect on payment release, limits |
| Circumvention | No taking on-platform relationships off-platform to avoid fees (reasonable scope/time) |
| Content and licence | Users own their content; grant the platform a licence to display/operate; responsibility for uploads; IP infringement process |
| Reviews | Rules, removal rights |
| Prohibited items/behaviour | Reference doc 08 |
| Safety | Users responsible for on-site safety; emergency disclaimer |
| Liability | Limitation of liability and disclaimers, drafted to be enforceable under Nigerian consumer-protection law |
| Indemnity | Users indemnify for breach/illegal acts |
| Communications | Consent to in-app, email, SMS notices; marketing opt-out |
| Data/privacy | Link to privacy notice; admin access to messages for disputes/safety |
| Changes to terms | Notice period; acceptance by continued use or re-consent for material changes |
| Governing law | Nigerian law; courts/arbitration clause as lawyer advises |
| Contact | Support email/address, complaint process |

## 3. Provider Terms Extras
Independent contractor status; accurate credentials; licensing/permit responsibilities for regulated trades; insurance recommendations; tax responsibility; conduct on client premises; subcontracting rules; payout account ownership; fee deduction authorisation.

## 4. Consumer-Protection Alignment
Check requirements under Nigerian consumer-protection law (FCCPC and related rules) for clear pricing, fair terms, complaint handling and refund transparency. Avoid hidden fees and unfair clauses.

## 5. Product Requirements Derived from ToS
- Registration must require explicit acceptance of ToS + Privacy Notice (checkbox, not pre-ticked). Store version, timestamp, IP.
- Re-acceptance flow when terms change materially.
- Terms and Privacy pages publicly accessible (static website) and linked inside the app (signup, Settings, checkout) and in both store listings.
- Fee disclosure UI on application, hire and payment screens.
- Provider onboarding requires acceptance of Provider Terms.
- Admin can see which terms version a user accepted.

Proposed schema addition: `termsAcceptances[]` (document, version, acceptedAt, ip).

## 6. Handoff Package for the Lawyer
Pack 1 + Pack 2 docs 03, 05, 06, 07, 08, 09; list of vendors; the company's registration details; answers to the open decisions OD-01, OD-02, OD-05 to OD-10.

## 7. App-Specific Terms Topics
- Licence to use the app; no reverse engineering, scraping or automated access.
- Acceptance of Apple's and Google's applicable app-store terms where required; check whether the stores' standard end-user terms are enough or custom terms are needed.
- App versions: right to require updates and to stop supporting old versions.
- Permissions: users control device permissions; features that need them may be limited if denied.
- Push/SMS consent for transactional messages; marketing opt-in separately.
- In-app account deletion and consequences (active jobs, payments, retention).
- User-generated content rules, reporting, blocking and moderation (aligns with store requirements).
- Support contact details (email) must be accurate and published.


---
# 11-OPERATIONS/11-Admin-and-Operations-Manual.md

# Admin & Operations Manual

Applies to the admin screens in Pack 1 (Dashboard, Users, Providers, Jobs, Categories, Reports, Disputes, Transactions, Verification, Audit logs, Settings).

## 1. Admin Roles (proposed RBAC)
| Role | Permissions |
|---|---|
| Super Admin (founders) | Everything including settings, fees, admin management |
| Moderator | Review reports, hide/remove content, warn/suspend users, no financial actions |
| Support Agent | View users/jobs/messages as needed for tickets, add notes, no refunds |
| Finance Admin | View transactions, approve refunds/payout retries, reconciliation |
| Dispute Resolver | Review and decide disputes within limits; second admin for appeals |
Principle: least privilege; every admin action is audit-logged (adminId, action, target, before/after, reason, timestamp, IP).

## 2. Daily Routine
1. Check dashboard: new users, jobs, payments, failed payments, open disputes, reports.
2. Clear the Reports queue (target: first action within 24h; urgent safety flags immediately).
3. Review verification queue.
4. Review disputes nearing SLA.
5. Check failed webhooks/payouts and reconciliation alerts.
6. Respond to support messages.
7. Review flagged accounts/jobs (doc 05 triggers).

## 3. Weekly Routine
KPI review (doc 14), category/pricing sanity checks, top complaints, provider quality review (low ratings/no-shows), backups and monitoring check, update Decision Log and Risk Register.

## 4. Procedures
**Moderating a report**
1. Open report → view target and context.
2. Decide: dismiss / warn / remove content / restrict / suspend / ban / escalate.
3. Select reason code; add internal note.
4. System notifies affected user; logs action.

**Reviewing verification**
Confirm provider result matches name/profile; handle mismatches by requesting resubmission; approve/reject; record reason.

**Resolving a dispute**
Follow doc 07 timeline. Never decide without reading messages and evidence. Record rationale and amounts. Use a second admin for appeals and for amounts above a configurable threshold.

**Refunds and payout issues**
Only Finance Admin/Super Admin. Verify payment status on the gateway dashboard. Record reference, reason. Never promise refunds outside policy.

**Suspending a user**
Check active jobs/payments first. Flag affected contracts. Notify the counterparty with neutral wording. Do not delete data; set status.

**Category management**
Add/rename/deactivate categories (never hard-delete if jobs reference them). Set type digital/physical/both.

**Data requests**
Log request, verify identity, perform export/deletion/anonymisation per doc 09, record completion.

## 5. Support
- Channels (MVP): support email + in-app contact form + optional WhatsApp business number.
- Templates for: verification failed, report outcome, dispute updates, refund timing, account suspended, how fees work.
- SLA: first response within 24h (business days).
- Ticket tracking: simple shared spreadsheet or helpdesk tool; log ID, user, issue type, owner, status.

## 6. Escalation
| Severity | Examples | Response |
|---|---|---|
| Critical | Safety threat, data breach, payment bug, site down | Immediately; founder on call |
| High | Fraud, stuck payments, high-value dispute | Same day |
| Medium | Standard disputes/reports | Within SLA |
| Low | Questions, feature requests | Weekly batch |

## 7. Admin Security
Unique accounts, strong passwords + MFA (required for Super Admin, Finance), no shared logins, session timeout, IP/device alerts, remove access when roles change, periodic permission review.

## 8. Operations Metrics
Report backlog, median time to first action, dispute resolution time, verification turnaround, refund count/value, repeat offenders.

## 9. Runbooks (create when infrastructure exists)
Site down; database restore; payment webhook failing; email/SMS provider failing; suspected breach; rollback deployment.

## 10. Acceptance Criteria
- Admin-only routes enforce RBAC; moderators cannot access finance actions.
- Every admin mutation creates an audit log entry.
- Suspending a user flags their active contracts.
- Admin views of messages/ID data are logged.

## 11. Mobile Operations Additions
- **Admin interface:** a web panel (D007). Admins never need the mobile app for moderation, disputes or finance.
- **App config control:** Super Admin can set minimum supported version per platform, latest version message and maintenance mode. Setting minimum version incorrectly locks users out, so require a second confirmation and test with a staging build.
- **Release management:** keep a release log (version, build number, date, store status, changes, OTA vs store build). Roll out gradually; watch crash-free rate before expanding.
- **Store reviews and ratings:** check weekly; reply politely to reviews; feed recurring complaints into the backlog.
- **Store review issues:** if a build is rejected, record the reason and fix before resubmitting; keep a reviewer demo account working.
- **Push monitoring:** watch push delivery failures and invalid-token rates.
- **Support triage for app problems:** collect app version, platform, OS version, device model and a screenshot; check crash reports.
- **Runbooks to add:** bad release rollback (disable via config or ship hotfix/OTA), push provider failure, store rejection, forced-update misconfiguration.


---
# 12-PRODUCT-SPECS/12-Notification-Specification.md

# Notification Specification

Aligned with Pack 1 Notification model (id, userId, type, title, body, readAt, createdAt).

## 1. Channels
| Channel | Use | MVP |
|---|---|---|
| In-app (bell + list) | All events | Yes |
| Email | Account, receipts, key job/payment events | Yes |
| SMS | OTP, critical alerts (payment, hire, dispute) — cost-controlled | Yes (limited) |
| **Push (mobile, Expo push over APNs/FCM)** | Messages, applications, hires, payments, disputes, reminders | **Yes** |
| WhatsApp | Possible later via business API | Post-MVP |

Push is the primary real-time channel for the app. Because users can disable push or the token may be invalid, critical events (payments, hires, disputes, security) must also be in-app and backed by email or SMS.

## 2. Principles
Useful, not noisy. Short, clear, actionable. Respect preferences. Never include sensitive data (full address, bank details, OTP reuse) in email/SMS bodies beyond what's needed. Every notification deep-links to the relevant screen.

## 3. Event Catalogue
| Event | Recipient | In-app | Email | SMS |
|---|---|---|---|---|
| Account created / verify email | User | Y | Y | |
| Phone OTP | User | | | Y |
| Password reset | User | | Y | |
| Verification approved/rejected | Provider | Y | Y | |
| New job matching provider's categories/area | Provider | Y | digest | |
| New application received | Customer | Y | Y | |
| Application viewed/shortlisted | Provider | Y | | |
| Application accepted | Provider | Y | Y | Y |
| Application rejected/job filled | Provider | Y | | |
| Hire created, payment required | Customer | Y | Y | |
| Payment successful (held) | Customer, Provider | Y | Y | Y (provider) |
| Payment failed | Customer | Y | Y | |
| New message | Recipient | Y | Y if unread after X minutes | |
| Job started / completion submitted | Customer | Y | Y | |
| Completion confirmed / payment released | Provider | Y | Y | Y |
| Auto-release reminder (before window ends) | Customer | Y | Y | |
| Job cancelled | Counterparty | Y | Y | |
| Dispute opened / response needed | Counterparty | Y | Y | Y |
| Dispute updated / resolved | Both | Y | Y | |
| Review reminder | Both | Y | Y | |
| New review received | Reviewee | Y | | |
| Report outcome | Reporter | Y | | |
| Account warning/suspension | User | Y | Y | |
| Payout sent/failed | Provider | Y | Y | Y (failed) |
| Terms/privacy update | All | Y | Y | |

## 4. Preferences
Users can toggle email and marketing notifications. Transactional/security/payment/legal notices cannot be turned off. Marketing requires opt-in consent.
Proposed schema: `User.notificationPreferences` { emailJobs, emailMessages, emailMarketing, smsAlerts }.

## 5. Rules
- Batch low-priority notifications (e.g., daily job digest for providers).
- Message email only if unread after a delay; avoid email-per-message.
- Rate-limit per user per hour. De-duplicate identical events.
- Store every notification in-app even if email/SMS fails.
- Retry failed email/SMS with backoff; log final failure.
- Quiet hours for non-critical SMS (e.g., no marketing at night).
- Localisation-ready: copy stored as templates with variables, English first; keep room for Pidgin/Yoruba/Hausa/Igbo later.

## 6. Template Format
`type`, `title`, `body` with variables `{{name}}`, `{{jobTitle}}`, `{{amount}}`, `{{link}}`. Keep SMS ≤ 160 chars where possible. Include brand name in SMS.

## 7. Technical Notes
Create a `NotificationService` with `notify(userId, eventType, payload)`. Event types are constants. Delivery handled by queue/worker where available; otherwise async calls with error handling. Real-time in-app delivery through the existing realtime layer (Socket.IO or equivalent).

Proposed API additions: `GET /notifications`, `PATCH /notifications/:id/read`, `POST /notifications/read-all`, `GET/PATCH /users/me/notification-preferences`.

## 7b. Mobile Push Rules
- Ask for notification permission at a meaningful moment (for example after posting the first job or applying), with a short explanation first. On iOS, a denied prompt can only be re-enabled in system settings, so do not waste the one prompt on first launch.
- Android: create notification channels (Messages, Job updates, Payments, Reminders, Marketing) so users can control each.
- Every push carries a deep-link target and an event ID for de-duplication.
- Payload contains minimal content; no full addresses, amounts beyond what's needed, or OTP codes.
- Update badge count from unread in-app notifications.
- Register token via `POST /devices` after login and on token change; deactivate on logout, on invalid-token errors, and on account deletion.
- When a user has the conversation open in the foreground, suppress the push for that conversation.
- Handle cold-start taps: the app must route to the right screen after login and data load.
- Monitor delivery errors from the push service and track opt-in rate.

## 8. Acceptance Criteria
- Each event in the catalogue creates the specified in-app notification and, where listed, a push to registered active devices.
- Push tap opens the correct screen from killed, background and foreground states.
- Unread count updates in real time.
- Users cannot read others' notifications.
- Email/SMS failure does not break the main transaction.
- Transactional notices ignore marketing opt-out; marketing respects it.


---
# 12-PRODUCT-SPECS/13-Search-and-Matching-Specification.md

# Search & Matching Specification

Pack 1 puts "Complex AI matching" out of scope for MVP. MVP search is rule-based and transparent. This doc defines it and prepares for later ranking.

## 1. Search Surfaces
1. Job search/feed (providers find jobs)
2. Provider search/browse (customers find providers)
3. Category browse
4. Global search box (keywords → jobs/providers/categories)

## 2. Job Search
Filters: category/subcategory, keywords, budget range, location/distance, posted date, schedule/date needed, type (digital/physical/both), remote vs on-site.
Sort: newest (default), nearest (for physical), highest budget, closing soon.
Hide: draft, cancelled, filled/in-progress jobs, jobs from suspended customers, jobs a provider already applied to (or mark clearly).

## 3. Provider Search
Filters: category, skills, location/service area, rating minimum, verification level, price range, availability, completed-jobs minimum.
Sort: best match (default), rating, nearest, most completed jobs.
Show: only active, non-suspended providers with completed profiles and at least L1 verification.

## 4. Location Handling (Pack 1 requirement)
- Store normalised address: country, state, LGA/city, area/neighbourhood, optional geo point (lat/lng).
- Use a MongoDB `2dsphere` index on geo points; distance queries run on the server only.
- Providers define a service area: radius from a point and/or list of LGAs/areas.
- Customers' exact address is never public. Show approximate area/distance band (e.g., "within 5 km") until hire.
- Geolocation consent: explain first, then ask for foreground permission through the OS prompt; allow manual area selection if denied. Never require GPS. Do not track location in the background. On iOS, offer approximate location as acceptable.
- Digital jobs ignore distance.
- Abstract the maps/geocoding provider behind a `LocationService` (OD-12). Cache geocoding results.
- Nigerian address realities: informal addresses and landmarks; support free-text "landmark/nearby" field plus area/LGA selection.

## 5. Matching Logic (rule-based, MVP)
When a job is published, compute eligible providers:
1. Provider category matches job category.
2. Provider active, verified at required level, not suspended.
3. Physical jobs: job within provider service area; digital: no distance rule.
4. Provider available (if availability set).
5. Budget fit (soft): flag if job budget is far below provider's stated pricing.
Notify eligible providers (doc 12) with limits per provider per day.

**Relevance score (for "best match" ordering)** — weights are configurable and should be tuned later:
`score = categoryMatch*40 + skillOverlap*15 + distanceScore*20 + ratingScore*10 + verificationScore*10 + responsivenessScore*5`
Transparency: never rank by paid promotion at MVP. If sponsored placement is added later, label it "Sponsored".

## 6. Text Search
Start with MongoDB text indexes (or Atlas Search if available) on job title/description and provider bio/skills/categories. Support partial matches and common Nigerian terms (e.g., "generator mechanic", "AC repair"). Maintain a small synonym list (admin-editable later): "plumber/pipe fitter", "AC/air conditioner", "gen/generator".
Sanitize inputs; limit query length; rate-limit search endpoints.

## 7. Performance Targets (starting)
First page of results < 1.5 s on a typical mobile network; payloads kept small (list responses return only fields the card needs); infinite scroll with cursor pagination, page size 10–20; cache recent results in the app for offline viewing; indexes on category, status, createdAt, geo point, providers' rating/verification; avoid unbounded queries.

## 8. API Notes
`GET /jobs?category=&q=&minBudget=&maxBudget=&lat=&lng=&radiusKm=&type=&sort=&page=&limit=`
`GET /providers?category=&q=&minRating=&verified=&lat=&lng=&radiusKm=&sort=&page=&limit=`
Server validates and bounds all parameters (e.g., radius max 100 km). Responses are paginated with total counts or cursors.

## 9. Anti-gaming
Keyword stuffing penalties (post-MVP), suspended/duplicate profile exclusion, rate limits, reviews required to be on-platform and verified by job completion.

## 10. Future (doc 20)
AI semantic search, recommendations, learning-to-rank from hire/application data, saved searches, job alerts, "similar providers".

## 11. Acceptance Criteria
- Filters combine correctly (category + distance + budget).
- Draft/cancelled/filled jobs never appear in the feed.
- Exact customer address never appears in any search response.
- Distance results are correct within reasonable tolerance and use indexes.
- Suspended or unverified (below L1) providers do not appear.

## 12. Mobile Search UX
- Search bar always visible on Home; recent searches and suggested categories shown before typing.
- Debounce typing and cancel in-flight requests.
- Map toggle on the job feed (cluster markers; respect approximate locations).
- Filter sheet (bottom sheet) with clear/apply, showing active filter count.
- Skeleton loading, empty states with suggestions, and offline cached results labelled as such.
- Blocked users and their content are excluded from results for the blocker.


---
# 12-PRODUCT-SPECS/14-Analytics-and-KPI-Specification.md

# Analytics & KPI Specification

Pack 1 success metrics: registered customers/providers, jobs posted, applications per job, hire conversion, completed jobs, repeat customers, provider retention, average rating, dispute rate, payment success rate, platform revenue.

## 1. Principles
Measure the marketplace loop, not vanity numbers. Define each metric precisely. Respect privacy (doc 09); use consent for tracking.

## 2. North Star Metric
**Completed, paid jobs per week** (jobs reaching Completed with Payment Released).

## 3. Funnel
Visit → Signup → Role selected → Profile complete → (Customer) Job posted → Applications received → Hire → Payment successful → Job completed → Review.
(Provider) Signup → Profile complete → Verified → First application → First hire → First payout.

## 4. KPI Definitions
| KPI | Definition |
|---|---|
| App installs, install-to-signup rate | Store consoles plus first-open events |
| D1/D7/D30 retention | Users opening the app on day N ÷ new users |
| Crash-free sessions/users | Crash reporting tool |
| Push opt-in and open rate | Permission granted ÷ prompted; opens ÷ delivered |
| App version adoption | Share of active users on latest/minimum version |
| Store rating and review count | App Store/Google Play |
| Cold start time, screen load time | Performance monitoring |
| Registered customers / providers | Accounts by role with L1 verification |
| Activated customer | Posted ≥1 job within 7 days of signup |
| Activated provider | Complete profile + ≥1 application within 7 days |
| Jobs posted | Jobs reaching Published |
| Applications per job | Applications ÷ published jobs (median and mean) |
| Time to first application | Published → first application |
| Hire rate | Jobs with a hire ÷ published jobs |
| Time to hire | Published → provider selected |
| Payment conversion | Hires with Successful payment ÷ hires |
| Completion rate | Completed ÷ (hired jobs) |
| Cancellation rate | Cancelled ÷ hired jobs, split by who cancelled |
| Dispute rate | Disputed jobs ÷ hired jobs; resolution time |
| Average rating / review rate | Mean rating; reviews ÷ completed jobs |
| Repeat rate | Customers with ≥2 completed jobs ÷ customers with ≥1 |
| Provider retention | Providers active (applied or worked) in month N ÷ month 0 |
| GMV | Sum of agreed prices of completed paid jobs |
| Take rate | Platform fees ÷ GMV |
| Platform revenue | Platform fees recognised (net of refunds) |
| Payment success rate | Successful ÷ initiated payments |
| Payout success/time | Successful payouts ÷ attempts; median time |
| Supply/demand ratio | Active providers per open job, by category and city |
| Off-platform leakage signal | Hires with no payment, message-filter triggers, user reports |
| Support load | Tickets per 100 jobs; first response time |

## 5. Segmentation
By city/area, category, digital vs physical, user role, acquisition channel, new vs returning, verification level.

## 6. Event Tracking Plan (product events)
`app_installed_first_open`, `app_opened`, `push_permission_prompted`, `push_permission_result`, `location_permission_result`, `deep_link_opened`, `app_update_prompt_shown`, `signup_started`, `signup_completed`, `role_selected`, `profile_completed`, `verification_submitted`, `verification_result`, `job_created`, `job_published`, `job_viewed`, `application_submitted`, `application_status_changed`, `hire_created`, `payment_initiated`, `payment_succeeded`, `payment_failed`, `job_started`, `completion_submitted`, `completion_confirmed`, `payment_released`, `dispute_opened`, `dispute_resolved`, `review_submitted`, `search_performed`, `message_sent`, `report_submitted`.
Each event: eventName, userId (or anonymous ID), role, timestamp, properties (jobId, categoryId, city, amountBucket). Do not log message text, ID numbers or full addresses in analytics.

Business-critical metrics (money, states) are computed from the database (source of truth), not from client-side analytics.

## 7. Tools
MVP: database queries + admin web dashboard + a mobile-capable, privacy-respecting analytics tool (e.g., PostHog or similar) with consent, plus store console metrics. Crash and performance monitoring with Sentry (React Native SDK) or equivalent. Every event includes platform, app version, OS version and device model class. Disclose analytics SDKs in the store privacy forms.

## 8. Dashboards
**Founder weekly dashboard**: north star, funnel conversion, supply/demand by category, GMV/revenue, dispute and cancellation rates, ratings, top issues.
**Ops dashboard**: queue sizes (reports, disputes, verification), SLA breaches, failed payments/payouts.
**Finance view**: GMV, fees, refunds, payout status, reconciliation differences.

## 9. Data Quality
Single definitions in code (shared constants); backfill scripts; test KPI queries against known fixtures; timezone = Africa/Lagos for reporting, store UTC.

## 10. Reporting Cadence
Daily ops check, weekly KPI review (founders), monthly review feeding the Decision Log and Risk Register.

## 11. Targets
Set after pilot baseline. Initial hypotheses to test: ≥3 applications per job, median time to first application < 24h, hire rate ≥ 30%, completion rate ≥ 85%, dispute rate < 5%, average rating ≥ 4.2. Treat as hypotheses.

## 12. Acceptance Criteria
- Admin dashboard (`GET /admin/dashboard`) shows core KPIs derived from the database.
- Events are fired for the listed funnel steps.
- No sensitive personal data in analytics payloads.
- Analytics respects consent settings.


---
# 13-SECURITY-RISK/15-Security-Requirements.md

# Security Requirements Document

Extends Pack 1 Technical Design "Security" and the QA security tests. Applies OWASP Top 10 and OWASP ASVS (Level 1 minimum, Level 2 for payment/admin) as the reference.

## 1. Security Principles
Least privilege; deny by default; validate on the server; never trust the client (roles, prices, payment status); defence in depth; log and audit; protect personal data.

## 2. Authentication
- Passwords hashed with bcrypt/argon2 (adaptive cost); minimum length 8–10 with breached-password check where possible.
- Mobile app: no cookies. Access token (short-lived, e.g., 15 min) sent as a bearer header + rotating refresh token stored on the device in secure storage (Keychain/encrypted storage via expo-secure-store) and hashed server-side, tied to a device session. Revoke on logout, password change, suspension, or "log out of device".
- Admin web panel: httpOnly Secure SameSite cookies or equivalent with CSRF protection.
- Rate limit and lock out brute force on login, OTP, password reset.
- OTP: 6 digits, short expiry, limited attempts, per-phone/IP throttle (SMS pumping protection).
- Email/phone verification tokens single-use and expiring.
- MFA required for admin accounts; optional for users later.
- Generic error messages (don't reveal whether email exists).
- Password reset tokens single-use, short-lived, hashed in DB.

## 3. Authorization
- RBAC: customer, provider, business, admin sub-roles (doc 11).
- Resource-level checks on every endpoint: users access only their own jobs, applications, contracts, messages, payments, disputes. (Prevents IDOR/BOLA.)
- Role comes from the server session/token, never from request body.
- Admin routes separated and double-checked.
- State-machine enforcement: only allowed actors can perform allowed transitions (e.g., only the hired provider can submit completion; only the customer can confirm).

## 4. Input and Output Handling
- Server-side schema validation on every endpoint (e.g., Zod/Joi); reject unknown fields; whitelist updatable fields (avoid mass assignment).
- Prevent NoSQL injection: never pass raw request objects into Mongo queries; strip/deny `$`-operators; cast types.
- Output encoding / React escaping; sanitize any rich text/HTML; set Content-Security-Policy.
- Limit payload sizes; paginate lists; cap query limits.

## 5. Transport and Headers
HTTPS everywhere (the mobile OS blocks cleartext by default; do not weaken it). For the admin web panel and static website: HSTS, secure cookies, Helmet headers, strict CORS allow-list, CSP, and CSRF protection. CORS/CSRF do not protect the mobile API, so the API must authenticate and authorize every request on its own.

## 6. File Uploads
Allow-list MIME types and extensions; verify magic bytes; size limits; rename files; store in object storage (Cloudinary or equivalent), not on the app server; malware scanning where available; private/signed URLs for evidence and ID-related files; strip EXIF location data from public images.

## 7. Payments Security
Per doc 06: signature-verified idempotent webhooks, server-side amount calculation, integer kobo, no card data stored, restricted keys, separate test/live keys, reconciliation, audit trail. Rate-limit payment initialisation. Prevent double payments for the same contract.

## 8. Secrets and Configuration
**Nothing in the mobile app bundle is secret.** Values in `EXPO_PUBLIC_*` variables, app config and JavaScript can be extracted from the installed app. Keep only public identifiers there (API URL, public payment key, restricted maps key). Secrets in backend environment variables, EAS secrets (for build-time), or a secrets manager; never in git (use `.gitignore`, secret scanning, pre-commit hooks); rotate on exposure; separate dev/staging/prod; least-privilege DB users; no default credentials.

## 9. Data Protection
Encrypt at rest (database/storage provider settings) and in transit; encrypt sensitive fields (payout details, ID references) at field level where practical; mask data in logs; never log passwords, tokens, OTPs, card/bank data, full ID numbers; backups encrypted and tested; data retention per doc 09.

## 10. Messaging/Realtime
Authenticate Socket.IO connections; authorize room join by conversation membership; validate/size-limit messages; escape content; rate-limit sending; persist before broadcast.

## 11. Abuse and DoS Protection
Global and per-route rate limits; stricter limits on auth, OTP, search, messaging, applications; bot protection (CAPTCHA/Turnstile) on signup/login when abused; request timeouts; pagination caps.

## 12. Logging, Monitoring, Audit
Structured logs with request IDs; error tracking; alerts on spikes in 401/403/429/5xx, payment failures, webhook signature failures, admin actions; audit logs append-only for privileged/financial actions; retain per policy.

## 13. Dependency and Supply Chain
Lock files committed; automated dependency audit (npm audit / Dependabot); update critical patches quickly; minimal dependencies; review licences.

## 14. Secure Development Practice
Code review via pull requests (CONTRIBUTING.md); branch protection on main; CI runs tests, lint, dependency audit; threat-model new features touching money/identity; security tests in QA plan.

## 15. Infrastructure
Managed hosting with automatic TLS; database not publicly exposed (IP allow-list/private network); least-privilege cloud IAM; automated backups with restore drills; staging separate from production with no real personal data.

## 16. Incident Response
Define severity, owner, containment steps, communication, regulator/user notification (doc 09), postmortem. Keep emergency contacts and a "rotate all secrets" checklist.

## 17. Security Test Checklist (maps to QA plan)
Auth bypass; IDOR on every resource; role escalation; NoSQL injection; XSS; CSRF; mass assignment; rate-limit effectiveness; upload abuse; webhook forgery/replay; amount tampering; session fixation/refresh reuse; CORS misconfiguration; sensitive data exposure in API responses; admin route protection.

## 18. Launch Gate
No open critical/high findings; penetration test or structured self-review completed; secrets audit done; backups restored once successfully; monitoring and alerts live.

## 19. Mobile-Specific Security
- **Token storage:** secure storage only; never AsyncStorage/plain files for tokens; clear on logout and account deletion.
- **API abuse without a browser:** attackers call the API directly, so do not rely on the app for validation, pricing, role checks or rate limiting. Consider app attestation (Play Integrity / App Attest) post-MVP for sensitive endpoints.
- **Deep links:** validate and sanitise all parameters; never let a link perform an action (pay, release, delete) without in-app confirmation; use verified app links/universal links where possible.
- **WebView (payments):** load only the gateway's official domains; disable file access and arbitrary JavaScript bridges; no sensitive data in URLs.
- **Logging:** no tokens, OTPs, personal data in device logs or crash reports; scrub before sending.
- **Screenshots/clipboard:** do not copy sensitive values to the clipboard; consider hiding sensitive screens in the app switcher (post-MVP).
- **Map and third-party keys:** restrict by bundle ID/package name/signing certificate.
- **OTA updates:** sign and protect the update channel; restrict who can publish; keep rollback ability; never ship updates that change core purpose or bypass store review.
- **Build pipeline:** protect Expo/EAS accounts with MFA; limit who can trigger production builds and OTA updates; protect Apple and Google console accounts with MFA and role separation.
- **Reverse engineering:** assume the app is decompiled; minimise logic that must be secret; keep business rules server-side.
- **Old app versions:** enforce minimum supported version for security fixes.
- **Jailbreak/root:** detect and warn (post-MVP); block high-risk actions only if fraud data justifies it.
- **Device sessions:** list active devices, allow remote logout, notify on new-device login.
- **Permissions:** request only what is needed, when needed; no background location in MVP.


---
# 13-SECURITY-RISK/16-Risk-Register.md

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


---
# 14-LAUNCH/17-Launch-Checklist.md

# Launch Checklist

Gate rule (from Pack 1 QA): no P0 blocker, no known critical security issue, critical payment flows tested, backups/monitoring configured, production environment variables verified.

## A. Business & Legal
- [ ] Founders' agreement signed (ownership, vesting, IP assignment, roles)
- [ ] Brand name checked (CAC, trademark registry, domain, social handles)
- [ ] Company registered (OD-06); TIN obtained; business bank account opened
- [ ] Accountant consulted on VAT/fees/payout tax treatment
- [ ] Payment provider approved for live mode; hold/escrow model confirmed in writing (OD-02, OD-03)
- [ ] Lawyer-reviewed ToS, Provider Terms, Privacy Notice, Cookie Notice published
- [ ] Data protection obligations checked (NDPC registration/requirements, vendor agreements)
- [ ] Insurance considered (liability) and provider guidance published
- [ ] Fee rate and cancellation policy decided and shown in UI (OD-01, OD-09)

## B. Product Readiness
- [ ] All P0 tasks done; P1 payments/disputes/reviews done or consciously deferred
- [ ] Categories and pilot city configured
- [ ] Help/FAQ, safety tips, fee explainer published
- [ ] Email/SMS templates live and tested (doc 12)
- [ ] Empty/loading/error/offline states on all screens; verified on real iPhones and real low-end Android devices and slow network
- [ ] Accessibility basics checked

## C. Trust & Safety
- [ ] Verification flow working with chosen provider (OD-04)
- [ ] Report/flag features live; admin queues staffed
- [ ] Prohibited list and rules published (doc 08)
- [ ] Dispute process rehearsed end-to-end (doc 07)
- [ ] Moderation reason codes and templates ready

## D. Payments
- [ ] Test-mode full flow: initialise → pay → webhook → hold → release → payout
- [ ] Failure flows: failed payment, duplicate webhook, bad signature, amount tamper, refund
- [ ] Live-mode small real transaction tested end-to-end
- [ ] Reconciliation job and payout retry tested
- [ ] Webhook URL, secrets and keys set for production

## E. Security
- [ ] Doc 15 launch gate complete
- [ ] Secrets scan clean; no .env committed
- [ ] Dependency audit passed
- [ ] Admin MFA enabled; admin accounts reviewed
- [ ] Rate limits and CORS configured for production
- [ ] Backups configured and restore tested

## F. Infrastructure & Operations
- [ ] Production, staging, development environments separated
- [ ] Domain, HTTPS, DNS email records (SPF/DKIM/DMARC) configured for the static website, API and admin panel
- [ ] Error tracking, uptime monitoring, log retention, health endpoint
- [ ] Alerts to founders' phones for critical failures
- [ ] Runbooks drafted (site down, DB restore, webhook failure, breach)
- [ ] Support email/channel live; templates ready; SLAs agreed

## G. Analytics
- [ ] Event tracking and admin dashboard verified (doc 14)
- [ ] Consent banner/cookie notice live
- [ ] Baseline weekly KPI report template ready

## H. Go-to-Market
- [ ] 30–50 providers onboarded in pilot categories (doc 04)
- [ ] First batch of real jobs lined up
- [ ] Launch content and referral/offer terms ready
- [ ] Feedback channel for pilot users

## I. Soft Launch Plan
1. Invite-only beta with limited volume (e.g., 20–30 jobs).
2. Daily review of every job, dispute and payment for the first 2 weeks.
3. Fix issues, adjust fee/policies, update Decision Log.
4. Expand gradually once completion and dispute rates meet targets.

## J. Rollback
Know how to disable payments, pause new jobs, or put the site in maintenance mode within minutes.

## K. Mobile and Store Release (see doc 21 for details)
- [ ] Apple Developer Program and Google Play Console accounts active, MFA on, two founders have access (OD-19)
- [ ] App name, bundle ID and package name final (OD-23)
- [ ] Production build tested (not only development/Expo Go) on iOS and low-end Android
- [ ] Push notifications work on production credentials (APNs key, FCM configured)
- [ ] Deep links and universal/app links verified
- [ ] Minimum-version gate and maintenance mode tested
- [ ] Block, report and in-app account deletion work
- [ ] Privacy policy, terms, support and deletion pages live on the website and linked in the app and listings
- [ ] Apple App Privacy answers and Google Data safety form completed from the data inventory
- [ ] Store listings: name, descriptions, screenshots, icon, category, age rating questionnaire, contact email
- [ ] Reviewer demo accounts and notes prepared (login details, how to reach each role's screens, payment test instructions)
- [ ] TestFlight and Google Play testing tracks used; closed-testing requirements for new Google developer accounts checked and met
- [ ] Payments policy check recorded in the Decision Log
- [ ] Staged rollout configured; crash monitoring dashboard ready
- [ ] No secrets in the bundle (inspect the built app/JS bundle)
- [ ] Release log started


---
# 14-LAUNCH/18-Requirements-Traceability-Matrix.md

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


---
# 14-LAUNCH/21-App-Store-Compliance-and-Release-Plan.md

# App Store Compliance & Release Plan

> Store rules change often. Every item marked "verify" must be checked against the current Apple App Store Review Guidelines, Apple Developer Program terms, Google Play Developer Policy and Play Console requirements before you rely on it. Nothing here is legal advice.

## 1. Accounts and Identity (OD-19)
| Item | Notes |
|---|---|
| Apple Developer Program | Paid annual membership. Organisation accounts generally need a registered legal entity and a business verification number (verify). Individual accounts show the individual's name as seller |
| Google Play Console | One-time registration fee (verify). New personal accounts may have to run a closed test with a minimum number of testers for a minimum period before production (verify current numbers). Organisation accounts need business verification |
| Both | Turn on MFA; give both founders access with sensible roles; keep recovery details and registration documents in a shared secure place |
| Expo/EAS | Create an organisation account on Expo, MFA, both founders as members |
Because organisation accounts depend on the company registration, start CAC registration (OD-06) early; it is on the critical path for store release. Payment provider live approval also needs the entity.

## 2. Policy Areas That Affect ProCon
**User-generated content (messages, reviews, profiles, jobs).** Provide: content flagging/filtering, report content and users, block users, timely admin action, published contact info. Built in Epic 10; spec in doc 05 §10.

**Account deletion.** If users can create accounts in the app, they must be able to start deletion inside the app; Google also expects a web link for deletion requests (verify). Built via `DELETE /users/me`; explained on the website; backend workflow per doc 09 (deferred when active jobs, payments or disputes exist, with clear messaging).

**Payments.** Digital goods/subscriptions sold in the app generally must use Apple/Google billing; real-world services consumed outside the app generally may use other payment methods (verify exact wording and exceptions, including for person-to-person services and freelance/digital services performed for clients). MVP sells no in-app digital goods. Record the interpretation in the Decision Log. Re-check before adding premium subscriptions, featured listings or digital purchases (post-MVP).

**Privacy.** Privacy policy URL; Apple privacy answers (data types, linked to identity, tracking); Google Data safety form; accurate permission strings; disclose third-party SDK data collection. Source of truth: data inventory in doc 09.

**Permissions.** Request location, camera, photos and notifications only when needed, with clear explanations. App must function reasonably when denied.

**Login and reviewer access.** Provide working demo credentials (customer, provider; admin not needed in the app), instructions for reaching each flow, and sandbox payment instructions. If phone OTP is required, provide a bypass-free path for reviewers such as a fixed test account (design this deliberately and secure it).

**Sign in options.** If you add third-party social login later, check whether the store requires equivalent privacy-preserving options (verify).

**Metadata honesty.** Name, screenshots and description must match the app; no misleading claims such as "background checked" unless true (doc 05).

**Content rating / age.** Complete store questionnaires honestly; 18+ for accounts (OD-07). Check whether messaging/UGC affects the rating.

**Restricted categories.** Marketplace for services must prohibit illegal content (doc 08); be ready to explain moderation.

**Target API level / SDK requirements.** Google Play requires apps to target a recent Android API level and Apple requires builds with a recent Xcode/SDK; Expo SDK upgrades handle this, so schedule upgrades (verify current deadlines).

## 3. Release Pipeline
1. **Development builds** (EAS) for daily work on Android and iOS.
2. **Preview builds** (internal distribution) pointing at the staging API for founders and testers.
3. **TestFlight** (iOS) and **Google Play internal/closed testing** (Android) for the beta group.
4. **Production** build via EAS Build → EAS Submit → store review.
5. **Staged rollout** on Google Play; phased release on the App Store.
6. **OTA updates** (EAS Update) only for JavaScript/asset fixes compatible with the installed native runtime; test on the preview channel first; keep rollback ability.
7. **Native changes** (new permissions, new native libraries, SDK upgrades) always need a new store build and review.

Versioning: semantic version for users; incrementing build number per store upload; backend `min supported version` raised only after most users have updated.

## 4. Environments and Identifiers
Separate app variants for development, preview and production (distinct bundle ID/package name suffixes) so they can be installed together. Staging uses a separate backend, database and payment test keys.

## 5. Pre-Submission Checklist
- [ ] App icon, splash screen, name, short and long description, keywords, category, support URL, privacy URL, contact email
- [ ] Screenshots for required device sizes; short preview video optional
- [ ] Permission strings written and honest
- [ ] Privacy forms completed; SDK list checked
- [ ] Block/report/account deletion verified on the production build
- [ ] Demo account and review notes prepared
- [ ] Sandbox payment instructions for reviewers
- [ ] Production build smoke-tested on real devices (login, post job, apply, hire/pay in test mode, chat, push, deep link)
- [ ] Crash monitoring connected
- [ ] No secrets in bundle; API keys restricted
- [ ] Minimum-version gate tested
- [ ] Legal pages live
- [ ] Release notes written

## 6. After Release
Monitor crash-free rate, ANRs/crashes, store reviews, push delivery, install-to-signup rate, and support tickets for 48 hours; pause rollout if serious issues; hotfix via OTA or new build; log in release log; reply to reviews.

## 7. Common Rejection Causes to Avoid
Broken login for reviewers; missing account deletion; missing report/block; privacy form mismatch; placeholder content; crashes on launch; unexplained permissions; misleading metadata; links that don't work; payment flow that appears to sell digital goods outside store rules.

## 8. Timeline Planning
Allow buffer for review times, account verification, closed-testing periods and fixes after rejection. Do not tie a public launch date to store approval until the first submission passes.


---
# 15-AGENT/19-Agent-Context-Master-Instructions.md

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


---
# 16-BACKLOG/20-Future-Features-and-Ideas-Backlog.md

# Future Features & Ideas Backlog

Not for MVP. Add ideas freely; promote an item only with evidence from pilot data and a Decision Log entry. Priority = rough first guess (H/M/L). "Needs" lists prerequisites.

## Trust & Safety
| Idea | Priority | Needs |
|---|---|---|
| Address verification, guarantor, trade-certificate verification | H | L2 verification working |
| Background checks where legally supported | M | Legal review, vendor |
| Trusted-contact sharing, check-in/check-out, SOS button | H | Mobile maturity, legal review |
| Provider insurance/warranty partners | M | Partnerships |
| Reputation score beyond star rating (reliability, response time) | M | Data from pilot |
| Fraud scoring and anomaly detection | M | Event data |

## Marketplace Mechanics
| Idea | Priority | Needs |
|---|---|---|
| Instant booking / fixed-price service packages ("gigs") | H | Provider pricing data |
| Recurring bookings (weekly cleaning etc.) | H | Payments stable |
| Milestone payments for larger projects | H | Contract/escrow maturity (BR-14) |
| Hourly/daily rates and timesheets | M | Time-tracking design |
| Saved searches, job alerts, favourites, rebooking | M | Search |
| Team/agency provider accounts | M | Business model |
| Group jobs (multiple workers for one job) | M | Contract model change |
| Quotes after site inspection | M | Physical-service flow |

## Payments & Finance
| Idea | Priority | Needs |
|---|---|---|
| Wallets for providers/customers | M | Regulatory advice |
| Faster payouts; mobile money / USSD / bank transfer options | M | Provider support |
| Invoices and receipts PDF; business invoicing | H | Tax advice |
| Tipping | L | Payments |
| Provider financing / advances | L | Licensing |
| Multi-currency, international customers | L | Expansion |

## Growth
| Idea | Priority | Needs |
|---|---|---|
| Referral programme | M | Fee model stable |
| Provider subscriptions (priority, analytics) | M | Supply density |
| Featured/sponsored listings (labelled) | M | Traffic |
| Promo codes and first-job discounts | M | Margin model |
| SEO pages by category × city | H | Content |
| Community/training content for providers; skills academy | M | Partnerships |
| Partnerships with estates, hotels, schools, churches, SMEs | H | Sales |
| WhatsApp bot to post jobs or receive job alerts | H | WhatsApp Business API |

## Product & UX
| Idea | Priority | Needs |
|---|---|---|
| Customer/provider web app or PWA (for desktop users and SEO) | M | Validated mobile MVP |
| Tablet layouts | L | Usage data |
| Biometric unlock (Face ID/fingerprint) | M | Security review |
| Home-screen widgets, Apple/Google wallet-style receipts | L | Usage |
| Deep-linked sharing of provider profiles and jobs with rich previews | H | Website |
| Richer offline mode (queue safe actions, offline drafts) | M | Sync design |
| Local-language support (Pidgin, Yoruba, Hausa, Igbo) | M | Translation |
| Voice search and voice job posting | M | AI |
| Photo/video job posting with AI cost/category suggestion | M | AI |
| Low-data mode | M | Frontend |
| In-app calling with number masking | M | Telephony vendor |

## AI Features
| Idea | Priority | Needs |
|---|---|---|
| AI provider matching and ranking | M | Behaviour data, doc 13 |
| AI-assisted job descriptions and price suggestions | M | Pricing data |
| AI moderation of messages, profiles, reviews | M | Policy clarity |
| Dispute evidence summarisation for admins | M | Dispute volume |
| Chat assistant for onboarding/support | L | Support content |

## Operations & Platform
| Idea | Priority | Needs |
|---|---|---|
| Support ticketing system integration | M | Volume |
| Admin analytics and cohort tools | M | Events |
| Public API/webhooks for business customers | L | Maturity |
| Multi-city expansion tooling | M | Playbook |
| Microservice extraction where needed | L | Scale |
| Data warehouse | L | Scale |

## Ideas Parking Lot
Add new ideas here with date, author and rationale:
- 

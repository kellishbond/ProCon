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

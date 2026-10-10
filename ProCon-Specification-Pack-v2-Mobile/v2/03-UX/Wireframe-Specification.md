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

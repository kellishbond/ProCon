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

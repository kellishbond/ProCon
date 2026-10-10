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

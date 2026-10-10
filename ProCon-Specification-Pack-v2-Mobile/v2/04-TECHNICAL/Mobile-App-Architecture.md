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

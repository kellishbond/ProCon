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

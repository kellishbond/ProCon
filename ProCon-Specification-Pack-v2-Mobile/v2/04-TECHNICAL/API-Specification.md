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

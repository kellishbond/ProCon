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

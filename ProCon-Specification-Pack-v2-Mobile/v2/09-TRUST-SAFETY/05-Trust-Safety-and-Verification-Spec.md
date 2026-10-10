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

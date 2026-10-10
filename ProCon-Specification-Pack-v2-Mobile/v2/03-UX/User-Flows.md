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

# Admin & Operations Manual

Applies to the admin screens in Pack 1 (Dashboard, Users, Providers, Jobs, Categories, Reports, Disputes, Transactions, Verification, Audit logs, Settings).

## 1. Admin Roles (proposed RBAC)
| Role | Permissions |
|---|---|
| Super Admin (founders) | Everything including settings, fees, admin management |
| Moderator | Review reports, hide/remove content, warn/suspend users, no financial actions |
| Support Agent | View users/jobs/messages as needed for tickets, add notes, no refunds |
| Finance Admin | View transactions, approve refunds/payout retries, reconciliation |
| Dispute Resolver | Review and decide disputes within limits; second admin for appeals |
Principle: least privilege; every admin action is audit-logged (adminId, action, target, before/after, reason, timestamp, IP).

## 2. Daily Routine
1. Check dashboard: new users, jobs, payments, failed payments, open disputes, reports.
2. Clear the Reports queue (target: first action within 24h; urgent safety flags immediately).
3. Review verification queue.
4. Review disputes nearing SLA.
5. Check failed webhooks/payouts and reconciliation alerts.
6. Respond to support messages.
7. Review flagged accounts/jobs (doc 05 triggers).

## 3. Weekly Routine
KPI review (doc 14), category/pricing sanity checks, top complaints, provider quality review (low ratings/no-shows), backups and monitoring check, update Decision Log and Risk Register.

## 4. Procedures
**Moderating a report**
1. Open report → view target and context.
2. Decide: dismiss / warn / remove content / restrict / suspend / ban / escalate.
3. Select reason code; add internal note.
4. System notifies affected user; logs action.

**Reviewing verification**
Confirm provider result matches name/profile; handle mismatches by requesting resubmission; approve/reject; record reason.

**Resolving a dispute**
Follow doc 07 timeline. Never decide without reading messages and evidence. Record rationale and amounts. Use a second admin for appeals and for amounts above a configurable threshold.

**Refunds and payout issues**
Only Finance Admin/Super Admin. Verify payment status on the gateway dashboard. Record reference, reason. Never promise refunds outside policy.

**Suspending a user**
Check active jobs/payments first. Flag affected contracts. Notify the counterparty with neutral wording. Do not delete data; set status.

**Category management**
Add/rename/deactivate categories (never hard-delete if jobs reference them). Set type digital/physical/both.

**Data requests**
Log request, verify identity, perform export/deletion/anonymisation per doc 09, record completion.

## 5. Support
- Channels (MVP): support email + in-app contact form + optional WhatsApp business number.
- Templates for: verification failed, report outcome, dispute updates, refund timing, account suspended, how fees work.
- SLA: first response within 24h (business days).
- Ticket tracking: simple shared spreadsheet or helpdesk tool; log ID, user, issue type, owner, status.

## 6. Escalation
| Severity | Examples | Response |
|---|---|---|
| Critical | Safety threat, data breach, payment bug, site down | Immediately; founder on call |
| High | Fraud, stuck payments, high-value dispute | Same day |
| Medium | Standard disputes/reports | Within SLA |
| Low | Questions, feature requests | Weekly batch |

## 7. Admin Security
Unique accounts, strong passwords + MFA (required for Super Admin, Finance), no shared logins, session timeout, IP/device alerts, remove access when roles change, periodic permission review.

## 8. Operations Metrics
Report backlog, median time to first action, dispute resolution time, verification turnaround, refund count/value, repeat offenders.

## 9. Runbooks (create when infrastructure exists)
Site down; database restore; payment webhook failing; email/SMS provider failing; suspected breach; rollback deployment.

## 10. Acceptance Criteria
- Admin-only routes enforce RBAC; moderators cannot access finance actions.
- Every admin mutation creates an audit log entry.
- Suspending a user flags their active contracts.
- Admin views of messages/ID data are logged.

## 11. Mobile Operations Additions
- **Admin interface:** a web panel (D007). Admins never need the mobile app for moderation, disputes or finance.
- **App config control:** Super Admin can set minimum supported version per platform, latest version message and maintenance mode. Setting minimum version incorrectly locks users out, so require a second confirmation and test with a staging build.
- **Release management:** keep a release log (version, build number, date, store status, changes, OTA vs store build). Roll out gradually; watch crash-free rate before expanding.
- **Store reviews and ratings:** check weekly; reply politely to reviews; feed recurring complaints into the backlog.
- **Store review issues:** if a build is rejected, record the reason and fix before resubmitting; keep a reviewer demo account working.
- **Push monitoring:** watch push delivery failures and invalid-token rates.
- **Support triage for app problems:** collect app version, platform, OS version, device model and a screenshot; check crash reports.
- **Runbooks to add:** bad release rollback (disable via config or ship hotfix/OTA), push provider failure, store rejection, forced-update misconfiguration.

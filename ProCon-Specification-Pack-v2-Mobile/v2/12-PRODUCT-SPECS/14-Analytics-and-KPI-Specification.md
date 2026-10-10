# Analytics & KPI Specification

Pack 1 success metrics: registered customers/providers, jobs posted, applications per job, hire conversion, completed jobs, repeat customers, provider retention, average rating, dispute rate, payment success rate, platform revenue.

## 1. Principles
Measure the marketplace loop, not vanity numbers. Define each metric precisely. Respect privacy (doc 09); use consent for tracking.

## 2. North Star Metric
**Completed, paid jobs per week** (jobs reaching Completed with Payment Released).

## 3. Funnel
Visit → Signup → Role selected → Profile complete → (Customer) Job posted → Applications received → Hire → Payment successful → Job completed → Review.
(Provider) Signup → Profile complete → Verified → First application → First hire → First payout.

## 4. KPI Definitions
| KPI | Definition |
|---|---|
| App installs, install-to-signup rate | Store consoles plus first-open events |
| D1/D7/D30 retention | Users opening the app on day N ÷ new users |
| Crash-free sessions/users | Crash reporting tool |
| Push opt-in and open rate | Permission granted ÷ prompted; opens ÷ delivered |
| App version adoption | Share of active users on latest/minimum version |
| Store rating and review count | App Store/Google Play |
| Cold start time, screen load time | Performance monitoring |
| Registered customers / providers | Accounts by role with L1 verification |
| Activated customer | Posted ≥1 job within 7 days of signup |
| Activated provider | Complete profile + ≥1 application within 7 days |
| Jobs posted | Jobs reaching Published |
| Applications per job | Applications ÷ published jobs (median and mean) |
| Time to first application | Published → first application |
| Hire rate | Jobs with a hire ÷ published jobs |
| Time to hire | Published → provider selected |
| Payment conversion | Hires with Successful payment ÷ hires |
| Completion rate | Completed ÷ (hired jobs) |
| Cancellation rate | Cancelled ÷ hired jobs, split by who cancelled |
| Dispute rate | Disputed jobs ÷ hired jobs; resolution time |
| Average rating / review rate | Mean rating; reviews ÷ completed jobs |
| Repeat rate | Customers with ≥2 completed jobs ÷ customers with ≥1 |
| Provider retention | Providers active (applied or worked) in month N ÷ month 0 |
| GMV | Sum of agreed prices of completed paid jobs |
| Take rate | Platform fees ÷ GMV |
| Platform revenue | Platform fees recognised (net of refunds) |
| Payment success rate | Successful ÷ initiated payments |
| Payout success/time | Successful payouts ÷ attempts; median time |
| Supply/demand ratio | Active providers per open job, by category and city |
| Off-platform leakage signal | Hires with no payment, message-filter triggers, user reports |
| Support load | Tickets per 100 jobs; first response time |

## 5. Segmentation
By city/area, category, digital vs physical, user role, acquisition channel, new vs returning, verification level.

## 6. Event Tracking Plan (product events)
`app_installed_first_open`, `app_opened`, `push_permission_prompted`, `push_permission_result`, `location_permission_result`, `deep_link_opened`, `app_update_prompt_shown`, `signup_started`, `signup_completed`, `role_selected`, `profile_completed`, `verification_submitted`, `verification_result`, `job_created`, `job_published`, `job_viewed`, `application_submitted`, `application_status_changed`, `hire_created`, `payment_initiated`, `payment_succeeded`, `payment_failed`, `job_started`, `completion_submitted`, `completion_confirmed`, `payment_released`, `dispute_opened`, `dispute_resolved`, `review_submitted`, `search_performed`, `message_sent`, `report_submitted`.
Each event: eventName, userId (or anonymous ID), role, timestamp, properties (jobId, categoryId, city, amountBucket). Do not log message text, ID numbers or full addresses in analytics.

Business-critical metrics (money, states) are computed from the database (source of truth), not from client-side analytics.

## 7. Tools
MVP: database queries + admin web dashboard + a mobile-capable, privacy-respecting analytics tool (e.g., PostHog or similar) with consent, plus store console metrics. Crash and performance monitoring with Sentry (React Native SDK) or equivalent. Every event includes platform, app version, OS version and device model class. Disclose analytics SDKs in the store privacy forms.

## 8. Dashboards
**Founder weekly dashboard**: north star, funnel conversion, supply/demand by category, GMV/revenue, dispute and cancellation rates, ratings, top issues.
**Ops dashboard**: queue sizes (reports, disputes, verification), SLA breaches, failed payments/payouts.
**Finance view**: GMV, fees, refunds, payout status, reconciliation differences.

## 9. Data Quality
Single definitions in code (shared constants); backfill scripts; test KPI queries against known fixtures; timezone = Africa/Lagos for reporting, store UTC.

## 10. Reporting Cadence
Daily ops check, weekly KPI review (founders), monthly review feeding the Decision Log and Risk Register.

## 11. Targets
Set after pilot baseline. Initial hypotheses to test: ≥3 applications per job, median time to first application < 24h, hire rate ≥ 30%, completion rate ≥ 85%, dispute rate < 5%, average rating ≥ 4.2. Treat as hypotheses.

## 12. Acceptance Criteria
- Admin dashboard (`GET /admin/dashboard`) shows core KPIs derived from the database.
- Events are fired for the listed funnel steps.
- No sensitive personal data in analytics payloads.
- Analytics respects consent settings.

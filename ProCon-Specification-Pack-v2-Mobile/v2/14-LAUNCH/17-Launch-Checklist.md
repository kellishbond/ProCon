# Launch Checklist

Gate rule (from Pack 1 QA): no P0 blocker, no known critical security issue, critical payment flows tested, backups/monitoring configured, production environment variables verified.

## A. Business & Legal
- [ ] Founders' agreement signed (ownership, vesting, IP assignment, roles)
- [ ] Brand name checked (CAC, trademark registry, domain, social handles)
- [ ] Company registered (OD-06); TIN obtained; business bank account opened
- [ ] Accountant consulted on VAT/fees/payout tax treatment
- [ ] Payment provider approved for live mode; hold/escrow model confirmed in writing (OD-02, OD-03)
- [ ] Lawyer-reviewed ToS, Provider Terms, Privacy Notice, Cookie Notice published
- [ ] Data protection obligations checked (NDPC registration/requirements, vendor agreements)
- [ ] Insurance considered (liability) and provider guidance published
- [ ] Fee rate and cancellation policy decided and shown in UI (OD-01, OD-09)

## B. Product Readiness
- [ ] All P0 tasks done; P1 payments/disputes/reviews done or consciously deferred
- [ ] Categories and pilot city configured
- [ ] Help/FAQ, safety tips, fee explainer published
- [ ] Email/SMS templates live and tested (doc 12)
- [ ] Empty/loading/error/offline states on all screens; verified on real iPhones and real low-end Android devices and slow network
- [ ] Accessibility basics checked

## C. Trust & Safety
- [ ] Verification flow working with chosen provider (OD-04)
- [ ] Report/flag features live; admin queues staffed
- [ ] Prohibited list and rules published (doc 08)
- [ ] Dispute process rehearsed end-to-end (doc 07)
- [ ] Moderation reason codes and templates ready

## D. Payments
- [ ] Test-mode full flow: initialise → pay → webhook → hold → release → payout
- [ ] Failure flows: failed payment, duplicate webhook, bad signature, amount tamper, refund
- [ ] Live-mode small real transaction tested end-to-end
- [ ] Reconciliation job and payout retry tested
- [ ] Webhook URL, secrets and keys set for production

## E. Security
- [ ] Doc 15 launch gate complete
- [ ] Secrets scan clean; no .env committed
- [ ] Dependency audit passed
- [ ] Admin MFA enabled; admin accounts reviewed
- [ ] Rate limits and CORS configured for production
- [ ] Backups configured and restore tested

## F. Infrastructure & Operations
- [ ] Production, staging, development environments separated
- [ ] Domain, HTTPS, DNS email records (SPF/DKIM/DMARC) configured for the static website, API and admin panel
- [ ] Error tracking, uptime monitoring, log retention, health endpoint
- [ ] Alerts to founders' phones for critical failures
- [ ] Runbooks drafted (site down, DB restore, webhook failure, breach)
- [ ] Support email/channel live; templates ready; SLAs agreed

## G. Analytics
- [ ] Event tracking and admin dashboard verified (doc 14)
- [ ] Consent banner/cookie notice live
- [ ] Baseline weekly KPI report template ready

## H. Go-to-Market
- [ ] 30–50 providers onboarded in pilot categories (doc 04)
- [ ] First batch of real jobs lined up
- [ ] Launch content and referral/offer terms ready
- [ ] Feedback channel for pilot users

## I. Soft Launch Plan
1. Invite-only beta with limited volume (e.g., 20–30 jobs).
2. Daily review of every job, dispute and payment for the first 2 weeks.
3. Fix issues, adjust fee/policies, update Decision Log.
4. Expand gradually once completion and dispute rates meet targets.

## J. Rollback
Know how to disable payments, pause new jobs, or put the site in maintenance mode within minutes.

## K. Mobile and Store Release (see doc 21 for details)
- [ ] Apple Developer Program and Google Play Console accounts active, MFA on, two founders have access (OD-19)
- [ ] App name, bundle ID and package name final (OD-23)
- [ ] Production build tested (not only development/Expo Go) on iOS and low-end Android
- [ ] Push notifications work on production credentials (APNs key, FCM configured)
- [ ] Deep links and universal/app links verified
- [ ] Minimum-version gate and maintenance mode tested
- [ ] Block, report and in-app account deletion work
- [ ] Privacy policy, terms, support and deletion pages live on the website and linked in the app and listings
- [ ] Apple App Privacy answers and Google Data safety form completed from the data inventory
- [ ] Store listings: name, descriptions, screenshots, icon, category, age rating questionnaire, contact email
- [ ] Reviewer demo accounts and notes prepared (login details, how to reach each role's screens, payment test instructions)
- [ ] TestFlight and Google Play testing tracks used; closed-testing requirements for new Google developer accounts checked and met
- [ ] Payments policy check recorded in the Decision Log
- [ ] Staged rollout configured; crash monitoring dashboard ready
- [ ] No secrets in the bundle (inspect the built app/JS bundle)
- [ ] Release log started

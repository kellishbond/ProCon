# App Store Compliance & Release Plan

> Store rules change often. Every item marked "verify" must be checked against the current Apple App Store Review Guidelines, Apple Developer Program terms, Google Play Developer Policy and Play Console requirements before you rely on it. Nothing here is legal advice.

## 1. Accounts and Identity (OD-19)
| Item | Notes |
|---|---|
| Apple Developer Program | Paid annual membership. Organisation accounts generally need a registered legal entity and a business verification number (verify). Individual accounts show the individual's name as seller |
| Google Play Console | One-time registration fee (verify). New personal accounts may have to run a closed test with a minimum number of testers for a minimum period before production (verify current numbers). Organisation accounts need business verification |
| Both | Turn on MFA; give both founders access with sensible roles; keep recovery details and registration documents in a shared secure place |
| Expo/EAS | Create an organisation account on Expo, MFA, both founders as members |
Because organisation accounts depend on the company registration, start CAC registration (OD-06) early; it is on the critical path for store release. Payment provider live approval also needs the entity.

## 2. Policy Areas That Affect ProCon
**User-generated content (messages, reviews, profiles, jobs).** Provide: content flagging/filtering, report content and users, block users, timely admin action, published contact info. Built in Epic 10; spec in doc 05 §10.

**Account deletion.** If users can create accounts in the app, they must be able to start deletion inside the app; Google also expects a web link for deletion requests (verify). Built via `DELETE /users/me`; explained on the website; backend workflow per doc 09 (deferred when active jobs, payments or disputes exist, with clear messaging).

**Payments.** Digital goods/subscriptions sold in the app generally must use Apple/Google billing; real-world services consumed outside the app generally may use other payment methods (verify exact wording and exceptions, including for person-to-person services and freelance/digital services performed for clients). MVP sells no in-app digital goods. Record the interpretation in the Decision Log. Re-check before adding premium subscriptions, featured listings or digital purchases (post-MVP).

**Privacy.** Privacy policy URL; Apple privacy answers (data types, linked to identity, tracking); Google Data safety form; accurate permission strings; disclose third-party SDK data collection. Source of truth: data inventory in doc 09.

**Permissions.** Request location, camera, photos and notifications only when needed, with clear explanations. App must function reasonably when denied.

**Login and reviewer access.** Provide working demo credentials (customer, provider; admin not needed in the app), instructions for reaching each flow, and sandbox payment instructions. If phone OTP is required, provide a bypass-free path for reviewers such as a fixed test account (design this deliberately and secure it).

**Sign in options.** If you add third-party social login later, check whether the store requires equivalent privacy-preserving options (verify).

**Metadata honesty.** Name, screenshots and description must match the app; no misleading claims such as "background checked" unless true (doc 05).

**Content rating / age.** Complete store questionnaires honestly; 18+ for accounts (OD-07). Check whether messaging/UGC affects the rating.

**Restricted categories.** Marketplace for services must prohibit illegal content (doc 08); be ready to explain moderation.

**Target API level / SDK requirements.** Google Play requires apps to target a recent Android API level and Apple requires builds with a recent Xcode/SDK; Expo SDK upgrades handle this, so schedule upgrades (verify current deadlines).

## 3. Release Pipeline
1. **Development builds** (EAS) for daily work on Android and iOS.
2. **Preview builds** (internal distribution) pointing at the staging API for founders and testers.
3. **TestFlight** (iOS) and **Google Play internal/closed testing** (Android) for the beta group.
4. **Production** build via EAS Build → EAS Submit → store review.
5. **Staged rollout** on Google Play; phased release on the App Store.
6. **OTA updates** (EAS Update) only for JavaScript/asset fixes compatible with the installed native runtime; test on the preview channel first; keep rollback ability.
7. **Native changes** (new permissions, new native libraries, SDK upgrades) always need a new store build and review.

Versioning: semantic version for users; incrementing build number per store upload; backend `min supported version` raised only after most users have updated.

## 4. Environments and Identifiers
Separate app variants for development, preview and production (distinct bundle ID/package name suffixes) so they can be installed together. Staging uses a separate backend, database and payment test keys.

## 5. Pre-Submission Checklist
- [ ] App icon, splash screen, name, short and long description, keywords, category, support URL, privacy URL, contact email
- [ ] Screenshots for required device sizes; short preview video optional
- [ ] Permission strings written and honest
- [ ] Privacy forms completed; SDK list checked
- [ ] Block/report/account deletion verified on the production build
- [ ] Demo account and review notes prepared
- [ ] Sandbox payment instructions for reviewers
- [ ] Production build smoke-tested on real devices (login, post job, apply, hire/pay in test mode, chat, push, deep link)
- [ ] Crash monitoring connected
- [ ] No secrets in bundle; API keys restricted
- [ ] Minimum-version gate tested
- [ ] Legal pages live
- [ ] Release notes written

## 6. After Release
Monitor crash-free rate, ANRs/crashes, store reviews, push delivery, install-to-signup rate, and support tickets for 48 hours; pause rollout if serious issues; hotfix via OTA or new build; log in release log; reply to reviews.

## 7. Common Rejection Causes to Avoid
Broken login for reviewers; missing account deletion; missing report/block; privacy form mismatch; placeholder content; crashes on launch; unexplained permissions; misleading metadata; links that don't work; payment flow that appears to sell digital goods outside store rules.

## 8. Timeline Planning
Allow buffer for review times, account verification, closed-testing periods and fixes after rejection. Do not tie a public launch date to store approval until the first submission passes.

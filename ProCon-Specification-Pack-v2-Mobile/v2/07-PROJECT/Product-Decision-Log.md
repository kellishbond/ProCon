# Product Decision Log

## Decision Template
Date:
Decision:
Context:
Options considered:
Chosen option:
Reason:
Impact:
Owner:

## Initial Decisions

### D001 — Marketplace Scope
Decision: Support both digital services and physical/local services.
Reason: The product's differentiation is connecting customers with people who can perform both laptop-based work and hands-on local work.

### D002 — Architecture
Decision: Start with a modular monolith.
Reason: Faster MVP development and easier deployment while preserving domain boundaries.

### D003 — Mobile First (SUPERSEDED by D005)
Original decision: Responsive web first; native mobile apps after product validation.
Status: Superseded on the mobile pivot.

### D004 — Trust
Decision: Verification, ratings, job history and dispute mechanisms are core product capabilities.
Reason: Trust is a central marketplace problem.

Future decisions should be added here before they become hidden assumptions in code.

### D005 — Native Mobile App Instead of Web App
Date: (fill in)
Decision: The customer/provider/business product is a native mobile app for iOS and Android. No customer-facing web app in the MVP. Supersedes D003.
Context: Founders concluded a mobile app suits the product: phone-first users, push notifications, camera and location, and app-store credibility.
Options considered: responsive web app; PWA; React Native/Expo; fully native Swift/Kotlin; Flutter.
Chosen option: React Native with Expo.
Reason: Single codebase for both platforms, strong JS/React skill fit for the founders, EAS for builds and updates, good library support for push, location, camera and secure storage.
Impact: Changes auth (tokens, no cookies), notifications (push), location/permissions, releases (store review, EAS), testing (devices), compliance (app store rules), and the launch checklist. Docs updated across both packs.
Owner: Founders

### D006 — Expo Workflow
Decision: Use Expo Go only for early prototyping; use development builds (EAS) for real feature work; ship via EAS Build/Submit; OTA updates only for JavaScript/asset fixes.
Reason: Expo Go cannot cover all native needs (push, custom config); builds must match production behaviour.

### D007 — Admin as Web Panel (PROPOSED — confirm)
Decision: Admins and moderators use a separate lightweight web panel, not the mobile app.
Reason: Dispute review, moderation and finance work are easier on a desktop; keeps the mobile app focused on customers and providers.
Alternative: admin screens inside the mobile app (more work, harder for heavy workflows).

### D008 — Static Website (PROPOSED — confirm)
Decision: Maintain a small static website for privacy policy, terms, support and account-deletion information, as required by app store listings.

### D009 — Platforms (PROPOSED — confirm)
Decision: Build for iOS and Android together from one codebase; prioritise testing on low-end Android devices because that matches likely user devices (verify with pilot data).

Future decisions should be added here before they become hidden assumptions in code.

### D010 — Project Name: ProCon
Decision: The product is named ProCon (replacing the working name ConnectNaija).
Reason: Founders wanted a unique name.
Open check: availability (OD-18) must be confirmed with CAC, trademark registry, domain, social handles and the app stores before registration and branding spend.
Impact: All documents updated; reserve app name, bundle ID/package name and domain (OD-23) using the new name once availability is confirmed.

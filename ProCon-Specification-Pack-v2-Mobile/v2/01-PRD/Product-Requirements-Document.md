# Product Requirements Document (PRD)
## Working Product Name: ProCon

### 1. Product Vision
ProCon is a Nigeria-first **mobile app (iOS and Android)** that connects people and businesses that need work done with trusted people who can do it. The platform supports both digital services and physical/local labour.

**Platform decision (D005):** The customer and provider product is a native mobile app built with React Native and Expo. There is no customer-facing web app in the MVP. Admins use a separate lightweight web admin panel (D007), and a small static website hosts legal pages, support and account-deletion information required by the app stores.

### 2. Problem
Finding trustworthy workers in Nigeria often depends on personal referrals, WhatsApp groups, social media, or informal networks. Customers struggle to compare providers, verify identity, agree on scope and price, track work, and resolve disputes. Skilled workers also struggle to consistently find customers and build portable reputations.

### 3. Target Users
- Customers needing one-off or recurring services
- Freelancers and digital professionals
- Skilled tradespeople
- General labour/service workers
- Small businesses and organizations
- Platform administrators

### 4. Core Value Proposition
For customers: discover, compare, hire, communicate with, pay, and review trusted providers.
For providers: create a professional profile, discover jobs, apply, get hired, build reputation, and receive payments.

### 5. Service Categories
Initial categories should include:
- Cleaning
- Plumbing
- Electrical
- Generator/AC services
- Painting
- Carpentry
- Moving/labour
- Beauty/personal care
- Repairs/maintenance
- Events
- Photography/video
- Tutoring
- Writing
- Design
- Software development
- Digital marketing
- Virtual assistance
- Other services

Categories must be admin-configurable.

### 6. User Roles
Customer, Service Provider, Business, Administrator.

### 7. MVP Features
- iOS and Android app (single React Native/Expo codebase)
- Account registration/login
- Role selection
- Customer profile
- Provider profile
- Identity/phone verification foundation
- Service categories
- Job creation
- Job browsing/search
- Location and distance filtering
- Provider applications/offers
- Customer shortlist and hiring
- In-platform job status
- Messaging
- Notifications
- Reviews/ratings
- Admin dashboard
- Basic reporting/moderation
- Payment integration architecture
- Transaction records
- Push notifications (device registration, deep links to the relevant screen)
- Camera/photo upload for profiles, jobs, portfolio and dispute evidence
- Block and report users (also an app store requirement for apps with user-generated content)
- In-app account deletion (app store requirement)
- Forced-update / minimum app version control
- Lightweight web admin panel (admin and moderators only)
- Static website for legal pages, support and account deletion info

### 8. Out of Scope for MVP
- Customer/provider web app (the product is mobile-only in MVP)
- Tablet-optimised layouts
- Complex AI matching
- International expansion
- Full payroll/employment management
- Advanced subscription plans
- Complex auction/bidding algorithms
- Automated background checks beyond supported verification
- Multi-country currencies

### 9. Key User Stories
#### Customer
- As a customer, I want to create an account so I can hire providers.
- As a customer, I want to post a job with category, description, location, budget and timing.
- As a customer, I want to receive applications so I can compare providers.
- As a customer, I want to message a provider before hiring.
- As a customer, I want to confirm completion and review the provider.

#### Provider
- As a provider, I want to create a profile showing my skills, experience, location and pricing.
- As a provider, I want to find jobs relevant to my skills and location.
- As a provider, I want to apply to jobs.
- As a provider, I want to track accepted jobs and payments.
- As a provider, I want reviews to build my reputation.

#### Admin
- As an admin, I want to manage users, jobs, categories, disputes and reports.
- As an admin, I want to moderate suspicious content and accounts.

### 10. Non-Functional Requirements
- Native mobile experience on iOS and Android with a single codebase
- Works acceptably on low-end Android phones and slow/unstable mobile networks (small app size, light screens, image compression, caching, retry)
- Offline tolerance: cached read screens, queued retries for safe actions, clear offline states
- Secure token storage on the device (secure storage, not plain storage)
- Backward-compatible API: old app versions stay in use for weeks, so the API must not break them
- Secure authentication and authorization
- Server-side validation
- Rate limiting on sensitive endpoints
- Auditability of financial/job state changes
- Accessible UI (screen readers, scalable text, sufficient contrast, touch targets)
- Reasonable screen load performance on Nigerian mobile networks and mid/low-range devices
- Compliance with Apple App Store and Google Play policies
- Scalable architecture
- Secure handling of secrets and personal information

### 11. Success Metrics
- App installs and install-to-signup rate
- Registered customers
- Registered providers
- Jobs posted
- Applications per job
- Hire conversion rate
- Completed jobs
- Repeat customers
- Provider retention
- Average rating
- Dispute rate
- Payment success rate
- Platform revenue
- Day-1/Day-7/Day-30 retention
- Crash-free sessions and store rating
- Push notification opt-in rate

### 12. Business Model
Potential models:
- Commission/service fee on completed transactions
- Provider premium subscriptions
- Business plans
- Featured provider listings
- Sponsored placements
- Optional verification fees

The MVP should begin with one simple, transparent transaction-fee model.

### 13. Product Principles
1. Trust before growth.
2. Mobile-native: the app is the product.
3. Simple enough for non-technical users.
4. Location matters for physical services.
5. Payments and job state must be traceable.
6. Never hide important fees.
7. Build Nigeria-first, but avoid architecture that blocks future expansion.
8. Respect the user's data and battery: lightweight screens, compressed images, foreground-only location, minimal background activity.
9. Never break old app versions silently: version the API and support a minimum-version gate.

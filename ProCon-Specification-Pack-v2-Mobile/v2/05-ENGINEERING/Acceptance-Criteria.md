# Acceptance Criteria

## Create Job
Given an authenticated customer, they can create a job with required title, category, description, budget and location. Invalid input is rejected. The new job is visible according to its publication status.

## Apply to Job
Given an authenticated provider, the provider can apply to an eligible job. Duplicate applications are prevented. Customer can view the application.

## Hire
Customer can select an application. The job moves to the correct state. Other applications become unavailable/rejected according to business rules.

## Completion
Provider can submit completion. Customer can confirm or raise a dispute. The platform records timestamps and actors.

## Review
Only eligible participants of a completed job can review. Duplicate reviews are prevented. Rating aggregation updates correctly.

## Payment
Payment status must be based on server-side verification/webhook data. Duplicate webhook events must be idempotent.

## Security
A user cannot access another user's private resources. Provider-only/customer-only/admin-only endpoints enforce role permissions.

## Mobile App
App launches on supported iOS and Android versions. Below the minimum supported version, the user sees a blocking update screen. Tokens are stored in secure storage and cleared on logout. The app works from cached data when offline and clearly blocks money actions. Push token registers after login and is removed on logout. Tapping a push notification opens the correct screen from cold start and warm start. Denying location or notification permission never blocks core use. Users can report and block other users. Users can request account deletion inside the app. No secrets are present in the app bundle.

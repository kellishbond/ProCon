# Database Schema

## User
- id
- role
- name
- email
- phone
- passwordHash
- status
- verificationStatus
- createdAt
- updatedAt

## ProviderProfile
- userId
- bio
- skills
- categories
- experience
- pricing
- serviceArea
- location
- availability
- portfolio
- ratingAverage
- completedJobs

## BusinessProfile
- userId
- businessName
- description
- industry
- contactDetails
- verificationStatus

## Category
- id
- name
- slug
- parentId
- type (digital/physical/both)
- active

## Job
- id
- customerId
- title
- description
- categoryId
- budgetMin
- budgetMax
- location
- schedule
- status
- attachments
- createdAt
- updatedAt

## Application
- id
- jobId
- providerId
- message
- proposedPrice
- status
- createdAt

## Hire/Contract
- id
- jobId
- customerId
- providerId
- agreedPrice
- status
- startAt
- completionAt

## Message
- id
- conversationId
- senderId
- body
- attachments
- createdAt
- readAt

## Review
- id
- jobId
- reviewerId
- revieweeId
- rating
- comment
- createdAt

## Payment
- id
- jobId
- payerId
- payeeId
- providerReference
- amount
- platformFee
- currency
- status
- createdAt
- updatedAt

## Dispute
- id
- jobId
- openedBy
- reason
- evidence
- status
- resolution
- resolvedBy
- resolvedAt

## Notification
- id
- userId
- type
- title
- body
- readAt
- createdAt

## Report
- id
- reporterId
- targetType
- targetId
- reason
- status
- resolvedBy
- resolvedAt

Indexes should be designed around authentication lookups, job filtering, category filtering, provider location, conversations and payment references.

## Mobile-Driven Additions (D005)

## Device
- id
- userId
- expoPushToken (or native token)
- platform (ios/android)
- appVersion
- osVersion
- deviceId
- notificationsEnabled
- lastSeenAt
- active (false when the push service reports an invalid token)
- createdAt

## Session (device session / refresh token)
- id
- userId
- deviceId
- refreshTokenHash
- createdAt
- lastUsedAt
- expiresAt
- revokedAt

## AppConfig
- platform (ios/android)
- minSupportedVersion
- latestVersion
- maintenanceMode
- message
- updatedAt

## Block
- id
- blockerId
- blockedId
- createdAt

Notes:
- Report (existing) must support targetType values: user, job, message, review, profile.
- User should add: `deletionRequestedAt`, `anonymisedAt`, `notificationPreferences`, `termsAcceptances[]`, `consents[]` (see Pack 2 docs 09, 10, 12).
- Payment, Dispute, Verification and AuditLog additions are specified in Pack 2 docs 05, 06, 07 and 18.

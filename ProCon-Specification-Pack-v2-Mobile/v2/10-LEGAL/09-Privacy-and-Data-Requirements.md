# Privacy & Data Requirements

> Not legal advice. Have a Nigerian data-protection lawyer review before launch. The main law referenced is the Nigeria Data Protection Act 2023 (NDPA), regulated by the Nigeria Data Protection Commission (NDPC). Confirm current obligations (registration, audits, thresholds, breach timelines) with a lawyer or the NDPC.

## 1. Roles
ProCon (the company) is the **data controller** for user data. Payment, SMS, verification, hosting and maps vendors are **data processors**; sign data-processing terms with each.

## 2. Personal Data Inventory
| Data | Source | Purpose | Sensitivity |
|---|---|---|---|
| Name, email, phone, password hash | Registration | Account, login, communication | Normal |
| Profile photo, bio, skills, portfolio | Provider/customer | Marketplace display | Normal |
| Location (service area, job address, optional lat/lng) | User | Matching, delivery of service | High |
| Verification result/reference; ID details | Verification provider | Trust | High — minimise |
| Messages and attachments | Users | Job coordination, dispute evidence | Medium–High |
| Payment references, payout bank details (tokens) | Gateway | Payments | High |
| Reviews, ratings | Users | Reputation | Normal |
| Device ID, push token, app version, OS, device model, IP, logs | App/System | Notifications, security, debugging, compatibility | Normal–Medium |
| Device permissions: location, camera/photos, notifications | User choice | Features | High (location) |
| Crash/diagnostic and analytics data | SDKs | Stability, product improvement | Normal–Medium |
| Reports/disputes/evidence | Users/admin | Safety, resolution | High |

Do not collect data without a stated purpose. Do not collect special-category data (health, religion, etc.) unless essential.

## 3. Lawful Basis and Consent
- Contract: needed to run accounts, jobs, payments.
- Legitimate interest: fraud prevention, security, service improvement (document the balance).
- Legal obligation: tax/accounting records, lawful requests.
- Consent: marketing messages, optional precise location, optional analytics/cookies. Must be freely given, specific, withdrawable, and recorded (timestamp, version).
Show a privacy notice at signup and a link in the footer. Version the notice and record acceptance.

## 4. User Rights (build the capability)
Access/copy of data; correction; deletion (subject to legal retention); objection to processing/marketing; withdrawal of consent; data portability where applicable; complaint route. Provide a settings page and a contact email for requests; respond within the legal timeframe (confirm with lawyer).
Proposed endpoints (post-MVP acceptable if manual process exists at launch): `POST /users/me/data-export`, `POST /users/me/delete-request`.

## 5. Retention Schedule (proposed — confirm with lawyer/accountant)
| Data | Retain |
|---|---|
| Account data | While active + a set period after deletion request for legal/dispute needs |
| Financial/transaction records | Per tax/accounting law (commonly multiple years; confirm) |
| Messages | While job exists + dispute window + a set period; then delete/anonymise |
| Dispute evidence | Until resolved + appeal window + a set period |
| Verification data | Keep result and reference; delete raw documents quickly or never store |
| Logs | Short rolling period (e.g., 90 days) |
| Marketing consent records | As long as needed to prove consent |

Deletion = remove or anonymise personal data while keeping legally required financial records and reviews in anonymised form (e.g., "Former user").

## 5b. Data Location and Transfers
Hosting, storage, maps and email vendors may be outside Nigeria. Choose vendors with adequate safeguards; document cross-border transfers and include them in the privacy notice. Confirm NDPA transfer rules with a lawyer.

## 6. Security of Personal Data
See doc 15. At minimum: encryption in transit (HTTPS), encryption at rest where supported, access control by role, least privilege for admins, audit logs for admin access to personal data, secrets in environment variables, backups encrypted.

## 7. Breach Response
Maintain an incident plan: detect, contain, assess, notify the regulator and affected users within the legally required time (confirm timeline with lawyer), document, fix. Assign an incident owner among founders.

## 8. Tracking, SDKs and Cookies
The app does not use cookies; the static website and admin panel may. Use only necessary tracking at MVP plus consent-based analytics. List every SDK (analytics, crash reporting, maps, payments, push) with what data it collects. Avoid selling or sharing data for advertising. Provide a cookie notice on the website.

## 9. Children
18+ only (OD-07). Block signup if age confirmation is declined. Do not knowingly collect children's data; delete if discovered.

## 10. Product Requirements
- Privacy notice + consent checkbox at registration (versioned).
- Data minimisation: public profile shows only needed fields; never expose email/phone/exact address publicly.
- Precise job address visible only to the hired provider.
- Admin access to messages/ID data is restricted and logged.
- Data-subject request tracker (even a simple admin screen/spreadsheet).
- Delete/anonymise workflow documented and tested.
- **In-app account deletion** (Settings → Delete account) that triggers the same backend workflow; the stores expect it, and a web page explaining deletion must also be available.
- **Permission strings** (iOS usage descriptions, Android permission rationale) that honestly state why location, camera, photos and notifications are needed.
- **Store privacy disclosures:** Apple App Privacy ("nutrition label") details and Google Play Data safety form must match the actual data collected, including by third-party SDKs. Keep an internal data inventory (above) as the single source for both.
- **Push token handling:** treat as personal data; delete on logout/account deletion.
- **Local device storage:** no personal data in plain storage; clear on logout.
- Vendor list with purposes and agreements maintained.

## 11. Proposed Schema Additions
`consents[]` (type, version, acceptedAt, ip), `privacyNoticeVersion`, `deletionRequestedAt`, `anonymisedAt`.

## 12. Launch Gate
Privacy notice published, vendors listed, retention/deletion process documented, lawyer review complete, registration/compliance obligations with NDPC checked.

## 13. Mobile Launch Gate additions
Privacy policy URL live and linked in store listings and inside the app; store privacy forms completed from the data inventory; account deletion works in-app and is documented on the website; SDK list reviewed.

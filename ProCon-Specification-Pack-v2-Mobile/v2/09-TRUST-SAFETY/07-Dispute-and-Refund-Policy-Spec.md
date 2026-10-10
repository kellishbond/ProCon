# Dispute & Refund Policy Specification

Aligned with Pack 1 Dispute Flow: open dispute → reason → evidence → job/payment flagged → admin review → decision → refund/release/other → audit log. Job state `Disputed` and Dispute model exist in Pack 1.

## 1. Principles
Fair, evidence-based, fast, documented, consistent. Both parties are heard. Decisions are reasoned and recorded.

## 2. Who Can Open a Dispute
The customer or provider on a job in In Progress, Submitted for Completion, or within 7 days after Completed/Cancelled (window is configurable). Only one open dispute per job.

## 3. Reason Codes (Dispute.reason)
Customer-opened: work not started/no-show; work incomplete; poor quality/not as described; damage or safety issue; provider asked for off-platform payment; extra charges demanded.
Provider-opened: customer unresponsive after completion; customer refuses to confirm; scope changed unfairly; access denied/no-show at site; abuse/harassment; payment problem.
Others: fraud suspicion; other (free text).

## 4. Process and SLAs (OD-15 defaults)
1. **Open** — user selects reason, writes description, attaches evidence (photos, screenshots, chat excerpts auto-attached). Job → Disputed; payment flagged; auto-release paused.
2. **Notify** — other party notified and gets 48 hours to respond with their account and evidence.
3. **Review** — admin reviews timeline, messages, evidence, ratings history. May request more information (clock paused).
4. **Decision** — within 5 business days of the response (or no-response deadline). Admin records decision, reasoning, and amounts.
5. **Execute** — system performs release/refund/partial split, updates states, notifies both.
6. **Close** — dispute closed; optional one appeal within 7 days to a second admin.
First admin acknowledgement target: 24 hours.

## 5. Possible Outcomes (Dispute.resolution)
| Outcome | Effect |
|---|---|
| Release in full to provider | Payment → Released; job Completed |
| Refund in full to customer | Payment → Refunded; job Cancelled |
| Partial split | Part refunded, part released; fee on released portion only |
| Redo/fix period | Dispute paused up to N days for provider to correct work; then re-review |
| No action/dismissed | Dispute closed; original flow resumes |
| Account action | Warning/suspension per doc 05 |

## 6. Cancellation & Refund Defaults (OD-09 — proposed, adjust after interviews)
| Situation | Default result |
|---|---|
| Customer cancels before provider starts, before agreed start time by more than 24h | Full refund |
| Customer cancels within 24h of start | Refund minus a configurable cancellation fee paid to provider (e.g., small %) |
| Provider cancels or no-shows | Full refund to customer; provider reliability counted; repeated issues → account action |
| Job started, then cancelled by mutual agreement | Split by agreement, recorded in-app |
| Job started, unilateral cancel | Goes to dispute |
| Payment failed/expired | No charge; contract not activated |
Platform fee is not retained on fully refunded jobs.

## 7. Evidence Requirements
- Accepted: images, short video, PDFs, chat records, receipts, location/time data if consented.
- Evidence stored securely, access limited to parties and admins; retained per doc 09.
- Admin sees complete message history for the job. Users are told this in the ToS.

## 8. Decision Guidelines for Admins
Check: Was scope agreed in writing in-app? Did both parties communicate in-app? Evidence of delivery? Timeline compliance? Prior behaviour? Prefer proportionate outcomes; avoid all-or-nothing when partial work is evident. Use decision templates; require a reason code and written rationale.

## 9. Anti-abuse
Limit disputes per user per period; flag users with high dispute rates; flag users with repeated losses; penalize false claims.

## 10. Data Model Notes
Pack 1 Dispute has: id, jobId, openedBy, reason, evidence, status, resolution, resolvedBy, resolvedAt.
Proposed additions: `reasonCode`, `description`, `respondentResponse`, `respondentEvidence`, `responseDeadline`, `resolutionAmounts` (refund/release), `adminNotes` (internal), `appealStatus`, `timeline[]`.
Dispute statuses (proposed): Open → Awaiting Response → Under Review → Resolved → Appealed → Closed.

## 11. Acceptance Criteria
- Opening a dispute blocks payment release and auto-release timer.
- Both parties can submit evidence until the deadline.
- Only admins can resolve; all decisions require a reason and create audit logs.
- Resolution amounts never exceed the held amount.
- Users receive notifications at each stage.

## 12. Mobile Notes
- Evidence capture: allow taking photos/video directly in the app, with compression and a size limit; show upload progress and allow retry; store with the dispute record.
- Push and in-app notifications at each dispute stage; email as backup (doc 12). The response deadline countdown must be visible in the app.
- Users who delete their account while a dispute is open: deletion is deferred until the dispute and payment are settled.
- Blocked users can still respond in an existing dispute.

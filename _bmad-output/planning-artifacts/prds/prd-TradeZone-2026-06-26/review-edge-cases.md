# TradeZone PRD — Edge-Case Review (Unhandled Cases Only)

Scope: gaps the PRD/addendum do not address. Only unhandled branching paths, boundaries, and state transitions.

## A. Listing lifecycle & status transitions
- A1. Rejected → resubmit path undefined.
- A2. `fee_required` has no timeout (unpaid listings sit forever).
- A3. Editing a `fee_required` listing (e.g. price drop below "high-value") — fee recalculation undefined.
- A4. `expired → published` renewal transition not in the state machine; does unchanged renewal skip moderation?
- A5. `closed → published` relist undefined.
- A6. `draft` declared but never operationalized.
- A7. 60-day clock origin when a listing stalls in pending/fee_required.
- A8. Material edit instantly hides a live listing during re-moderation (no "stay live until re-approved").
- A9. Concurrent seller-close vs admin-decision.
- A10. Renewal + previously paid fee (re-charge? credit?).

## B. Re-moderation on edit
- B1. Paid-then-edited fee handling (re-pay? refund if below threshold?).
- B2. Rejection of an edited version kills the original (no revert to last-approved).
- B3. Minor-edit bypass of moderation — undefined "minor" bucket is a scam-injection exploit.
- B4. Repeated edits while in `pending` (queue position/duplication).
- B5. Contact-preference change classification (material/minor?) and effect on active chats.

## C. PayHere payment failure / timeout / duplicate callback
- C1. Success-but-no-callback: seller charged, listing never publishes; no reconciliation path.
- C2. No refund path anywhere (rejected-after-pay, deletion, deactivation, badge revoke, double-charge).
- C3. Payment for a no-longer-publishable listing (rejected/deleted/category off mid-payment).
- C4. Duplicate success callback past idempotency window.
- C5. Callback signature-verification failure on a genuine payment.
- C6. Fee amount changed mid-payment.
- C7. Concurrent retries → double charge.
- C8. Badge granted-but-unpaid limbo (no timeout/auto-revoke).
- C9. Badge fee payment failure (no retry/expiry).
- C10. Chargeback/dispute after publish.
- C11. Payment session / `fee_required` window expiry.

## D. WhatsApp OTP failures & number changes
- D1. OTP delivery failure blocks listing with no fallback FR.
- D2. Non-WhatsApp number entered (never receives OTP).
- D3. Resend rate-limit lockout recovery undefined.
- D4. WhatsApp number uniqueness per account not enforced (ban evasion / duplicates).
- D5. Number change orphans live WhatsApp listings (deep-link to old, unverified number).
- D6. Listings during re-verification limbo (paused? hidden? live?).
- D7. Verified number ≠ listed contact number (verify A, route to B).
- D8. Number recycling/reassignment by telecoms; no re-verification cadence.
- D9. Number change as account-takeover vector.

## E. Badge grant-then-non-payment & lifecycle
- E1. Granted-unpaid display state.
- E2. No badge revocation mechanism.
- E3. No badge expiry/re-vetting cadence.
- E4. Badge on role change / account deletion (persistence/refund).
- E5. Re-request after decline (no cooldown → admin spam).
- E6. Badge fee recurring vs one-time unspecified.
- E7. Badge with no active listings.

## F. Seller account deletion
- F1. Account deletion/deactivation entirely undefined.
- F2. Fate of published listings on deletion.
- F3. Active in-app conversations on deletion.
- F4. Pending/queued listings on deletion.
- F5. `fee_required`/paid listings + refunds on deletion.
- F6. Badged seller deletion (refund/teardown).
- F7. Re-registration after deletion (data resurfacing/verification reset).
- F8. No admin ban/suspend of a fraudulent USER (only listing moderation exists).

## G. Buyer contacting expired/closed/rejected listing
- G1. Direct URL to a non-`published` listing (404? "no longer available"?).
- G2. Active chat when the listing expires/closes.
- G3. Stale WhatsApp deep-link reference to a dead listing.
- G4. New chat initiated on a just-expired/closed listing (race; FR-16 gates on contact pref, not status).
- G5. Thread continuity across expiry→renew.

## H. Category deactivation/removal
- H1. "Published but hidden" not a modeled state (status/visibility mismatch).
- H2. Open chats under a deactivated category.
- H3. Pending/fee_required listings during deactivation (can admin still approve/publish?).
- H4. Reactivation behavior + expiry clock while hidden.
- H5. Remove vs deactivate — fate of listings under a removed category.
- H6. Category move/reorder; target may have different required attributes.
- H7. Attribute schema change on a populated category (orphaned values, broken filters).
- H8. Adding a required attribute retroactively (existing listings now invalid).

## I. Concurrent admin actions
- I1. Multiple admins / no concurrency control (approve vs reject race).
- I2. Admin fee-requirement vs seller close/delete.
- I3. Admin approve vs seller edit (which wins).
- I4. Badge grant vs account deletion/number-unverify.
- I5. Category deactivation vs concurrent approval.
- I6. No admin-role granularity vs audit requirement.

## J. Abuse / spam (scam reporting dropped from v1)
- J1. No post-publication report path at all.
- J2. No in-chat reporting/blocking/muting.
- J3. Buyer-side spam to sellers (email-only buyers; no chat rate limit).
- J4. Fake buyer accounts (disposable, email-only).
- J5. Prohibited/illegal goods that slip past moderation — no after-the-fact surface.
- J6. Minor-edit scam injection (see B3) + J1 = undetectable post-approval abuse.
- J7. Duplicate/repost spam; UJ-3 relies on admin memory.
- J8. Number harvesting despite sign-in gate (email-only signup).
- J9. No blocklist for repeat offenders (no ban; number reuse not blocked).
- J10. No chat data retention for safety/evidence.

## K. Chats on listing reject/remove
- K1. Chats on a listing later rejected via edit re-moderation.
- K2. Orphaned threads on listing deletion/close.
- K3. Broken references in notifications to a removed listing/thread.
- K4. Chat history survival vs listing removal (no retention policy).
- K5. Notifying the other party when a thread becomes dead.

## Cross-cutting
- X1. Email as a single notification point of failure.
- X2. Moderation SLA-breach behavior undefined.

## Top 5 most important
1. PayHere success-but-no-callback + no refund path anywhere (C1, C2).
2. No user-level ban/report/block + scam reporting dropped (J1, J2, F8).
3. Number change orphans live WhatsApp listings (D5).
4. Minor-edit moderation bypass (B3).
5. Seller account deletion entirely undefined (F1–F6).

Total: ~86 unhandled cases across 12 areas.

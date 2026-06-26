# Adversarial Review — TradeZone PRD (2026-06-26)

Reviewer stance: cynical, assume-the-worst. Findings cite specific sections/FRs.

## CRITICAL

**C1 — Badge process depends on a feature that doesn't exist in v1.** §4.2/FR-5 grant the Verification Badge after offline vetting including "review of the seller's listing reviews and marketplace presence." But §6.2 defers two-sided ratings/reviews to v1.1. The flagship trust mechanism is gated on on-platform data that cannot exist at launch. Either reword (vet via existing listings + external reputation) or pull reviews into v1.

**C2 — "Trust is the product," yet recognized trust mechanisms are deferred.** §1/§16 stake the brand on trust. The addendum lists ratings, in-app scam-keyword detection, number masking, safe-meetup guidance as table-stakes — v1 ships none. What remains (WhatsApp-OTP = number control not identity, email, content moderation) does not stop the scam UJ-4 dramatizes (a verified seller asking for a deposit in chat).

**C3 — Primary "trust working" metric has no instrument.** SM-3 measures substantiated fraud complaints per 100 listings, but buyer reporting is deferred (§6.2). No FR lets a buyer report fraud or substantiates a complaint. The flagship KPI is unmeasurable in v1.

**C4 — Cold-start mitigation is asserted, not designed — and the trust apparatus fights it.** §15 names cold-start "highest" risk; mitigation is "seed… keep listing free" with no plan/number/owner/timeline. Meanwhile mandatory WhatsApp-OTP + email + wait-for-moderation pile friction on the supply side, versus incumbents' free instant posting.

## HIGH
- **H1** Human-moderate-EVERY-listing has no scaling model; a singular "Admin" + undefined "operating hours" SLA (SM-6). Success scales the queue past one human.
- **H2** Badge economics claimed to work with zero numbers (fee = Open Q#1; SM-5 target placeholder). Offline showroom visits have real cost.
- **H3** FR-9 "minor edits publish immediately" is undefined and a content-swap exploit defeating §5's every-listing gate.
- **H4** WhatsApp-OTP mechanism unresolved (Business API vs SMS vs link), policy-volatile; "email fallback" kills the WhatsApp-native positioning.
- **H5** Only sellers are verified; buyers need only email confirmation, exposing the scarce seller side to fake buyers/time-wasters.
- **H6** UJ-1 "notified instantly" contradicts FR-19 (in-app + email only; WhatsApp/push deferred) for a WhatsApp-first audience.

## MEDIUM
- **M1** "Fee required → pay → auto-publish" can skip content review (is "fee required" implicit content approval?).
- **M2** Renewal vs. fees undefined (does renewing a high-value listing re-charge?).
- **M3** Untestable adjectives: FR-14 synonym scope (Open Q#5), FR-15 "behave reliably", §10 "feel instant", FR-16 "real time".
- **M4** SM-C3 audit has no independent auditor (single admin audits own work).
- **M5** Price optional (FR-8) but discovery filters/sorts on price (FR-13/15) — price-less listing behavior unspecified.
- **M6** 10 photos × 10 MB = up to 100 MB/listing vs §10 "feel instant" on mobile data; no client-side upload constraint.
- **M7** Changed WhatsApp number vs already-published WhatsApp-contact listings (stale number) unhandled.

## LOW
- **L1** Entire SM framework is placeholders (Open Q#2); SM-1 (~200/90d) may be sandbagged.
- **L2** "Large-scale seller" never defined/measurable; "marketplace presence" circular for a new marketplace.
- **L3** Working title still "confirm".
- **L4** Accessibility aspiration without criteria.
- **L5** Result-card "location" assumes a District attribute exists.
- **L6** Buyer-side confusion that PayHere "paying" = paying for goods; add a UX guardrail.

## Counts
critical 4 · high 6 · medium 7 · low 6 · total 23

## Overall verdict
Well-structured and unusually self-aware, but as written it sells "trust as the product" while deferring/omitting every recognized trust mechanism, and bets on a cold-start it mitigates with hope. Several flagship claims are untestable or self-contradicting and should be resolved before build.

# TradeZone PRD — Addendum

Depth that belongs to downstream documents (architecture, UX, solution design), preserved here so the PRD stays capability-focused.

## Technical-how (for architecture)

- **WhatsApp OTP delivery mechanism.** The PRD requires WhatsApp-OTP seller verification but is mechanism-agnostic. Architecture must choose between WhatsApp Business API (programmatic OTP templates, requires Meta approval + a BSP) vs. SMS fallback vs. a link-based confirm. Implications for cost, deliverability, and policy compliance to be evaluated.
- **WhatsApp contact (deep-link).** `https://wa.me/<number>?text=<listing ref>` style deep-link vs. masked-number relay. Brief specifies a direct WhatsApp link; research shows OLX uses number masking to reduce scraping/abuse — a masking option is worth evaluating (see PRD §11.2 privacy assumption).
- **PayHere integration.** Gateway selected for Listing Fees / Badge fees only (never goods). Architecture must implement secure server-side callback handling with signature verification and idempotent "publish-on-payment-success" so a retried callback can't double-publish or double-charge.
- **Search/discovery engine.** Typo/synonym tolerance and persistent attribute filters imply a real search backend (e.g. an indexed search service) rather than naive SQL LIKE. Synonym dictionary for SL vehicle terms (tuk-tuk ↔ three-wheeler, etc.) to be curated.
- **Rich-text sanitization.** Server-side sanitization library/policy for seller Descriptions to prevent stored XSS.
- **Image pipeline.** Upload limits, resizing/compression, and CDN delivery for image-heavy listing pages on mobile networks.

## Decisions & rationale captured (also in .memlog.md)

- **Platform v1 = responsive web only** (native apps deferred). Rationale: faster to market, mobile-browser reach covers SL audience; chosen over native to reduce v1 cost. (Overrode an earlier "web + mobile" assumption.)
- **Fee model = free to list by default; admin requires a fee only on HIGH-VALUE listings; Verification Badge is paid.** Keeps listing free to fight cold-start vs. free incumbents; monetizes high-value transactions and the trust badge. (Promoted/featured placements deferred as a future lever.)
- **Verification Badge = large-scale sellers only (dealers/showrooms), granted via OFFLINE vetting** (physical showroom visit + check of listing reviews + marketplace presence), then paid via PayHere. Chosen over a self-serve document upload for a far stronger trust signal; trade-off is that vetting is high-effort and does not scale, hence badge is paid and reserved for low-volume large sellers.
- **Language at launch = English UI;** Sinhala + Tamil deferred to a later phase. (Overrode an earlier "all three at launch" decision to reduce v1 scope.)
- **Ratings/reviews deferred to v1.1** fast-follow; **scam-warning + reporting** dropped from v1.
- **Listing media = up to 10 photos, ≤10 MB each. Listing expiry = 60 days, renewable.**
- **Gateway = PayHere.** Chosen over Genie/FriMi (not re-litigated in PRD).
- **v1 hardening added after reviewer gate (user-approved):** payment reconciliation + refund/credit path (FR-14); admin suspend/ban user (FR-22) + lightweight buyer report-a-listing (FR-20); account deletion/deactivation with a stated policy (FR-4). Edit-bypass closed by a tight non-content whitelist in FR-10. SM-3 re-instrumented to use reports + admin-detected fraud + support complaints. Remaining ~80 edge cases deferred to architecture/UX (see `review-edge-cases.md`).

## Recovered strategic nuances (from brief reconciliation)

- **WhatsApp differentiation = verified identity, not the deep-link.** A WhatsApp contact button alone is not unique (ikman has one); the edge is *verified WhatsApp identity*. Re-added to PRD §11.1.
- **Cost is a positioning bet, not a moat** — a well-funded incumbent can match free-to-list. Re-added to PRD §1 and §11.3.
- **Price restored as a third headline force** alongside trust + discovery in the Vision (brief led with price + trust).

## Market-research context (for positioning / UX)

- Incumbents: ikman.lk and Riyasewana entrenched; basic listings are actually *free* on both (cost is promotions/memberships, plus Riyasewana's Rs.650 fee for unregistered vehicles) — clarifies what "cheaper" must mean.
- Global comparables' #1 discovery complaints: non-sticky filters, category drift, stale "sold" listings, unstructured data — TradeZone's admin-curated taxonomy + expiry + structured filters are the direct counters.
- Trust table-stakes elsewhere: identity verification, two-sided ratings, in-app scam-keyword detection, number masking, safe-meetup guidance.

## Acknowledged risk (recorded, not re-litigated)

- Cold-start / two-sided liquidity vs. free entrenched incumbents; charging to list is contrarian. You have chosen to proceed; mitigations are in PRD §15.

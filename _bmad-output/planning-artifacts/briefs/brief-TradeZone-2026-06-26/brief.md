---
title: "Product Brief: TradeZone"
status: ready
created: 2026-06-26
updated: 2026-06-26
---

# Product Brief: TradeZone

## Executive Summary

TradeZone is an online marketplace for Sri Lanka that connects buyers and sellers of second-hand and new goods across **many categories**, all defined by the system admin. Vehicles (cars, vans, jeeps, three-wheelers, bikes, lorries, buses) are the first category to consider, but the platform is built as a general, multi-category marketplace from the start. It is a *listing and contact* platform, not a payment platform: TradeZone never handles money for the goods themselves. Its job is to put a genuine seller in front of an interested buyer and let them talk — through in-app chat or a direct WhatsApp link.

Two things set it apart from the entrenched incumbents (ikman.lk and Riyasewana). First, **price**: listing on TradeZone costs sellers less than the established platforms, and the admin can decide per-listing whether a fee applies at all. Second, **trust**: every seller is verified via WhatsApp OTP and email, every listing is reviewed by an admin before it goes live, and sellers can earn a verification badge after an identity review. In a market where advance-payment fraud and fake sellers are the most common complaint, TradeZone positions itself as the *clean, verified, no-junk* place to buy and sell.

The platform serves Sri Lanka only, with categories opened and managed by the admin over time.

## The Problem

Sri Lankans actively buy and sell online, but the experience has two persistent pains:

- **Cost for sellers.** The dominant platforms are perceived as expensive once a seller wants real visibility — promotions, "bump up," top-ad placements, and business memberships add up. `[ASSUMPTION: your stated driver is that ikman/Riyasewana feel expensive; note that basic listings on both are actually free, with cost coming from promotions/memberships and Riyasewana's Rs.650 fee for unregistered vehicles. Worth confirming exactly which costs you're undercutting.]`
- **Trust and fraud.** This is the larger, genuinely unsolved problem. Advance-payment scams ("send a deposit to reserve"), fake listings, impersonation, and fake bank-transfer screenshots are widespread, and Sri Lanka Police regularly warn the public. No major platform mandates strong verification of every seller — verification today is light (a phone SMS confirm at most), so buyers carry all the risk.

Buyers waste time on time-wasters and scams; honest sellers struggle to stand out from the noise and prove they're genuine.

## The Solution

TradeZone is a moderated, verified marketplace:

- **Admin-defined categories.** The admin creates and manages the categories sellers can list under (vehicles is the first to be populated; more categories are opened over time).
- **One account, chosen role.** At signup a user provides email, a phone number, and address, and chooses to be a **Seller, a Buyer, or both**.
- **Verified sellers.** Sellers verify their WhatsApp number via OTP and confirm their email before they can list. Sellers (individuals or companies) can request a **verification badge**; the admin reviews their profile and grants it if genuine.
- **Rich listings.** Sellers list an item under a category with a title, photos, and a formatted description (headings, bold, highlights, etc.). Price is **optional**. Sellers state their preferred contact method — in-app chat or WhatsApp.
- **Admin-moderated.** Every new listing goes to the TradeZone admin, who can **approve, reject, or require a payment** before it is published. If a fee is required, the seller is prompted to pay through a payment gateway; once paid, the admin publishes the listing and is notified.
- **Buyer experience.** Buyers browse or search categories, open an item to see full details and the seller's contact preference. If the seller allows in-app chat, the buyer messages them and the seller is notified to start a live conversation; if the seller prefers WhatsApp, a tap opens a WhatsApp chat with the seller.
- **Admin control.** A separate admin login gives full control of the platform: categories, listing moderation, fee requests, verification decisions, and notifications.

No payment for the goods ever flows through TradeZone — it only connects the two parties.

## What Makes This Different

Honest read, informed by the market:

- **Trust as the product (strongest wedge).** Mandatory verified sellers + admin review of every listing directly attacks the #1 pain (fraud) that no incumbent fully solves. This is the most defensible differentiator — *if* verification is real and hard to spoof.
- **Lower cost to list.** A cheaper, admin-discretionary fee model vs. incumbents. `[ASSUMPTION: this is a positioning bet, not a moat — it can be matched by a well-funded incumbent.]`
- **WhatsApp-native onboarding.** WhatsApp OTP and a WhatsApp-first contact flow fit Sri Lankan behaviour (WhatsApp is effectively the national messaging layer). Note: a WhatsApp *contact button* alone is **not unique** — ikman already has one — so the differentiation must come from verified WhatsApp identity, not the deep-link itself.

`[RISK — acknowledged by you, recorded honestly: ikman.lk and Riyasewana are entrenched with large buyer+seller bases. A cheaper, newer platform faces a cold-start problem (buyers follow listings, sellers follow buyers). Charging to list is contrarian when competitors let you list free. You have chosen to proceed regardless; this brief records the risk rather than re-litigating it.]`

## Who This Serves

- **Sellers.** Individuals and companies across any category the admin opens (vehicles first) who want a cheaper, trustworthy place to list and to signal they are genuine.
- **Buyers.** Sri Lankans searching across categories who want to deal with verified sellers and avoid scams.
- **Admin (TradeZone operator).** You — full control over categories, moderation, fees, and verification; the human quality gate that makes "trusted marketplace" real.

Sri Lanka only.

## Success Criteria

`[ASSUMPTION: you haven't set targets yet — these are placeholder signals to refine.]`

- **Liquidity:** enough live, genuine vehicle listings that buyers find real choice (e.g. first milestone: N active verified sellers and M live listings in the launch category).
- **Trust working:** low rate of scam/fraud reports per listing vs. the market reputation; meaningful share of sellers seeking the verification badge.
- **Engagement:** buyer→seller contacts initiated per listing (chat opens + WhatsApp taps).
- **Business:** paid listings and verification badges generating revenue, while keeping fees below incumbents.
- **Operational:** admin moderation turnaround fast enough that sellers don't defect to instant-post rivals (incumbents approve in ~instant–30 min).

## Scope

**In (v1):**
- Admin-defined categories (vehicles first, e.g. car, van, jeep, three-wheeler, bike, lorry, bus; admin can add more).
- Signup with role selection (seller / buyer / both); email + phone + address.
- Seller WhatsApp OTP + email verification.
- Listing creation under a category: title, photos, rich-text description, optional price, preferred contact.
- Admin moderation: approve / reject / request payment; payment gateway for listing fees; publish + notify.
- Verification badge request + admin review.
- Buyer browse/search across categories, item detail, in-app chat (with seller notification) and WhatsApp deep-link.
- Separate admin panel with full control.

**Out (for now):**
- Handling payment for the goods themselves (always out — platform connects only).
- `[ASSUMPTION: ratings/reviews, dispute handling, mobile apps, multi-language (Sinhala/Tamil) — desirable later, not v1 unless you say otherwise.]`

## Vision

If it works, TradeZone becomes Sri Lanka's *trusted* marketplace — the place where every seller is a verified, real person and every listing has been checked, across all the categories the admin opens up, with trust (not just listing volume) as the brand promise that pulls buyers and sellers away from the noise of free-but-risky alternatives.

---

### Open Questions / To Confirm
1. Exact fee model: free-to-list with paid extras, or a flat cheap per-listing fee? What does "cheaper than ikman/Riyasewana" mean concretely?
2. Which payment gateway (PayHere / Genie / FriMi) for charging sellers?
3. Multi-language (Sinhala/Tamil) at launch or English first?
4. Concrete launch targets for the success criteria.

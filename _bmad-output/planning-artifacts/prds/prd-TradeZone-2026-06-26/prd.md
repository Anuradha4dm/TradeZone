---
title: TradeZone
status: final
created: 2026-06-26
updated: 2026-06-26
---

# PRD: TradeZone
*Working title — confirm.*

## 0. Document Purpose

This PRD is the source of truth for TradeZone's first launch (v1). It is written for the product owner/admin (you) and the downstream UX, architecture, and engineering workflows. It builds on `briefs/brief-TradeZone-2026-06-26/brief.md` (the approved product brief) and a market-research digest captured in `.memlog.md`; it does not duplicate them. Structure: vocabulary is anchored in the Glossary (§3); features are grouped with Functional Requirements (FRs) nested and globally numbered; cross-cutting non-functional requirements live in §10; assumptions are tagged inline as `[ASSUMPTION: ...]` and indexed in §9. Implementation and technology choices are kept out of the FRs and recorded in `addendum.md`. Detailed edge-case handling delegated to architecture/UX is tracked in `review-edge-cases.md`.

## 1. Vision

TradeZone is Sri Lanka's **trusted** online marketplace — a place where every seller is a verified, real person and every listing has been checked by a human before it goes live. It connects buyers and sellers of new and second-hand goods across categories the admin opens over time, starting with **vehicles** (cars, vans, jeeps, three-wheelers, bikes, lorries, buses). TradeZone is a *listing and contact* platform: it never touches money for the goods themselves. Its entire job is to put a genuine seller in front of an interested buyer and make that connection fast, safe, and easy.

Three forces shape the product. **Trust** is the lead: fraud is the unsolved problem in Sri Lankan online trading — advance-payment scams, fake sellers, and doctored bank screenshots are routine, and no incumbent mandates strong verification. TradeZone makes trust the product through mandatory WhatsApp-OTP + email verification for every seller, human moderation of every listing, and a paid, offline-vetted Verification Badge for large-scale dealers. **Discovery** is the second force: finding the right item is hard everywhere else — search is cluttered, filters don't hold, sold items linger — so TradeZone treats discovery as first-class, with admin-curated categories, structured attributes, persistent filters, and listings that expire or close when sold. **Price** is the third: listing is free by default (a fee applies only to high-value listings at the admin's discretion), undercutting the perceived cost of incumbents — a deliberate positioning bet, not a defensible moat, since a well-funded incumbent could match it.

If it works, TradeZone becomes the clean, verified, no-junk place Sri Lankans go to buy and sell — where trust, not raw listing volume, is the brand promise that pulls people away from free-but-risky alternatives.

## 2. Target User

### 2.1 Jobs To Be Done

**Buyers**
- When I'm shopping for an item (e.g. a used three-wheeler), I want to *quickly find genuine options that match my needs* so I don't waste hours scrolling junk and duplicates.
- When I find something I like, I want to *reach the seller easily and safely* so I can ask questions and arrange the deal.
- When I deal with a stranger online, I want *confidence the seller is real* so I don't get scammed out of a deposit.

**Sellers**
- When I have something to sell, I want to *list it cheaply and have it actually seen by buyers* so it sells without paying for expensive promotions.
- When I'm a genuine large-scale seller, I want to *prove I'm a vetted dealer* so buyers contact me with confidence.
- When a buyer is interested, I want to *be notified and talk to them on my preferred channel* (in-app or WhatsApp) so I don't miss the sale.

**Admin (TradeZone operator)**
- I want to *control which categories exist, what gets published, and who is verified* so the marketplace stays clean and trustworthy.
- I want to *decide whether a fee applies to high-value listings and collect it* so the platform earns revenue without driving sellers away.
- I want to *remove bad listings and ban bad actors* so trust is enforced, not just promised.

### 2.2 Non-Users (v1)
- Buyers/sellers outside Sri Lanka — TradeZone targets SL; geo-restriction is soft (positioning/targeting only, anyone can browse).
- Sellers who want TradeZone to process payment for goods or hold funds in escrow — explicitly not offered.
- Pure-service providers (e.g. plumbers, tutors) unless the admin opens a services category; v1 focus is physical goods, vehicles first.
- Small/individual sellers seeking a Verification Badge — the badge is reserved for vetted large-scale sellers (dealers/showrooms); individuals still list with baseline Seller Verification.

### 2.3 Key User Journeys

**UJ-1. Nimal finds a verified three-wheeler and messages the seller in minutes.**
Nimal, a self-employed delivery driver in Gampaha shopping for a used three-wheeler under Rs. 900,000, has been burned before by a fake deposit scam on another site. Unauthenticated, he lands on TradeZone, opens **Vehicles → Three-wheelers**, and applies filters: price ceiling, brand, year, district. The list shows only live, admin-approved listings, each with photos and a clear **Verification Badge** where the seller is a vetted dealer. He opens one, reads the formatted description, sees the seller is verified, and taps **Chat**. He's prompted to sign in (or quick-register as a buyer), then sends "Is this still available? Can I see it this weekend?" The seller is notified (in-app + email). **Climax:** within minutes he's in a conversation with a real, verified seller about a real, checked listing. **Resolution:** they agree to meet; Nimal never had to send money to anyone online. **Edge case:** if the seller's preferred contact is WhatsApp, the **Contact** button instead opens a WhatsApp chat with the seller's verified number, pre-filled with the listing reference.

**UJ-2. Shirani lists her late father's van and gets it published the same day.**
Shirani, selling a family van, registers and chooses role **Seller (and Buyer)**. Before she can list, TradeZone requires her to verify: she enters her WhatsApp number, receives an OTP, confirms it, and clicks the email confirmation link. Now able to list, she picks **Vehicles → Vans**, uploads 8 photos, writes a description with headings and bold highlights, sets a price (optional, she includes it), and chooses **in-app chat** as her contact method. She submits. **Climax:** the listing goes to the admin queue; the admin reviews it, decides no fee is needed, and approves it — Shirani is notified it's live. **Resolution:** her van is discoverable. **Edge case:** if the admin judges the listing high-value and requires a fee, Shirani is prompted to pay via PayHere, and the listing publishes automatically once payment succeeds.

**UJ-3. The admin keeps the marketplace clean from one panel.**
The admin logs into the separate admin panel, sees a queue of pending listings, opens each, and checks photos/description/category fit. One is a duplicate of a removed scam listing — **rejected** with a reason, and the repeat-offender account is **banned**. One is a high-value car — **approved with a fee required**. A showroom has requested a **Verification Badge**; the admin schedules the offline review (physical showroom visit, check of the seller's existing listings and external reputation) and, once satisfied, grants it. **Climax:** in one session the admin has shaped exactly what buyers will see. **Resolution:** sellers are notified of each decision; the public marketplace reflects only approved, checked content.

**UJ-4. Priya trusts the badge and picks the vetted dealer.**
Priya is comparing two similar bike listings. One seller carries the **Verification Badge** — a dealer TradeZone physically vetted; the other is an unbadged individual who, in chat, pushes her to "pay a deposit to reserve via bank transfer." **Climax:** the badge gives Priya a clear, platform-backed reason to trust one seller over the other; the deposit-first ask from the unbadged seller reads as the red flag it is, and she **reports** the listing. **Resolution:** she proceeds with the badged dealer and arranges to view the bike in person — she never wires a deposit to a stranger; the admin reviews her report and removes the bad listing.

## 3. Glossary

- **TradeZone** — The marketplace platform described by this PRD. Sri Lanka only (soft geo-targeting).
- **User** — Any registered person. Has one account and one or more **Roles**.
- **Role** — The capacity a User acts in: **Buyer**, **Seller**, or **both**. Chosen at signup; a User may hold both.
- **Buyer** — A User browsing/searching listings and contacting Sellers. No verification required to browse; sign-in required to initiate contact.
- **Seller** — A User who creates **Listings**. Must complete **Seller Verification** before listing.
- **Admin** — The TradeZone operator (one or more operator accounts). Uses the separate **Admin Panel**. Controls Categories, listing **Moderation**, **Listing Fees**, **Verification Badge** decisions, **Reports**, and User bans.
- **Category** — An admin-defined classification a Listing belongs to (e.g. Vehicles → Three-wheelers). May define **Attributes**. Organized hierarchically (a Category may have sub-categories). `[ASSUMPTION: two-level hierarchy is enough for v1.]`
- **Attribute** — A structured field on a Category used for filtering/search (e.g. Brand, Year, District, Mileage). Admin-defined per Category.
- **Listing** — A single item a Seller offers under one Category: title, photos, rich-text **Description**, optional **Price**, **Contact Preference**, and Attribute values. Has a **Listing Status**.
- **Listing Status** — Lifecycle state of a Listing: `pending` (awaiting Moderation) → `fee_required` → `published` → `closed`/`expired`/`rejected`.
- **Moderation** — Admin review of a Listing before it is published: approve, reject (with reason), or require a fee.
- **Listing Fee** — An admin-discretionary charge required only on **high-value** Listings, paid by the Seller via **PayHere** before publication. Most Listings are free.
- **Seller Verification** — Mandatory checks every Seller completes before listing: **WhatsApp OTP** + **Email Verification**.
- **WhatsApp OTP** — A one-time code sent to the Seller's WhatsApp number to verify ownership of that number.
- **Verification Badge** — An earned, paid trust marker granted by the Admin to a vetted **large-scale Seller** (dealer/showroom) after an *offline* review. Distinct from, and stronger than, baseline Seller Verification.
- **Contact Preference** — The Seller's chosen channel for buyer contact on a Listing: **In-App Chat** or **WhatsApp**.
- **In-App Chat** — A messaging conversation between a Buyer and Seller inside TradeZone, with notifications.
- **WhatsApp Deep-Link** — A tap that opens WhatsApp pointed at the Seller's verified number, pre-filled with a Listing reference.
- **Report** — A buyer-initiated flag on a Listing that enters the Admin's review queue.
- **PayHere** — The Sri Lankan payment gateway used to collect Listing Fees and Verification Badge fees. Never used for goods.
- **Admin Panel** — The separate, admin-only interface for full platform control.

## 4. Features

### 4.1 Accounts & Roles
**Description:** A single account model where any User registers with email, phone number, and address, and selects a Role of Buyer, Seller, or both. Browsing is open to everyone; initiating contact requires sign-in. Realizes UJ-1, UJ-2.

**Functional Requirements:**

#### FR-1: Registration with role selection
A visitor can register a User account providing email, phone number, and address, and selecting Role = Buyer, Seller, or both. Realizes UJ-2.

**Consequences (testable):**
- Account cannot be created without a valid email format, a phone number, and a non-empty address.
- A User may select Buyer, Seller, or both; the selection is stored and editable later in profile.
- Email must be confirmed via a verification link before the account is considered email-verified.
- Duplicate registration with an already-registered email is rejected with a clear message.

#### FR-2: Authentication & session
A User can sign in and maintain an authenticated session; an unauthenticated visitor can browse and search but cannot initiate contact or list.

**Consequences (testable):**
- Unauthenticated users can view Categories, search, and open Listing detail pages.
- Initiating In-App Chat or revealing a WhatsApp Deep-Link requires sign-in; the user is prompted to sign in/register at that point and returned to the Listing afterward. `[ASSUMPTION: WhatsApp number reveal requires sign-in, to deter scraping — confirm.]`
- Standard password reset via email is available.

#### FR-3: Profile management
A User can view and edit their profile (contact details, address, role), subject to re-verification when verification-critical fields change.

**Consequences (testable):**
- Changing the WhatsApp number invalidates WhatsApp verification and requires a new WhatsApp OTP before the User can list again.
- Changing email requires re-confirmation via link.

#### FR-4: Account deletion / deactivation
A User can delete or deactivate their account; the system applies a defined policy to their listings, conversations, and outstanding fees.

**Consequences (testable):**
- On account deletion, the User's `published` Listings are removed from discovery (set to `closed`) and their `pending`/`fee_required` Listings are withdrawn from the Moderation queue.
- Active In-App Chat threads tied to the deleted account are closed; the counterpart is notified the participant is no longer available, and message history is retained per the data-retention policy. `[ASSUMPTION: chat history retained for a defined window for safety/audit — confirm duration.]`
- Any unpaid Listing Fee or Badge fee obligation is voided; refunds for already-paid fees follow FR-14.
- A deactivated (vs deleted) account hides the User's listings and pauses contact but preserves data for later reactivation. `[ASSUMPTION: deactivate = reversible hide; delete = irreversible removal — confirm.]`

### 4.2 Seller Verification & Trust
**Description:** Trust is TradeZone's core differentiator. Every Seller must verify a WhatsApp number (via OTP) and confirm email before listing. Large-scale Sellers (dealers/showrooms) may additionally earn a paid Verification Badge, granted by the Admin after an *offline* review — a physical showroom visit plus checks of the seller's existing listings and external (off-platform) reputation. Realizes UJ-2, UJ-3, UJ-4.

**Functional Requirements:**

#### FR-5: Mandatory seller verification before listing
A Seller can only create or publish a Listing after completing WhatsApp OTP verification and Email Verification. Realizes UJ-2.

**Consequences (testable):**
- A Seller who has not passed WhatsApp OTP cannot submit a Listing; the listing entry point is blocked with guidance to verify.
- WhatsApp OTP: a code is sent to the entered WhatsApp number; entry of the correct code within its validity window marks the number verified; expired/incorrect codes are rejected and can be resent (rate-limited).
- Email Verification status is required in addition to WhatsApp OTP.

#### FR-6: Verification badge request & offline review
A large-scale Seller can request a Verification Badge; the Admin grants or declines it after an offline vetting process and, when granted, collects the badge fee via PayHere. Realizes UJ-3, UJ-4.

**Consequences (testable):**
- A verified Seller can submit a badge request indicating they are a large-scale seller (dealer/showroom).
- The badge is granted only after the Admin completes offline vetting (physical showroom visit + review of the seller's existing listings and external reputation) and records the outcome. The vetting does **not** rely on on-platform ratings/reviews (deferred to v1.1).
- The Verification Badge is paid: on the Admin's grant, the Seller pays the badge fee via PayHere; the badge becomes active on payment success. `[ASSUMPTION: badge fee is one-time for v1; recurring renewal deferred — confirm.]`
- A granted, paid badge is visually distinct from baseline verification and shown wherever the Seller appears to Buyers; a declined request notifies the Seller with a reason.
- The Admin can revoke a granted badge (e.g. on misconduct); revocation notifies the Seller and removes the badge from their listings.

### 4.3 Categories & Taxonomy
**Description:** The admin defines the Categories (and sub-categories) sellers can list under, and the structured Attributes each Category exposes for filtering/search. Vehicles is the first category populated. This admin-curated taxonomy is what makes TradeZone's discovery cleaner than free-form competitors. Realizes UJ-1.

**Functional Requirements:**

#### FR-7: Admin category management
The Admin can create, edit, reorder, activate/deactivate, and remove Categories and sub-categories.

**Consequences (testable):**
- A new Category becomes selectable by Sellers only when active.
- Deactivating a Category hides it from Buyers and prevents new Listings under it; existing Listings under it are hidden but retained, not deleted. `[ASSUMPTION: hide-and-retain on deactivation; reactivation restores them — confirm.]`
- The initial Vehicles category supports sub-categories: car, van, jeep, three-wheeler, bike, lorry, bus.

#### FR-8: Admin attribute schema per category
The Admin can define structured Attributes per Category (type, allowed values, whether filterable/required) to drive search and filtering.

**Consequences (testable):**
- An Attribute can be defined as a select/enum (e.g. Brand), numeric range (e.g. Year, Price, Mileage), or location (District).
- Filterable Attributes appear as Buyer-facing filters on that Category.
- Required Attributes must be supplied by the Seller at Listing creation.

### 4.4 Listing Creation & Management
**Description:** Verified Sellers create rich Listings under a Category with title, photos, formatted description, optional price, Attribute values, and a Contact Preference. Sellers can manage their listings (edit, mark sold/closed). Realizes UJ-2.

**Functional Requirements:**

#### FR-9: Create a listing
A verified Seller can create a Listing under a Category with a title, one or more photos, a rich-text Description, optional Price, required/optional Attribute values, and a Contact Preference (In-App Chat or WhatsApp). Realizes UJ-2.

**Consequences (testable):**
- A Listing requires title, Category, at least one photo, and all required Attributes; Price is optional.
- The Description supports formatting: headings, bold, highlights/lists. `[ASSUMPTION: rich-text is sanitized server-side to prevent script injection.]`
- Photos: up to 10 per Listing, each ≤ 10 MB; the client compresses/resizes images before upload to protect mobile-data performance. `[ASSUMPTION: client-side compression target to be set in UX/architecture.]`
- On submission the Listing enters `pending` status (awaiting Moderation); it is not yet visible to Buyers.

#### FR-10: Manage own listings
A Seller can view, edit, and change the status of their own Listings; any content edit returns the Listing to Moderation, while a tightly-scoped set of non-content changes publish immediately.

**Consequences (testable):**
- A Seller can mark a published Listing as `closed` (sold), removing it from active discovery.
- Editing any **content** of a published Listing — title, Description, photos, Category/sub-category, or Attribute values — returns it to `pending` for re-Moderation.
- Only these non-content changes publish immediately without re-Moderation: lowering the Price, marking as `closed`, and changing Contact Preference. Any other change is treated as content and re-moderated. (This closed whitelist prevents post-approval content swaps.)
- A Seller can see the current status of each Listing (pending, fee_required, published, rejected, closed, expired).

#### FR-11: Listing expiry / freshness
A published Listing automatically expires after 60 days, keeping discovery free of stale items; the Seller can renew.

**Consequences (testable):**
- A published Listing expires 60 days after publication and moves to `expired`, leaving active discovery.
- The Seller is notified before/at expiry and can renew/republish; renewal re-enters Moderation only if it includes a content edit (per FR-10). `[ASSUMPTION: an unchanged renewal of a previously-approved listing republishes without re-moderation — confirm.]`

### 4.5 Listing Moderation & Fees
**Description:** Every new and content-edited Listing is reviewed by the Admin before publication. The Admin can approve, reject with a reason, or — for high-value listings — require a fee; if a fee is required, the Seller pays via PayHere and the Listing publishes automatically on success. Payment outcomes are reconciled so a Seller is never charged without publication. Realizes UJ-2, UJ-3.

**Functional Requirements:**

#### FR-12: Moderation queue & decisions
The Admin can view all `pending` Listings and, per Listing, approve, reject (with reason), or require a Listing Fee (used for high-value listings). Realizes UJ-3.

**Consequences (testable):**
- Approving moves the Listing to `published` and notifies the Seller.
- Rejecting moves it to `rejected`, records a reason, and notifies the Seller with that reason; a `rejected` Listing can be edited and resubmitted, re-entering `pending`.
- Requiring a fee moves the Listing to `fee_required`, sets the fee amount, and notifies the Seller to pay. Requiring a fee implies the content is otherwise approved: on successful payment the Listing publishes without a further content review.

#### FR-13: Listing fee payment via PayHere
When a fee is required, the Seller can pay it through PayHere; on successful payment the Listing publishes automatically and the Admin is notified.

**Consequences (testable):**
- A `fee_required` Listing presents the Seller a PayHere payment flow for the specified amount.
- On PayHere success callback (signature-verified), the Listing transitions to `published` automatically and the Admin is notified.
- On payment failure/abandonment, the Listing stays `fee_required`; the Seller can retry.
- TradeZone never collects payment for the goods — fees apply only to high-value Listings and to the Verification Badge.

#### FR-14: Payment reconciliation & refunds
The system reconciles PayHere payments so that a successful charge always results in the intended outcome (a published Listing or an active Badge), and provides a refund/credit path when it cannot.

**Consequences (testable):**
- Every PayHere charge is reconciled against its intended outcome; a charge whose success callback is lost or delayed is detected (via reconciliation/polling) and the outcome is completed automatically. `[ASSUMPTION: reconciliation cadence/mechanism defined in architecture.]`
- If a paid Listing cannot be published (e.g. it was rejected, its Category was deactivated, or the account was deleted after payment), the Seller receives a refund or credit, and the Admin is notified.
- Duplicate/repeated successful callbacks for the same payment are idempotent — the Seller is charged once and the outcome applied once.
- Refund decisions and their reasons are auditable in the Admin Panel.

### 4.6 Discovery: Browse, Search & Filter
**Description:** The reason TradeZone exists is to make items *easy to find*. Discovery is built on the admin-curated taxonomy: Buyers browse Categories, run keyword search, and apply persistent, attribute-based filters; results show only live, approved Listings, with verified-seller status visible. This directly attacks the incumbents' biggest weakness (broken search, category drift, stale listings). Realizes UJ-1, UJ-4.

**Functional Requirements:**

#### FR-15: Browse categories
A visitor (no sign-in) can browse Categories and sub-categories and see published Listings within them. Realizes UJ-1.

**Consequences (testable):**
- Only `published` Listings appear in browse/search; pending/rejected/closed/expired never appear to Buyers.
- Each result shows title, primary photo, price (if set), Category, and, where the Category defines a District Attribute, location; the Verification Badge appears where applicable.

#### FR-16: Keyword search
A visitor can search Listings by keyword across title/description/attributes, with tolerance for common typos and synonyms. Realizes UJ-1.

**Consequences (testable):**
- Search matches across title, Description, and key Attributes.
- Search is typo/synonym tolerant for common terms `[ASSUMPTION: synonym dictionary scope, e.g. "three wheeler"/"threewheeler"/"tuk tuk" mapped together, to be curated — confirm].`
- Results default to a relevance + recency ordering, not paid-placement ordering. (No ad-injected ordering in v1; promoted placements are out of scope.)

#### FR-17: Attribute filters that persist
A visitor can apply Category-specific Attribute filters (e.g. price range, brand, year, district) that persist across pagination and refinement within the session. Realizes UJ-1.

**Consequences (testable):**
- Filters available are those the Admin marked filterable for the Category (FR-8).
- Applied filters persist while the user paginates, and refine results cumulatively.
- Sort options include newest and price (asc/desc) and behave consistently across pages.
- Listings without a Price are excluded from a price-range filter but still appear under "newest"; under a price sort they are ordered last. `[ASSUMPTION: price-less handling — confirm.]`

### 4.7 Buyer–Seller Contact
**Description:** Once a Buyer finds an item, contact must be easy. Sellers choose In-App Chat or WhatsApp per listing. In-App Chat notifies the Seller; WhatsApp opens a deep-link to the Seller's verified number. Realizes UJ-1.

**Functional Requirements:**

#### FR-18: In-app chat
A signed-in Buyer can start an In-App Chat with a Seller on a Listing whose Contact Preference is In-App Chat; the Seller is notified and both can exchange messages. Realizes UJ-1.

**Consequences (testable):**
- Starting a chat requires sign-in (FR-2); the Seller receives a notification of a new conversation.
- Messages are delivered and visible to both parties in a per-Listing conversation thread.
- Each party can view their conversations and unread indicators.
- Chat can only be initiated on a `published` Listing; when a Listing later leaves `published`, existing threads remain readable but are marked inactive and the counterpart is notified. `[ASSUMPTION: inactive-thread behavior to be detailed in UX.]`

#### FR-19: WhatsApp contact
A signed-in Buyer can contact a Seller via WhatsApp Deep-Link on a Listing whose Contact Preference is WhatsApp; the link targets the Seller's verified number, pre-filled with the Listing reference. Realizes UJ-1.

**Consequences (testable):**
- Tapping Contact opens WhatsApp (app or web) addressed to the Seller's verified WhatsApp number.
- The pre-filled message includes a reference to the Listing.
- A Listing's WhatsApp Deep-Link always targets the number currently verified for the Seller; if the Seller's number becomes unverified (FR-3), WhatsApp-contact Listings are paused from discovery until re-verified. `[ASSUMPTION: pause-until-reverified to prevent routing buyers to a stale number — confirm.]`

### 4.8 Trust & Safety: Reporting
**Description:** A lightweight buyer-facing reporting path lets the community surface bad listings the admin then acts on — the post-publication complement to pre-publication moderation. (Richer in-chat scam detection is deferred.) Realizes UJ-4.

**Functional Requirements:**

#### FR-20: Report a listing
A signed-in Buyer can report a Listing (with a reason); the Report enters the Admin's review queue. Realizes UJ-4.

**Consequences (testable):**
- A Buyer can submit a Report on a Listing with a reason; the reporter is acknowledged.
- Each Report appears in the Admin Panel queue (FR-21) for review and action (e.g. remove Listing, ban User).
- Substantiated Reports feed the trust metric (SM-3).

### 4.9 Admin Panel
**Description:** A separate, admin-only interface giving full control over the platform: Categories/Attributes, Listing Moderation and fees, Verification Badge decisions, Reports, User bans, and notifications. The Admin is the human quality gate that makes "trusted marketplace" real. Realizes UJ-3.

**Functional Requirements:**

#### FR-21: Admin control center
The Admin can, from a separate authenticated Admin Panel, manage Categories/Attributes (FR-7/FR-8), moderate Listings and set fees (FR-12), decide Verification Badges (FR-6), and review Reports (FR-20).

**Consequences (testable):**
- Admin Panel access requires separate admin authentication, distinct from User accounts; the panel supports one or more operator accounts.
- The Admin can act on each pending item (listing, badge request, report) with an auditable decision + reason.
- Admin actions that affect a Seller (approve/reject/fee/badge/report outcome) trigger a notification to that Seller.

#### FR-22: Suspend or ban a user
The Admin can suspend or ban a User; a banned User cannot sign in, list, or contact, and their active Listings are removed from discovery.

**Consequences (testable):**
- Banning a User sets their account to banned: they cannot authenticate, create Listings, or initiate contact.
- A banned User's `published` Listings are removed from discovery; in-flight obligations follow the refund rules (FR-14).
- Ban/suspend actions are auditable (who, when, reason).

### 4.10 Notifications
**Description:** Timely notifications keep the loop tight: Sellers learn moderation outcomes and new buyer contacts; Buyers learn of replies; the Admin learns of paid listings and new items needing review. Realizes UJ-1, UJ-2, UJ-3.

**Functional Requirements:**

#### FR-23: Event notifications
The system notifies Users and the Admin of the events relevant to them via in-app and email channels.

**Consequences (testable):**
- A Seller is notified on: moderation decision, fee required, listing published after payment, refund issued, new In-App Chat message, listing nearing/at expiry, badge decision, report outcome affecting them, ban/suspension.
- The Admin is notified on: new listing pending, fee paid (listing auto-published), reconciliation/refund needed, new badge request, new report.
- Notification channels for v1 are in-app + email. (WhatsApp/push notifications are deferred; email is therefore a delivery dependency — see §15.)

## 5. Non-Goals (Explicit)
- TradeZone will **not** process, hold, or escrow payment for the goods themselves — ever. It connects parties only.
- TradeZone will **not** auto-publish listings; human Moderation of every new/content-edited listing is intentional and core to the brand.
- TradeZone will **not** operate outside Sri Lanka in v1.
- TradeZone will **not** ship native iOS/Android apps in v1 (responsive web only; native is a later phase).
- TradeZone will **not** provide shipping/logistics, delivery tracking, or in-platform fulfillment.
- TradeZone will **not** become an auction platform (fixed/negotiated listings only) in v1. `[ASSUMPTION: no auctions in v1 — confirm.]`
- TradeZone will **not** grant Verification Badges to individual/small sellers in v1 — the badge is reserved for vetted large-scale dealers/showrooms.

## 6. MVP Scope

### 6.1 In Scope
- Single account with Role selection (Buyer / Seller / both); email + phone + address; account deletion/deactivation with a defined policy.
- Mandatory Seller Verification: WhatsApp OTP + Email Verification.
- Verification Badge (paid) for large-scale sellers, granted via offline admin vetting; admin can revoke.
- Admin-defined Categories/sub-categories + structured Attributes; Vehicles populated first.
- Listing creation: title, up to 10 photos (≤10 MB each), rich-text Description, optional Price, Attributes, Contact Preference.
- Listing lifecycle: pending → fee_required → published → closed/expired/rejected; 60-day expiry + renew; content edits re-moderate (tight non-content whitelist).
- Admin Moderation: approve / reject (reason) / require fee on high-value listings; PayHere fee payment → auto-publish; reconciliation + refund/credit path.
- Discovery: browse Categories, keyword search (typo/synonym tolerant), persistent attribute filters, consistent sorts.
- Buyer–Seller contact: In-App Chat (with notifications) and WhatsApp Deep-Link.
- Trust & safety: buyer report-a-listing; admin suspend/ban user.
- Separate Admin Panel with full control (one or more operator accounts).
- Notifications: in-app + email.
- Responsive web (works well on mobile browsers), **English UI** at launch.

### 6.2 Out of Scope for MVP
- Native mobile apps — deferred to a later phase (responsive web covers mobile for v1).
- Payment/escrow for goods — permanent non-goal.
- **Two-sided ratings/reviews** — planned as a **v1.1 fast-follow** (trust brand needs them soon, but not blocking launch).
- **In-chat scam-keyword detection / safety nudges** — deferred (basic report-a-listing is in v1; richer detection later).
- **Sinhala & Tamil UI** — deferred to a later phase (English first at launch).
- Dispute resolution / formal mediation — deferred.
- Saved searches, alerts, favorites/wishlists — deferred (nice-to-have for discovery).
- Promoted/featured paid placements — deferred (possible future revenue lever).
- Auctions / bidding — deferred.
- Services categories — deferred until admin opens them.
- Buyer-side identity verification — deferred (buyers are email-confirmed only in v1; see §15 risk).

## 7. Success Metrics

*All targets below are `[ASSUMPTION]` placeholders — launch targets are not yet decided (Open Question #2). Confirm or replace.*

**Primary**
- **SM-1 — Liquidity (supply):** number of live, approved Listings and active verified Sellers in the launch (Vehicles) category. Target: `[ASSUMPTION: e.g. ≥ 200 live listings and ≥ 50 verified sellers within 90 days of launch].` Validates FR-5, FR-9, FR-12.
- **SM-2 — Buyer→Seller contacts per listing:** In-App Chat opens + WhatsApp taps per published Listing. Target: `[ASSUMPTION: e.g. ≥ 1.5 contacts per live listing per month].` Validates FR-15–FR-19.
- **SM-3 — Trust working:** rate of substantiated fraud cases per 100 listings, measured from buyer Reports (FR-20), fraud caught during Moderation, and complaints via the support channel — kept well below market reputation. Target: `[ASSUMPTION: e.g. < 1 substantiated case per 100 listings].` Validates FR-5, FR-6, FR-12, FR-20, FR-22.

**Secondary**
- **SM-4 — Discovery effectiveness:** share of search/browse sessions that reach a Listing detail page (and onward to contact). Target: `[ASSUMPTION: e.g. ≥ 40% of search sessions open ≥ 1 listing].` Validates FR-15–FR-17.
- **SM-5 — Badge demand:** number of large-scale sellers earning the paid Verification Badge. Target: `[ASSUMPTION: set with business model].` Validates FR-6.
- **SM-6 — Moderation turnaround:** median time from `pending` to a moderation decision, during defined operating hours. Target: `[ASSUMPTION: e.g. < 2 hours during stated operating hours — define hours].` Validates FR-12.
- **SM-7 — Revenue:** high-value Listing fees + badge fees collected via PayHere. Target: `[ASSUMPTION: set with business model].` Validates FR-13.

**Counter-metrics (do not optimize)**
- **SM-C1 — Listing volume at the expense of quality:** raw listing count must NOT be driven up by relaxing Moderation. Counterbalances SM-1; if listing volume rises while substantiated fraud cases (SM-3) also rise, the strategy is failing.
- **SM-C2 — Fee revenue at the expense of liquidity:** high-value Listing Fees (SM-7) must NOT be raised to a point that suppresses supply (SM-1). Counterbalances SM-7.
- **SM-C3 — Moderation speed at the expense of rigor:** turnaround (SM-6) must NOT be improved by rubber-stamping; an independent sampled audit of approvals should stay clean. Counterbalances SM-6.

## 8. Open Questions
1. **Fee amounts:** concrete Rs. figures for (a) the high-value Listing fee and (b) the Verification Badge fee — and what defines "high-value" (a price threshold? specific categories? or 100% admin judgment with no rule?).
2. **Launch targets:** concrete numbers for all SM-*, and the definition of moderation "operating hours" for SM-6.
3. **Auctions:** confirm auctions are out of v1 (currently assumed).
4. **WhatsApp number exposure:** is the seller's number revealed to signed-in buyers, or kept masked behind the WhatsApp deep-link?
5. **Search synonym scope:** how far does typo/synonym tolerance go (e.g. tuk-tuk ↔ three-wheeler dictionary)?
6. **Data retention:** retention window for chat history and deleted-account data (safety/audit vs privacy).
7. **Buyer verification:** stay email-only for buyers in v1, or add buyer phone/WhatsApp verification to protect sellers?
8. **Detailed edge-case handling** (payment failure modes beyond refund, concurrency/locking, number-change orphaning, category-deactivation states, chat lifecycle) is delegated to architecture/UX — tracked in `review-edge-cases.md`; confirm that delegation.

## 9. Assumptions Index
- §3 / §4.3 FR-7 — Two-level Category hierarchy suffices for v1; Listings under a deactivated Category are hidden but retained and restored on reactivation.
- §4.1 FR-2 — WhatsApp number reveal requires sign-in (anti-scraping).
- §4.1 FR-4 — Chat history retained for a defined window; deactivate = reversible, delete = irreversible.
- §4.2 FR-6 — Badge fee is one-time for v1.
- §4.4 FR-9 — Rich-text Description is sanitized server-side; client-side image compression target set in UX/architecture.
- §4.4 FR-11 — Unchanged renewal republishes without re-moderation.
- §4.5 FR-14 — Reconciliation cadence/mechanism defined in architecture.
- §4.6 FR-16 — Typo/synonym dictionary scope to be curated.
- §4.6 FR-17 — Price-less listings excluded from price filters, ordered last under price sort.
- §4.7 FR-18 — Inactive-thread behavior detailed in UX.
- §4.7 FR-19 — WhatsApp-contact listings paused until number re-verified.
- §5 — No auctions in v1.
- §7 — All SM-* targets are placeholders pending real launch targets; "operating hours" undefined.
- §10 — Search results target < 1s p75 (to confirm); accessibility WCAG-AA-aligned, not formally certified for v1.
- §11.2 — Whether the seller's WhatsApp number is shown or masked behind the deep-link.
- §15 — WhatsApp-OTP delivery mechanism (Business API vs SMS vs link) to be defined in architecture.

## 10. Cross-Cutting NFRs
- **Performance:** discovery (browse/search/filter) targets search results in **< 1s p75** on mobile browsers over typical Sri Lankan mobile networks; image-heavy listing pages lazy-load; listing uploads are client-compressed. `[ASSUMPTION: confirm the p75 target.]`
- **Reliability/Availability:** the marketplace and Admin Panel should be highly available; Moderation and PayHere callbacks must be resilient to retries — idempotent publish on payment success, and reconciliation so no Seller is charged without the intended outcome (FR-14). `[ASSUMPTION: concrete availability target set in architecture.]`
- **Security:** server-side input sanitization (rich-text/photos), rate-limited OTP and login, protection against listing/contact scraping, signature-verified PayHere callbacks, least-privilege Admin auth, protection of the number-change flow against account takeover.
- **Scalability:** taxonomy and search must scale as new Categories open beyond Vehicles; Moderation throughput scales via multiple operator accounts rather than a single human (see §15).
- **Observability:** Moderation actions, payments, refunds, badge decisions, reports, and bans are auditable (who did what, when, why).
- **Accessibility:** core flows usable on low-end Android devices and small screens. `[ASSUMPTION: WCAG-AA-aligned but not formally certified for v1 — confirm.]`

## 11. Constraints & Guardrails

### 11.1 Safety & Trust
- Mandatory Seller Verification is a hard gate on listing — never bypassed.
- Every new and content-edited listing is human-moderated before public visibility.
- The Verification Badge is only granted after genuine offline vetting; the badge's credibility depends on never shortcutting that review.
- The WhatsApp wedge is *verified WhatsApp identity*, not the deep-link itself (a contact button alone is not differentiating — incumbents have one).

### 11.2 Privacy
- A Seller's WhatsApp number is revealed to Buyers only via the WhatsApp contact action and only when Contact Preference is WhatsApp; otherwise it is not exposed. `[ASSUMPTION: confirm whether the number is shown or masked behind the deep-link.]`
- Buyer identity beyond what's needed to chat is not exposed to Sellers.
- Personal data (address, phone) collected at registration is stored securely and not shown publicly.
- Chat history and deleted-account data are retained only for a defined window (Open Question #6).

### 11.3 Cost / Business
- TradeZone's revenue is limited to high-value Listing Fees and Verification Badge fees via PayHere; it takes no cut of goods.
- Free-to-list by default supports the positioning and combats cold-start (see SM-C2). Lower cost is a positioning bet, not a moat — a well-funded incumbent could match it.

## 12. Monetization
- **High-value Listing Fees:** admin-discretionary, required only on high-value Listings, collected via PayHere before publication. Most listings are free.
- **Verification Badge fee:** paid, charged via PayHere when the Admin grants a badge to a vetted large-scale seller (one-time for v1).
- **Deferred levers:** promoted/featured placements and dealer subscriptions (future).
- Pricing specifics (amounts, "high-value" threshold) are Open Question #1.

## 13. Information Architecture (high level)
- **Public/Buyer surfaces:** Home / Category landing → Category & sub-category browse → Search results (with filters + sort) → Listing detail → Contact (Chat or WhatsApp) / Report; Auth (sign in/register); My account (profile, my conversations, account deletion).
- **Seller surfaces:** Verification flow; Create/Manage Listings; My Listings (status); Badge request + payment; Conversations; Notifications.
- **Admin Panel (separate):** Moderation queue; Categories & Attributes; Badge requests; Reports; Users (suspend/ban); Fees & refunds; Notifications/audit.
- *Detailed screen design is for the UX workflow (`bmad-ux`); this is the surface inventory only.*

## 14. Platform & Internationalization
- **v1:** responsive web, optimized for Sri Lankan mobile browsers; no native apps.
- **Language at launch:** English UI.
- **Later phases:** Sinhala and Tamil UI; native iOS/Android apps; additional Categories beyond Vehicles.

## 15. Risks & Mitigations
- **Cold-start / two-sided liquidity (highest):** buyers follow listings, sellers follow buyers; a newer platform competing with free incumbents risks empty shelves, and TradeZone's own verification + moderation add supply-side friction. *Mitigation:* seed the Vehicles category with genuine sellers, keep listing free by default (fees only on high-value), keep moderation turnaround fast, and convert fraud-burned users on the trust promise. (Acknowledged and accepted in the brief; a concrete seeding plan with owner/targets is still needed.)
- **"Trust" promised but key mechanisms phased:** ratings (v1.1) and richer scam detection are deferred, so v1 trust rests on verification + moderation + report-a-listing + bans. *Mitigation:* never overstate baseline verification (WhatsApp OTP proves number control, not identity); the offline-vetted badge carries the real identity signal; ship ratings in v1.1 as planned.
- **Moderation as a bottleneck / does not scale:** human review of every listing can be slow and unscalable with a single operator. *Mitigation:* multiple operator accounts, fast-turnaround target (SM-6), Admin Panel tooling, and an independent approval audit (SM-C3) — without dropping the human gate.
- **Badge vetting cost vs scale:** offline showroom visits are high-effort. *Mitigation:* badge is paid and reserved for low-volume large sellers, so volume is low and the fee offsets cost; keep the bar high to protect credibility.
- **WhatsApp dependency:** OTP and contact rely on WhatsApp availability/policy. *Mitigation:* monitor WhatsApp Business API terms; email is a secondary channel; if an SMS fallback is ever needed for OTP, treat the positioning impact explicitly. `[ASSUMPTION: WhatsApp OTP delivery mechanism to be defined in architecture.]`
- **Email as a notification single point of failure:** v1 notifications are in-app + email only. *Mitigation:* ensure reliable transactional email; revisit WhatsApp/push notifications post-launch.
- **Unverified buyers expose sellers:** buyers are email-only, so fake/throwaway buyer accounts can spam or scam sellers. *Mitigation:* report-a-listing + bans + chat rate-limiting; consider buyer verification (Open Question #7).

## 16. Why Now
Sri Lankan online trading is large and active, but trust is deteriorating: advance-payment and fake-seller scams are common enough that the Police issue public warnings, and incumbents have not closed the gap with strong verification. At the same time, WhatsApp is effectively the national messaging layer, making WhatsApp-native verification and contact feel natural to users. The opening is a *trusted* marketplace that also fixes the universally-hated discovery experience — and doing it now, before an incumbent mandates verification, is the wedge.

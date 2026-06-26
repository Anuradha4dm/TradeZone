# TradeZone Brief — Addendum

Supporting depth for the brief. Carried forward for the PRD / architecture stages. Competitor traffic/valuation figures and gateway fees are third-party and time-sensitive — verify before relying on them.

## Competitive Landscape (Sri Lanka, 2026)

| Player | What it is | Monetization | Vehicle strength | Notable weakness |
|---|---|---|---|---|
| **ikman.lk** | Dominant general classifieds (Saltside, 2012, tri-lingual) | Freemium: free basic posting; B2B memberships, banner ads, Bump Up / Top Ad promos | Flagship category, largest dealer base | Heavy Trustpilot complaints: aggressive upsell, ads expiring, scam "member" ads |
| **Riyasewana** | #1 dedicated vehicle marketplace (2009) | Free for used/registered + parts; **Rs.650** for new/unregistered ads; Top Ad/Bump Up; prepaid "Credits" | Very strong | Pure board, disclaims all validation of seller/vehicle |
| **PatPat.lk** | Vehicle-first → lifestyle classifieds/e-commerce (2017) | Free posting + Premium upgrades + dealer pages; leasing/finance | Search by monthly installment; agent calls buyer in ~15 min | App perf, login/OTP failures, fewer filters |
| **Saleme.lk** | Smaller general classifieds | Free | Minor | Small user base/traffic |
| **Carmudi.lk** | Vehicle marketplace | Ad revenue | Declining traffic | Fading vs Riyasewana/ikman |
| **Facebook Marketplace + buy/sell groups** | Massive informal channel (~9M active SL FB users) | Free | Strong for local/low-value | No fees, **no verification, most-cited scam venue** |

## How Incumbents Handle the Things TradeZone Is Betting On

- **Seller verification:** Light everywhere. ikman = phone verify before chat + paid "Verified Seller/Member" badges. Riyasewana = SMS phone confirm only. Facebook = none. → **No incumbent mandates strong verification of every seller** (TradeZone's wedge).
- **Buyer–seller contact:** Converging on WhatsApp. **ikman already has Call + in-app Chat + a WhatsApp button on every ad.** → WhatsApp deep-link alone is table-stakes, not a differentiator.
- **Listing fees:** Standard = **free to list, pay to promote**. Mandatory list fee is contrarian (friction risk vs free rivals). Frame TradeZone's fee as bundled with verification/moderation value rather than a raw posting tax.
- **Moderation:** Exists but fast/automated (ikman pre-review + spam checks; PatPat instant; Riyasewana ~30 min). Manual approval of *every* listing is a quality lever TradeZone can own — but turnaround speed is a competitive expectation.

## Fraud (the core pain to solve)

- #1 scam: **advance-payment fraud** — fake cheap listing, "I'm overseas," demand Rs.5k–20k deposit, disappear. Police/CCID actively warning.
- Also: foreign "I paid, now ship it" email scams; fake bank-transfer screenshots; phishing impersonating ikman/Daraz "payment teams"; QR/OTP theft.
- Standard advice everywhere: inspect in person, hand-to-hand/COD, never pay in advance, video-verify. Trust is genuinely unsolved.

## Market Context

- Internet: 13.9M users, **59.7% penetration** (Oct 2025), +12% YoY (~40% still offline).
- Mobile: 29.5M subs (135% density), smartphones = 71% of devices.
- **WhatsApp: ~16.5M users** — default national comms layer; WhatsApp-first design fits. ⚠️ WhatsApp OTP-theft/impersonation scams rising — build OTP flows defensively.

## Payment Gateways (for charging sellers — not for goods)

- **PayHere** — most popular SL IPG; cards + wallets (eZ Cash/Genie/FriMi/mCash) + online banking + recurring; tiers Lite 3.90% / Plus 2.99% / Premium 2.69%. Best default.
- **Genie Business (Dialog)** — mobile/QR, low fees, PCI DSS 4.0, sandbox; good for recurring.
- **FriMi** — wallet/mobile-first, limited international.
- Others: WebXPay, Onepay, iPay, mCash; Stripe/PayPal for international cards.
- Constraints: LKR pricing; recurring billing supported (badges/subscriptions); confirm "classifieds/marketplace" merchant category is allowed; fees change often.

## Differentiation Summary

- **Strongest:** trust-as-product (mandatory verified sellers + every-listing moderation) — attacks fraud no one solves.
- **Positioning bet (matchable):** lower listing cost.
- **Fit, not moat:** WhatsApp-native onboarding/identity (button alone already exists on ikman).
- **Uncontested buyer-side ideas:** ratings/reviews, scam-pattern warnings, "never pay in advance" nudges, in-app reporting.

_Sources: DataReportal Digital 2026 Sri Lanka; TRCSL Q4 2025 / Apr 2026; ikman blog & Trustpilot; Riyasewana terms; PatPat about/LMD; Sri Lanka Police / Adaderana scam advisories; PayHere/Genie/FriMi pricing pages. Figures directional; verify before commitment._

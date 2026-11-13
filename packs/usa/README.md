# Market Pack: USA

For: `{{client_name}}` (market = US). Card payments, email/SMS, multi-channel ads.
Nothing here goes live without the owner's approval (see `docs/guardrails.md`).
App prices, plans and features are not listed on purpose: **verify at onboarding**.

## 1. Stack

| Area | Choice | Notes |
|---|---|---|
| Store | Shopify | Client owns the store and domain. |
| Payments | Shopify Payments + Shop Pay | Eligibility for the client's business and products: verify at onboarding. |
| Email / SMS | Klaviyo (native flows) | Five flows in section 2. SMS only with explicit opt-in. |
| Support | Gorgias AI Agent | Order status and returns; everything else escalates to humans (section 3). |
| Shipping | Shopify Shipping or a 3PL | Pick one per client; record it in the client profile. |
| Ads | Meta, Google Shopping, TikTok | Hard spend limits set inside each platform, not only in prompts. |
| AI shopping | Shopify Agentic Storefronts (ChatGPT and Copilot, US buyers) | Availability and setup steps: verify at onboarding. Readiness checklist in section 4. |
| Brain | Airtable (Brand Brain) + Make scenarios 1-2 | Scenarios 3-4 are Pakistan-only. Built inactive; activated after approval. |

## 2. Klaviyo flows checklist

Message counts are starter defaults, editable per client. Build every flow in draft/manual mode; turn live only after owner approval. Copy skeletons: `email-sms-templates.md`.

| Done | Flow | Trigger | Messages (starter) | Goal |
|---|---|---|---|---|
| [ ] | Welcome | Subscribes to the email list (signup form or checkout opt-in) | 3 emails | Introduce the brand, set expectations, first purchase. |
| [ ] | Abandoned cart | Starts checkout, no order placed | 3 emails (+1 SMS if opted in) | Recover the checkout. |
| [ ] | Browse abandonment | Views a product, no cart and no order | 1-2 emails | Bring the shopper back to the product. |
| [ ] | Post-purchase | Order placed / fulfilled | 3 emails | Thank you, how to use the product, ask for a real review, second order. |
| [ ] | Win-back | No order for a set number of days (set per client from the reorder cycle) | 2 emails | Re-engage or let the profile go quiet. |

Rules for all flows
- [ ] SMS only to profiles with explicit SMS consent. Email consent does not cover SMS.
- [ ] Every email has an unsubscribe link and the sender's physical mailing address.
- [ ] Every SMS names the brand and gives opt-out wording (Reply STOP).
- [ ] Exclude recent purchasers from cart and browse flows.
- [ ] Any discount in a flow comes from Airtable `KPI Targets & Caps` and is approved by the client.
- [ ] Product facts come only from the Brand Brain. No health, safety or "best / #1" claims.
- [ ] Review requests go to real buyers only, after delivery. No incentive tied to a positive review.
- [ ] Sending domain set up and authenticated before the first send: verify at onboarding.

## 3. Gorgias: AI Agent vs humans

| AI Agent handles | Escalate to a human |
|---|---|
| Order status and tracking ("where is my order") | Refund above the approval limit (default US $50, in `KPI Targets & Caps`) |
| Return and exchange requests inside the written policy | Any request outside the written policy |
| Policy questions answered from Airtable `Policies & SOPs` | Chargebacks, payment disputes, suspected fraud |
| Product questions answered from the Brand Brain | Damaged, wrong or missing items |
| | Health, safety, allergy or legal questions |
| | Angry or repeat-contact customers; anyone asking for a person |
| | Address change after fulfilment; cancel after shipping |
| | Wholesale, press, influencer and partnership messages |

Setup checklist
- [ ] Load policies and FAQs from the Brand Brain into Gorgias. One source of truth: update Airtable first.
- [ ] Start in draft or limited mode (autonomy level 2) and review replies for about 2 weeks before widening.
- [ ] Set the handover rule and the human team's hours. US daytime is night in Pakistan: the client's team owns urgent tickets.
- [ ] The AI Agent never invents a policy, a delivery date or a product claim. If the answer is not in the Brand Brain, it escalates.
- [ ] Exact AI Agent features and channel coverage: verify at onboarding.

## 4. AI shopping readiness checklist

For Shopify Agentic Storefronts (ChatGPT and Copilot). Clean data matters more than copy.

Product data
- [ ] Every product has a clear title, plain description, price, variants, images and stock status.
- [ ] SKU and product identifiers (GTIN/barcode where the product has one) filled in.
- [ ] Product category, type and key attributes (size, material, color, dimensions, weight) filled in.
- [ ] Descriptions state facts from the Brand Brain. No health, safety or "best / #1" claims.
- [ ] Prices and stock in Shopify match what is true today.
- [ ] Reviews shown are from real customers only.

Policies
- [ ] Shipping, returns/refund, privacy and terms pages published and current.
- [ ] Shipping rates and delivery times set in Shopify, not only written in a page.
- [ ] Policies in Shopify match Airtable `Policies & SOPs`.
- [ ] Contact details visible on the store.

Checkout
- [ ] Guest checkout on (no forced account creation).
- [ ] Shopify Payments and Shop Pay active.
- [ ] Sales tax set up in Shopify.
- [ ] Test order placed and refunded cleanly.

Program
- [ ] Agentic Storefronts eligibility, channel settings and reporting: verify at onboarding.

## 5. Compliance checklist

Not legal advice; client confirms with counsel.

- [ ] **FTC fake-review rule:** reviews and testimonials only from real customers. No AI-generated, bought or fake reviews. No review suppression. No incentive tied to a positive review. AI avatars never pose as real buyers.
- [ ] **Endorsements:** influencers and affiliates disclose the relationship clearly.
- [ ] **SMS consent:** explicit opt-in before any marketing text, collected separately from email consent, with clear disclosure at signup. Honor STOP at once. Keep consent records.
- [ ] **SMS timing:** send in the recipient's local daytime. Exact quiet hours: client confirms with counsel.
- [ ] **Email:** working unsubscribe link in every marketing email, opt-outs honored promptly, honest subject lines and sender name, physical mailing address in the footer.
- [ ] **Sales tax:** collected through Shopify's tax settings. Where the client must register and collect: client confirms with their accountant.
- [ ] **Privacy:** privacy policy published; cookie/consent settings match the states the client sells into. Client confirms with counsel.
- [ ] **Claims:** no health, safety or "best / #1" claims in ads, emails, product pages or support replies.
- [ ] **Ad platform policies:** Meta, Google and TikTok rules followed; official APIs and connectors only.

## 6. Time-zone rule

US daytime is night in Pakistan.

| Situation | Who acts |
|---|---|
| Routine action inside the limits in `KPI Targets & Caps` | Runs automatically, logged in `Agent Action Log`. |
| Action that needs approval, not urgent | Goes to `Approvals Queue`; the owner handles it in Pakistan working hours. |
| Urgent approval during US hours (spend spike, site down, payment failure, viral complaint) | Goes to the **client's team**. Named approver and backup in the client profile. |
| Anything that spends money above the cap | Waits for approval. It never runs automatically. |

- [ ] Daily brief at 08:00 client time (US), by email.
- [ ] Client names an approver and a backup with phone and email in `clients/<client-name>/client-profile.md`.
- [ ] Hard spend limits inside Meta, Google and TikTok are the safety net when nobody is awake.

## 7. KPIs

| KPI | Formula | Notes |
|---|---|---|
| MER | Total revenue / total marketing spend | All channels together, same period. Blended view. |
| ROAS | Revenue attributed to a channel or campaign / ad spend on that channel or campaign | Per platform. Attribution windows differ by platform; note the window used. |
| Cost per customer | Total marketing spend / new customers acquired | New customers only, same period. |
| AOV | Total revenue / number of orders | State whether tax and shipping are included; keep it consistent. |
| Repeat rate | Customers with 2 or more orders / total customers x 100 | Fix the period (for example trailing 90 or 365 days). |
| Chargeback rate | Chargebacks / total card orders x 100 | Same period. Any rise is flagged in the daily brief. |

Targets and hard limits are set per client in Airtable `KPI Targets & Caps`. Do not copy targets from another client.

## 8. Install order for a new US client

Start the slow items on day 1; they take days to weeks.

- [ ] 1. Day 1, in parallel: Meta Business Manager and verification, Google Ads + Merchant Center, TikTok Ads (the organic posting API audit takes weeks), Klaviyo, Gorgias, Make Core account (client-owned).
- [ ] 2. Shopify store and domain ready. Activate Shopify Payments and Shop Pay. Guest checkout on.
- [ ] 3. Set up sales tax in Shopify. Set up Shopify Shipping or connect the 3PL.
- [ ] 4. Publish shipping, returns, privacy and terms pages.
- [ ] 5. Fill the Brand Brain: Brand, Products, Policies, KPI caps (ad spend cap, 20% max daily budget change, 10% price-change approval, US $50 refund approval).
- [ ] 6. Klaviyo: connect Shopify, authenticate the sending domain, add signup forms with separate email and SMS consent, build the five flows in draft.
- [ ] 7. Gorgias: connect Shopify, load policies and FAQs, set escalation rules, start the AI Agent in draft or limited mode.
- [ ] 8. Tracking: Meta Pixel + Conversions API, Google tag + Merchant Center product feed, TikTok Pixel.
- [ ] 9. Set hard spend limits inside Meta, Google and TikTok.
- [ ] 10. Run the AI shopping readiness checklist (section 4).
- [ ] 11. Run the compliance checklist (section 5); client confirms with counsel.
- [ ] 12. Import Make blueprints 1-2 into the client's Make account. Keep them **inactive**.
- [ ] 13. Run 5-10 test orders end to end: card and Shop Pay, guest checkout, abandoned cart, refund, a return request through Gorgias, one email and one SMS per flow to internal opted-in contacts. Check `Daily Briefs` and `Agent Action Log`.
- [ ] 14. Fix what failed, re-test, then ask the owner for approval to activate flows, scenarios and the AI Agent.
- [ ] 15. Turn on the daily brief. Agents start at level 2 (Draft). New campaigns and public posts need approval.

Related files: `email-sms-templates.md`, `make/README.md` (scenarios 1 and 2), `airtable/brand-brain-schema.md`, `docs/client-onboarding-checklist.md`.

# Client onboarding checklist

Client: `{{client_name}}` · Market: `{{market}}` (PK / US) · Start date: `{{start_date}}`

The template deploys in 30-60 minutes per client **once the accounts below are ready**. The accounts are the slow part. Start section 1 on day 1, all items in parallel.

## 1. Day-1 dependencies (start immediately)

"Expected wait" shows days or weeks only where we know the item is slow. "Verify" means check the current timing with the provider when you apply; do not promise the client a date.

### Pakistan

| Done | Item | Who does it | Expected wait |
|---|---|---|---|
| [ ] | Shopify store + domain | Client creates and owns; agency builds the store | Verify |
| [ ] | Meta Business Manager | Client creates and owns; agency added as partner | Verify |
| [ ] | Meta Business verification | Client (needs business documents) | Days to weeks |
| [ ] | Meta ad account | Client owns; agency added as partner | Verify |
| [ ] | Meta Pixel + Conversions API | Agency sets up inside the client's account | Verify |
| [ ] | WhatsApp Business API number | Client provides the number and owns the account; agency sets up | Days to weeks |
| [ ] | Courier accounts (e.g. PostEx, TCS, Trax, Leopards, BlueEx) | Client signs up | Days to weeks |
| [ ] | Payment aggregator sign-up for prepaid (e.g. bSecure) | Client signs up | Days to weeks |
| [ ] | Make account, Core plan | Client creates; invites agency owner as admin | Verify |

Note: Shopify Payments is not available in Pakistan, so prepaid runs through the local aggregator.

### USA

| Done | Item | Who does it | Expected wait |
|---|---|---|---|
| [ ] | Shopify store + Shopify Payments (with Shop Pay) | Client creates and owns; agency builds the store | Verify |
| [ ] | Meta Business Manager | Client creates and owns; agency added as partner | Verify |
| [ ] | Meta Business verification | Client (needs business documents) | Days to weeks |
| [ ] | Meta ad account | Client owns; agency added as partner | Verify |
| [ ] | Meta Pixel + Conversions API | Agency sets up inside the client's account | Verify |
| [ ] | Google Ads access | Client owns; agency invited | Days to weeks |
| [ ] | Google Merchant Center | Client owns; agency invited | Verify |
| [ ] | TikTok Ads account | Client owns; agency invited | Verify |
| [ ] | TikTok organic posting API audit | Agency applies with the client's account | Weeks |
| [ ] | Klaviyo | Client creates; agency invited | Verify |
| [ ] | Gorgias | Client creates; agency invited | Verify |
| [ ] | Make account, Core plan | Client creates; invites agency owner as admin | Verify |

## 2. Access checklist

- [ ] Every account is created and owned by the client (client's email, client's billing).
- [ ] Agency is invited as admin / partner / collaborator on each account. No shared logins.
- [ ] No passwords, API keys or tokens sent by chat or email, or stored in any file.
- [ ] Credentials are entered only inside Make / Airtable connections in the client's accounts.
- [ ] Two-factor authentication stays on the client's devices.
- [ ] Access status for each account is recorded in `clients/<client-name>/client-profile.md`.
- [ ] Client knows how to remove the agency's access at any time.

## 3. Deployment steps

### Step 1: Client folder
- [ ] Copy `clients/_template` to `clients/<client-name>`.
- [ ] Fill in `client-profile.md` (business basics, market, voice, accounts, caps, approvers).
- [ ] Confirm no passwords or API keys were written in the profile.

### Step 2: Brand Brain (Airtable)
- [ ] Duplicate the base "Brand Brain - MASTER" into the client's Airtable workspace.
- [ ] Fill `Brand` (name, market, voice, audience, USP, banned words, logo and color links).
- [ ] Fill `Products` (SKU, title, description, price, cost, stock, allowed claims, FAQs).
- [ ] Fill `Policies & SOPs` (shipping, returns, refunds, support hours).
- [ ] Fill `KPI Targets & Caps` (daily ad spend cap, max budget change per day, price-change threshold, refund threshold).
- [ ] Check that the other tables are empty of dummy data.

### Step 3: Make
- [ ] Client creates their own Make account on the **Core plan** (the free plan allows only 2 active scenarios).
- [ ] Client invites the agency owner as admin.
- [ ] Import the blueprints from `make/blueprints/` (see `make/README.md`).
- [ ] Connect the client's accounts (Shopify, Airtable, Meta, and WhatsApp for PK).
- [ ] Set the client's time zone and the 08:00 daily brief time.
- [ ] Test each scenario once on test data; check a row lands in `Agent Action Log`.
- [ ] Keep every scenario **inactive** until approval.
- [ ] Activate after approval (agency owner, following the client's sign-off in section 4).

### Step 4: Market-pack apps and test orders
- [ ] Install the market-pack apps (`packs/pakistan/README.md` or `packs/usa/README.md`).
- [ ] PK: COD confirmation (app, or Make + WhatsApp Business Cloud), courier app, prepaid aggregator; WhatsApp templates approved.
- [ ] US: Shopify Payments + Shop Pay, Klaviyo flows, Gorgias, shipping (Shopify Shipping or 3PL); SMS only with explicit opt-in.
- [ ] Set hard spending limits inside each ad platform in use (Meta; US also Google and TikTok).
- [ ] Run 5-10 test orders end to end (order -> confirmation -> shipping -> status -> brief).
- [ ] PK: test confirm, cancel, no-reply reminder, auto-cancel and a refused parcel.
- [ ] US: test card payment, order emails, a support ticket and a return.
- [ ] Fix anything that failed; log open items in the client profile notes.

### Step 5: Daily brief and autonomy
- [ ] Turn on the daily brief.
- [ ] Confirm the first brief reached the owner and the client on the agreed channel.
- [ ] Set agents to level 2 (Draft) and record the levels in the client profile.
- [ ] Book the 2-week review to decide which agents move up (`docs/architecture.md`, section 3).

## 4. Go-live sign-off

By signing, the client confirms that test orders were reviewed, spending limits and approval thresholds are correct, and the scenarios may be activated.

| Field | Value |
|---|---|
| Client name | `{{client_name}}` |
| Market | `{{market}}` |
| Go-live date | `{{go_live_date}}` |
| Approver (client) | `{{client_approver_name}}` |
| Approver (agency) | `{{agency_owner_name}}` |
| Scenarios approved for activation | `{{scenario_list}}` |
| Open items accepted at go-live | `{{open_items}}` |
| Signature / written confirmation (link) | `{{signoff_link}}` |

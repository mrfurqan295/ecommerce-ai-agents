# Market Pack: Pakistan

For: `{{client_name}}` (market = PK). COD-first, WhatsApp-first, local couriers.
Nothing here goes live without the owner's approval (see `docs/guardrails.md`).
App names below are candidates to evaluate. Prices, plans and features are not listed on purpose: **verify at onboarding**.

## 1. Stack

| Area | Choice | Notes |
|---|---|---|
| Store | Shopify | Client owns the store and domain. |
| Payments: COD | Shopify manual payment method "Cash on Delivery" | Default method for most orders. |
| Payments: prepaid | Local aggregator, e.g. bSecure (JazzCash, EasyPaisa, cards) | Shopify Payments is not available in Pakistan. Aggregator, methods and fees: verify at onboarding. |
| Prepaid discount | Small discount for paying online | Amount set by the client in Airtable `KPI Targets & Caps`; needs approval like any price change. |
| COD confirmation | WhatsApp app (evaluate WASP, COD Confirm, Level) **or** Make + WhatsApp Business Cloud (scenario 3) | Use one, not both. Scenario 3 runs only if no COD app is installed. |
| Couriers | Courier app such as Courierify (PostEx, TCS, Trax, Leopards, BlueEx) | Client holds the courier accounts. Coverage per courier: verify at onboarding. |
| Ads | Meta; TikTok if it fits the product and audience | Hard spend limits set inside the ad platforms, not only in prompts. |
| Support | WhatsApp (COD app inbox or Make + WhatsApp Business Cloud) with AI replies | Opt-in customers and approved templates only. |
| Brain | Airtable (Brand Brain) + Make scenarios 1-4 | Built inactive; activated after approval. |

## 2. App evaluation checklist

Answer every question from the app's own listing, docs or support. Do not guess. Write the answer and the date checked in the client profile.

### COD confirmation app (WASP / COD Confirm / Level / other)

- [ ] Does it use the official WhatsApp Business API (Cloud API or an approved provider)? No unofficial or QR-scan automation.
- [ ] Does the client keep ownership of the WhatsApp number and the Meta Business account?
- [ ] Does it send Confirm / Cancel quick-reply buttons with approved templates?
- [ ] Does it support Urdu, Roman Urdu and English templates?
- [ ] Can it send a reminder at a set delay (default 4 h) and auto-cancel at a set delay (default 24 h)? Are both editable?
- [ ] Does it write Shopify order tags, and can the tag names be set to ours (section 5)?
- [ ] Can it cancel the Shopify order automatically, or only tag it?
- [ ] Does it hold fulfilment until the order is confirmed?
- [ ] Does it track repeat refusers or block phone numbers? If yes, can we still keep Airtable `COD Risk` as the source of truth?
- [ ] Does it have a shared inbox for replies, and can AI replies or a webhook connect to it?
- [ ] Does it expose webhooks or an API that Make can read (confirmed, cancelled, no reply)?
- [ ] How does it handle customers who reply with free text instead of tapping a button?
- [ ] Pricing model (per message, per order, monthly) and who pays Meta conversation charges: verify at onboarding.
- [ ] Support channel and response time in Pakistan hours: verify at onboarding.
- [ ] Data: where is customer data stored, and can it be exported or deleted on request?

### Courier app (Courierify / other)

- [ ] Which couriers does it support today (PostEx, TCS, Trax, Leopards, BlueEx)? Verify at onboarding.
- [ ] Does it use the client's own courier accounts and rates?
- [ ] Can booking be limited to orders tagged `cod-confirmed` or `prepaid` only?
- [ ] Can it pick a courier by city or rule (for example the courier with the lowest RTO in that city)?
- [ ] Does it write the tracking number and courier name back to the Shopify order?
- [ ] Does it sync courier status (dispatched, out for delivery, delivered, returned) back to Shopify, and how often?
- [ ] Does it add a tag or status we can map to `courier-booked` and `rto`?
- [ ] Does it expose status by webhook or API so Make scenario 4 can read it?
- [ ] Does it print load sheets and airway bills in bulk?
- [ ] Does it report COD remittance (cash collected vs cash paid out by the courier)?
- [ ] How are return (RTO) charges shown per parcel?
- [ ] Pricing model and limits: verify at onboarding.

Decision rule: pick the app that answers "yes" to tags, hold-until-confirmed and status sync. If no COD app passes, use Make scenario 3 with WhatsApp Business Cloud.

## 3. Order flow (COD)

| Step | Event | Action | Shopify tag | Logged in |
|---|---|---|---|---|
| 1 | New COD order | Check phone in Airtable `COD Risk`. If flag = Block, hold for manual review or offer prepaid only. | `cod-pending` | `Agent Action Log` |
| 2 | Order created | Send WhatsApp template `order_confirmation` with Confirm / Cancel buttons, in the customer's language. | `cod-pending` | `Agent Action Log` |
| 3a | Customer taps Confirm | Send `order_confirmed_thanks`. | replace with `cod-confirmed` | `Agent Action Log` |
| 3b | Customer taps Cancel | Cancel the order in Shopify. | replace with `cod-cancelled` | `Agent Action Log` |
| 4 | No reply after 4 h (editable) | Send `confirmation_reminder`. | `cod-pending` | `Agent Action Log` |
| 5 | No reply after 24 h (editable) | Cancel the order, send `order_cancelled_no_reply`. | replace with `cod-no-reply` | `Agent Action Log` |
| 6 | Order is `cod-confirmed` | Book the courier. Never before confirmation. Send `order_dispatched` with courier and tracking. | add `courier-booked` | `Agent Action Log` |
| 7 | Courier status: out for delivery | Send `out_for_delivery` (keep cash ready). | no change | `Agent Action Log` |
| 8 | Courier status: failed attempt | Send `delivery_failed_reattempt`. | no change | `Agent Action Log` |
| 9a | Delivered | Update `COD Risk`: orders +1. | no change | `COD Risk` |
| 9b | Refused or returned | Update `COD Risk`: orders +1, refused count +1, re-check flag. | add `rto` | `COD Risk`, `Agent Action Log` |

Notes
- Prepaid orders skip steps 2-5: tag `prepaid`, then go straight to courier booking.
- The 4 h and 24 h timers start at order creation and live in Airtable `KPI Targets & Caps` so the client can edit them.
- If a COD app is installed, it runs steps 2-5 and Make only reads the result. If not, Make scenario 3 runs them.
- Send reminders in daytime Pakistan hours only (suggested 09:00-21:00, editable). An order placed at night gets its reminder in the morning.
- A free-text reply (not a button tap) goes to the support inbox; the order stays `cod-pending` until a human or the AI reply resolves it.

## 4. RTO rules

- [ ] Book the courier only after the order is `cod-confirmed` or `prepaid`.
- [ ] Auto-cancel unconfirmed orders at 24 h (editable).
- [ ] Flag repeat refusers in Airtable `COD Risk` (key = phone number):

| Refused count | Flag | What happens on the next order |
|---|---|---|
| 0 | OK | Normal flow. |
| 1 | Watch | Normal flow, plus a note on the order; a human may call to confirm. |
| 2 or more | Block | No COD. Offer prepaid only, or hold for manual review. |

  Thresholds are suggestions and editable. A human can reset a flag (for example after a courier mistake).
- [ ] Track RTO % every week by **city**, **courier** and **product** (Make scenario 4 -> Airtable -> daily brief).
- [ ] Act on the weekly numbers, with approval: switch courier in a weak city, make a high-RTO city or product prepaid-only, fix the listing if a product is often refused.
- [ ] Never share the `COD Risk` list outside the client's own accounts.

## 5. Shopify order tags

| Tag | Meaning | Set when | Set by |
|---|---|---|---|
| `cod-pending` | COD order waiting for the customer's reply | Order created | COD app or scenario 3 |
| `cod-confirmed` | Customer confirmed | Confirm tapped | COD app or scenario 3 |
| `cod-cancelled` | Customer cancelled | Cancel tapped | COD app or scenario 3 |
| `cod-no-reply` | Auto-cancelled, no reply in 24 h | Timer ends | COD app or scenario 3 |
| `courier-booked` | Parcel booked with a courier | After confirmation or prepaid | Courier app |
| `rto` | Parcel refused or returned to origin | Courier status = returned | Courier app or scenario 4 |
| `prepaid` | Paid online, no confirmation needed | Order created | Shopify Flow or scenario 3 |

Rules: an order carries only one `cod-*` tag at a time. Keep the exact spelling; the Make scenarios and reports filter on these tags.

## 6. Language rule

- Reply in the customer's language: **Urdu** (Urdu script), **Roman Urdu** or **English**.
- First message: use the store's default language (set in Airtable `Brand`). After the customer writes back, match their language and keep it for that customer.
- Mixed message (Roman Urdu + English words): reply in Roman Urdu.
- Templates for all three languages: `whatsapp-templates.md`.
- Product facts come only from the Brand Brain. No health, safety or "best / #1" claims in any language.

## 7. KPIs

| KPI | Formula | Notes |
|---|---|---|
| Confirmation rate | Confirmed COD orders / total COD orders placed x 100 | Use orders created in the period. Cancelled and no-reply both count as not confirmed. |
| Delivered % | Delivered orders / dispatched orders x 100 | Use orders dispatched in the period with a final status. Parcels still in transit are excluded. |
| RTO % | Refused or returned orders / dispatched orders x 100 | Same base as Delivered %. Report by city, courier and product. |
| Cost per delivered order | Total ad spend / delivered orders | Same period. Optional fuller version: (ad spend + courier charges on returned parcels) / delivered orders. |

Targets and hard limits are set per client in Airtable `KPI Targets & Caps`. Do not copy targets from another client.

## 8. Install order for a new PK client

Start the slow items on day 1; they take days to weeks.

- [ ] 1. Day 1, in parallel: Meta Business Manager and verification, WhatsApp Business API number, courier accounts, payment aggregator sign-up, Make Core account (client-owned).
- [ ] 2. Shopify store and domain ready. Turn on the manual "Cash on Delivery" payment method.
- [ ] 3. Fill the Brand Brain: Brand, Products, Policies, KPI caps, timers (4 h / 24 h), prepaid discount.
- [ ] 4. Choose the COD confirmation app with the checklist in section 2. **Install it first**, before the courier app, so no order can be booked unconfirmed.
- [ ] 5. Submit the WhatsApp templates (`whatsapp-templates.md`) for Meta approval, one language per submission.
- [ ] 6. Set the tag names in the COD app to match section 5.
- [ ] 7. Install the courier app. Connect the client's courier accounts. Limit booking to `cod-confirmed` and `prepaid`.
- [ ] 8. Connect the payment aggregator once approved. Add the prepaid discount.
- [ ] 9. Meta Pixel + Conversions API. Set hard spend limits inside Meta (and TikTok if used).
- [ ] 10. Import Make blueprints 1-4 into the client's Make account. Keep them **inactive**. Skip scenario 3 if a COD app is installed.
- [ ] 11. Run **5-10 test orders end to end**: confirm, cancel, no reply (reminder + auto-cancel), prepaid, a repeat-refuser phone, and at least one real booking per courier. Check tags, messages in all three languages, `COD Risk` and `Agent Action Log`.
- [ ] 12. Fix what failed, re-test, then ask the owner for approval to activate.
- [ ] 13. Turn on the daily brief. Agents start at level 2 (Draft).

Related files: `whatsapp-templates.md`, `make/README.md` (scenarios 3 and 4), `airtable/brand-brain-schema.md` (`COD Risk`), `docs/client-onboarding-checklist.md`.

# Agent prompt library

One system prompt per agent for the e-commerce AI agents master template. All prompts are grounded in the Airtable base "Brand Brain - MASTER" and follow the guardrails in `docs/guardrails.md`.

## Index
| File | Agent (value for the Agent field) | Starting autonomy | Ceiling | Market |
|---|---|---|---|---|
| `orchestrator.md` | Orchestrator, Finance & KPIs | 2 Draft | 3 (does not spend) | PK + US |
| `catalog.md` | Catalog & Pricing | 2 Draft | 3 (prices are money) | PK + US |
| `seo.md` | SEO & AI Search | 2 Draft | 3 in v1 | PK + US (AI shopping part: US) |
| `creative.md` | Creative Studio | 2 Draft | 3 in v1, never publishes | PK + US |
| `paid-ads.md` | Paid Ads | 1 Watch | 3 (spends money) | PK: Meta (+ TikTok if it fits). US: Meta + Google + TikTok |
| `social.md` | Social | 2 Draft | 3 in v1 | PK + US |
| `email-sms.md` | Email & SMS | 2 Draft | 3 (SMS costs money) | US only - not used for PK in v1 |
| `support.md` | Support | 2 Draft | 3 (refunds are money) | PK: WhatsApp. US: Gorgias AI Agent |
| `orders-shipping.md` | Orders & Shipping | 2 Draft | 3 (courier and labels are money) | PK: COD app + courier app. US: Shopify Shipping or 3PL |
| `product-research.md` | Product Research | 1 Watch | 3 for anything that spends | PK + US |

Autonomy levels: 1 Watch -> 2 Draft -> 3 Act within limits -> 4 Autonomous. An agent moves up only when the owner says so, after about 2 weeks of clean work. Anything that spends money stops at 3.

## How to use a prompt
1. Open the agent file and copy the whole file.
2. Paste it as the **system prompt** (AI assistant project instructions, the AI step of a Make scenario, or the Gorgias AI Agent guidance for the US part of `support.md`).
3. Fill the placeholders:
   - `{{client_name}}` = `Brand`.Brand Name
   - `{{market}}` = `Brand`.Market (PK or US)
   - `{{store_url}}` = `Brand`.Store URL
   - Message placeholders such as `{{customer_name}}`, `{{order_number}}`, `{{tracking_link}}` are filled at run time by the app or scenario.
4. Delete the market section that does not apply (keep "Pakistan variant" for PK clients, "USA variant" for US clients). Keep everything else.
5. Give the agent read access to the client's copy of the Brand Brain. Do not paste credentials into the prompt.
6. Run it once on dummy data and check the output against section 9 of the file before real use.
7. Keep the master files unchanged; save the filled copy in `clients/<client-name>/`.

## Sections in every file (same order)
1. Role
2. Autonomy level
3. Read first (Brand Brain tables and fields)
4. Tasks (checklist)
5. Pakistan variant
6. USA variant
7. Needs approval (triggers -> `Approvals Queue`)
8. Never do
9. Output format
10. Log line (`Agent Action Log`)

## Shared rules (already inside every prompt)
- Product facts come only from the Brand Brain. No health, safety or "best / #1" claims.
- No fake reviews or testimonials. AI avatars never pose as real buyers.
- Nothing is activated, published, sent to customers or changed in ad spend without approval.
- WhatsApp: opt-in customers and approved templates only. Official APIs and connectors only.
- Every action is written to `Agent Action Log`.

## Seed approval thresholds
Stored in `KPI Targets & Caps` and editable per client. The prompts read the live value and fall back to these seeds:
| Trigger | Seed | Action Type in `Approvals Queue` |
|---|---|---|
| Budget change per day | more than 20% | Budget change |
| Daily ad spend | above the cap stored in `KPI Targets & Caps` | Budget change |
| New campaign | always | New campaign |
| Price change | over 10% | Price change |
| Refund | above US $50 / Rs 3,000 | Refund |
| New product | always | New product |
| Public post | always in the first month | Public post |

## Approvals Queue row (used by every agent)
```
Request: <one line, what and why>
Agent: <agent name from the index>
Action Type: Budget change / New campaign / Price change / Refund / New product / Public post / Other
Impact Amount: <number in Brand.Currency>
Details: <evidence, rule used, risk>
Action Payload: <system, object ID, field, old value, new value>
Status: Pending
Requested At: <ISO timestamp, Brand.Timezone>
```
Approver, Decided At and Executed are filled by the approver and the Make "Approval handler" scenario, never by the agent.

## Agent Action Log row (used by every agent)
```
Action | Time | Agent | System | Before | After | Result (Success/Failed/Skipped) | Notes
```

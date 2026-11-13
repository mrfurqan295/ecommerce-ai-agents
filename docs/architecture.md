# Architecture (v1)

Build path **D + B**: Shopify + ready-made apps do anything an app already does; Make + Airtable are the 24/7 brain and glue. An AI assistant with connectors is the agency owner's operator tool, not the client's runtime.

The master template lives in the agency's accounts. Each client gets a copy inside accounts the **client** owns.

## 1. Layers

```
Owner / client  (approvals + strategy)
        |
Orchestrator (daily brief, task routing) -- Brand Brain (Airtable) -- Guardrails
        |
Specialist agents
  Product:    research, catalog & pricing
  Store:      Shopify & CRO, SEO & AI search
  Growth:     creative, paid ads, social, email & SMS
  Operations: orders & shipping, support, finance & KPIs
        |
Tools: Shopify, Meta, Google, TikTok, Klaviyo, WhatsApp, couriers, Canva
```

**Owner / client.** People set strategy and approve anything that matters: activating scenarios, new campaigns, budgets above cap, price changes over 10%, refunds above the limit, new products and public posts in the first month. Approvers and their channels are named in `clients/<client-name>/client-profile.md`.

**Orchestrator, Brand Brain, Guardrails.** The orchestrator is a set of Make scenarios: it builds the daily brief and routes requests through the `Approvals Queue`. The Brand Brain is the Airtable base "Brand Brain - MASTER" (10 tables: brand, products, policies, caps, approvals, action log, briefs, content calendar, ad experiments, COD risk). It is the only source of product facts. Guardrails (`docs/guardrails.md`) sit beside both: caps in `KPI Targets & Caps`, hard spending limits inside the ad platforms, and every action written to `Agent Action Log`.

**Specialist agents.** Each agent is a prompt in `prompts/` plus the tool it works through (a Shopify app, a Make scenario, or the AI assistant with a connector). Agents are grouped as Product, Store, Growth and Operations. Each has an autonomy level (section 3) and reads the Brand Brain before it writes anything.

**Tools.** The systems where work actually happens: Shopify, Meta, Google, TikTok, Klaviyo, WhatsApp, couriers, Canva. Official APIs and connectors only; no browser bots on ad or social accounts. Credentials live only in Make/Airtable connections inside the client's own accounts.

## 2. Agents in v1

| Agent | v1 implementation | Market | Starting level | Ceiling |
|---|---|---|---|---|
| Orchestrator + finance & KPIs | Make daily brief scenario + AI step + Airtable `Daily Briefs` | Both | 1 Watch (reads and reports only) | 4 |
| Catalog & pricing | AI assistant + Shopify connector, `prompts/catalog.md` | Both | 2 Draft | 4; price changes over 10% always need approval |
| SEO & AI search | `prompts/seo.md`; US: product data for ChatGPT/Copilot (Shopify Agentic Storefronts) | Both | 2 Draft | 4 |
| Creative studio | AI assistant + Canva, `prompts/creative.md` | Both | 2 Draft | 4 |
| Paid ads | Meta official connector (reports; changes only with approval); caps in Airtable | Both; US adds Google + TikTok | 1 Watch | 3 (spends money) |
| Social | Airtable `Content Calendar` -> Canva -> Meta Business Suite scheduling | Both | 2 Draft | 4; public posts need approval in the first month |
| Email & SMS | Klaviyo native flows | USA | 2 Draft | 4 |
| Support | PK: WhatsApp (COD app or Make + WhatsApp Business Cloud) with AI replies. US: Gorgias AI Agent | Split | 2 Draft | 3 (refunds) |
| Orders & shipping | PK: COD confirmation app + courier app. US: Shopify Shipping or 3PL | Split | 2 Draft | 3 (courier bookings, refunds) |
| Product research | AI assistant on demand, weekly (scheduling is in the backlog) | Both | 1 Watch | 4 |

Notes:
- Default at client go-live is level 2 (Draft). The two reporting-only agents and paid ads start at 1 because v1 gives them read/report access only.
- Store build and CRO work on Shopify is done by the agency owner using the AI assistant + Shopify connector (operator tool), not by a runtime agent.
- Starting levels per client are recorded in the client profile and can be set lower, never higher.

## 3. Autonomy levels

| Level | Name | What the agent may do |
|---|---|---|
| 1 | Watch | Read data and report. Changes nothing. |
| 2 | Draft | Prepare work (copy, replies, listings, proposed changes). A human reviews and applies or sends it. |
| 3 | Act within limits | Act on its own inside `KPI Targets & Caps`. Anything outside the limits goes to `Approvals Queue`. |
| 4 | Autonomous | Act without per-action approval. Still logged. Never for agents that spend money. |

How an agent moves up:
- [ ] About 2 weeks of clean work at the current level (no guardrail breach, no reverted action, drafts approved with few edits).
- [ ] Agency owner reviews the `Agent Action Log` for that agent and signs off.
- [ ] New level recorded in the client profile and logged in `Agent Action Log`.
- One level at a time. Any incident moves the agent down one level (see `docs/guardrails.md`).
- **Anything that spends money stops at level 3.**

## 4. Data flow: the four Make scenarios

All scenarios are built **inactive** and stay inactive until a client's accounts are connected, tested and approved. Per guardrail, every scenario run that takes an action writes a row to `Agent Action Log`. If a blueprint in `make/blueprints/` differs from this page, the blueprint is the source of truth.

### Scenario 1: Daily brief (both markets)
| | |
|---|---|
| Trigger | Schedule, 08:00 client time |
| Steps | 1. Get Shopify orders for yesterday. 2. Get Meta ad insights for yesterday. 3. AI step writes the summary (PK: confirmed %, delivered %, RTO %; US: cost per customer, repeat rate, chargebacks). 4. Create the brief record. 5. Send to owner and client: email (US) or WhatsApp/email (PK). |
| Tables written | `Daily Briefs`, `Agent Action Log` |

### Scenario 2: Approval handler (both markets)
| | |
|---|---|
| Trigger | New record in `Approvals Queue` (status Pending) |
| Steps | 1. Notify the approver. 2. Wait for the decision. 3. If Approved: run the action. If Rejected: do nothing. 4. Log the outcome. |
| Tables written | `Approvals Queue` (status, approver, timestamps), `Agent Action Log` |

### Scenario 3: PK order flow (Pakistan)
| | |
|---|---|
| Trigger | New COD order in Shopify |
| Steps | 1. Only if no COD app is installed: send the approved WhatsApp template with Confirm / Cancel. 2. Tag the order. 3. Reminder after 4 h; cancel after 24 h with no reply (both editable). 4. Confirmed orders go to courier booking. 5. Update the customer's risk record. |
| Tables written | `COD Risk`, `Agent Action Log` (order tags are written in Shopify) |

### Scenario 4: PK RTO tracker (Pakistan)
| | |
|---|---|
| Trigger | Courier status update |
| Steps | 1. Save the courier status to Airtable. 2. Refused parcel: add 1 to the refused count in `COD Risk`. 3. Weekly: RTO by city, courier and product goes into the brief. |
| Tables written | `COD Risk`, `Daily Briefs` (weekly RTO section), `Agent Action Log`; courier status goes to the table named in `airtable/brand-brain-schema.md` |

## 5. Not in v1

| Item | Where it goes |
|---|---|
| Phase C: managed AI agents (code-based) | Later, only for big US clients with high spend and a developer |
| Content calendar -> Canva -> scheduling automation | `BACKLOG.md` (v1 is manual: calendar in Airtable, design in Canva, schedule in Meta Business Suite) |
| Ad-rule alerts | `BACKLOG.md` |
| Weekly product research scheduling | `BACKLOG.md` (v1 is on demand) |
| US Klaviyo and Gorgias reporting | `BACKLOG.md` (v1 uses each app's own reports) |

Also out of scope by decision: Lindy, Gumloop and Relevance AI. Make is the default automation platform; n8n uses the same designs if the owner prefers it (check n8n's Sustainable Use License first; one instance per client).

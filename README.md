# E-commerce AI Agents

Master template for running e-commerce brands with AI agents, from products and store to creatives, ads, social, support, orders and reporting.

Built for two markets:
- **Pakistan:** cash on delivery, WhatsApp, local couriers.
- **USA:** cards, email/SMS, Google + Meta + TikTok ads.

The master copy lives in the agency's accounts. Each client gets their own copy inside accounts the client owns.

## How it works
- **Shopify + ready-made apps** for anything an app already does (COD confirmation, courier booking, helpdesk, email).
- **Make + Airtable** as the 24/7 brain: daily brief, approvals, AI steps, cross-app logic.
- **Brand Brain** (Airtable) holds the brand, products, policies, KPI caps, approvals and the action log. Every agent reads from it.
- Agents start at autonomy level 1 (Watch) or 2 (Draft) and move up after about two weeks of clean work. Anything that spends money stops at level 3.

Details: [docs/architecture.md](docs/architecture.md)

## What's in here
| Folder | Contents |
|---|---|
| `airtable/` | Brand Brain schema (10 tables) |
| `make/` | Make scenarios as blueprint JSON: daily brief, approval handler, PK order flow, WhatsApp replies, RTO tracker |
| `prompts/` | One prompt per agent, Pakistan and USA variants inside |
| `packs/` | Market packs: Pakistan (COD, couriers, WhatsApp templates in Urdu, Roman Urdu and English) and USA (Klaviyo, compliance) |
| `docs/` | Architecture, guardrails, client onboarding checklist |
| `proposals/` | Client proposals for both markets |
| `clients/_template/` | Client profile to copy for each new client |

Status and open items: [PROGRESS.md](PROGRESS.md), [BACKLOG.md](BACKLOG.md), [BLOCKERS.md](BLOCKERS.md)

## New client setup
1. Copy `clients/_template` to `clients/<client-name>` and fill in the profile.
2. Duplicate the Airtable base into the client's workspace. Fill Brand, Products, Policies and KPI caps.
3. The client creates their own Make account (Core plan) and invites the agency as admin. Import the blueprints, connect the client's accounts, test, and activate after approval.
4. Install the market-pack apps and run 5 to 10 test orders end to end.
5. Turn on the daily brief. Agents start at level 2 (Draft).

Meta verification, WhatsApp Business API, courier and payment accounts, Google Ads and TikTok take days to weeks. Start them on day 1: [docs/client-onboarding-checklist.md](docs/client-onboarding-checklist.md)

## Ground rules
- Nothing goes live (scenarios, posts, customer messages, ad spend changes) without the owner's approval.
- No secrets in this repo. Credentials live only in Make and Airtable connections; `.env.example` has placeholder names only.
- No real client data in the master template. Use placeholders like `{{client_name}}` and `{{market}}`.

Full list: [docs/guardrails.md](docs/guardrails.md)

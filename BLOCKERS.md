# BLOCKERS

Updated: 2026-11-13

| # | Blocker | Impact | Fallback / what the owner does |
|---|---|---|---|
| 1 | Make master account has no Airtable, Shopify, Meta or WhatsApp connections (only "Make's AI Provider") | Scenarios are built and saved but cannot run end to end | Add an Airtable connection in Make (owner OAuth) to test scenario 2. Shopify / Meta / WhatsApp connect per client |
| 2 | Running a Make scenario needs it activated or "Run once" in the editor | Guardrail: no activation without owner approval | Owner uses "Run once" in the Make editor, or approves a one-time test |
| 3 | AI model list for "Make's AI Provider" could not be read (Make RPC error) | "AI summary" module in scenario 1 has no connection/model picked | Open the module once and pick the connection and a model |
| 4 | Meta insights field list could not be read without a connection | ROAS is not mapped in the daily brief | Map `purchase_roas` after connecting the client's Meta account (in BACKLOG) |
| 5 | n8n connector failed to connect (connection refused) | None for v1 (Make is the default) | Ignore unless the owner wants n8n |
| 6 | No Shopify, Meta Ads or Klaviyo connection set up yet | Operator tasks (store build, ad reports) not available yet | Connect them when the first client is onboarded |

Working connectors: Airtable, Make (Pro plan), Canva, Gmail, Notion, Google Drive.

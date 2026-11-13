# PROGRESS

Updated: 2026-11-13 · Status: v1 built; live end-to-end runs wait on connections (see BLOCKERS.md)

## Done
| Block | Output | Where |
|---|---|---|
| 1. Setup | Folder layout; connector check (Airtable, Make Pro, Canva, Gmail, Notion, Drive work) | repo root, `BLOCKERS.md` |
| 2. Brand Brain | Airtable base `Brand Brain - MASTER`: 10 tables, 2 formulas, seed caps, placeholder Brand + Policies, dummy test rows | `airtable/brand-brain-schema.md` |
| 3. Make core | Folder MASTER TEMPLATE; scenarios 1, 2, 3, 3b, 4 created **inactive**; blueprints exported (no connections, no secrets) | `make/README.md`, `make/blueprints/` |
| 4. Prompts | 10 agent prompts + index, same 10 sections each, PK + US variants | `prompts/` |
| 5. Market packs | Pakistan + USA packs; 9 WhatsApp templates in Urdu, Roman Urdu, English; Klaviyo starter copy | `packs/` |
| 6. Client kit | Architecture, guardrails, onboarding checklist, client profile template, both proposals, `.env.example` | `docs/`, `clients/_template/`, `proposals/` |
| 7. Test | Blueprint JSON parses (5/5); Make accepted all 5 scenarios as valid; Airtable formulas checked on dummy rows (Margin % = 40, Refusal Rate = 25); Approval link field works | this file |

## Not tested yet
- No scenario has been **run**. Running needs (a) connections that do not exist in the master Make account and (b) activation, which needs the owner's approval.
- Make mapping formulas (revenue sum, tag searches, filters, `orderCancel` mutation) are unverified until the first run on a real store. List in `make/README.md`.
- Prompts, packs and client kit were spot-checked (structure, guardrail words, tags, template names), not read line by line.

## Next (owner)
1. Make -> add an Airtable connection, open scenario 2, pick the connection, "Run once" with the SAMPLE approval row. This is the one test possible without a client.
2. Read both proposals and fill `{{setup_fee}}` / `{{monthly_fee}}`.
3. First client: start the day-1 dependencies in `docs/client-onboarding-checklist.md`, then follow "Per-client setup" in `make/README.md`.
4. Delete the SAMPLE rows when duplicating the base for a client.

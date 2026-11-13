# BACKLOG

Updated: 2026-11-13. Everything that did not fit v1.

## Planned after v1
- [ ] Content calendar -> Canva -> scheduling scenario
- [ ] Ad-rule alerts (spend above cap, ROAS below target)
- [ ] Weekly product research on a schedule
- [ ] US Klaviyo and Gorgias reporting in the daily brief
- [ ] Phase C: managed AI agents (code-based) for large US clients

## Found while building v1
- [ ] Daily brief: add ROAS (Meta `purchase_roas`), Google and TikTok spend, US fields (cost per customer, repeat rate, chargebacks)
- [ ] Daily brief: Delivered % and RTO % for PK (needs courier status counts per day)
- [ ] Weekly RTO rollup by city, courier and product (data is already in `Agent Action Log`, System = Courier)
- [ ] Daily brief on WhatsApp for PK owners (email only in v1)
- [ ] Approval handler: auto-run branches (price change, budget change, refund) once an agent reaches level 3; v1 emails the operator
- [ ] Approval handler: stop repeat "Pending" emails when a pending row is edited (add a Notified checkbox)
- [ ] PK order flow: read reminder / cancel hours from `KPI Targets & Caps` instead of the CONFIG module
- [ ] PK order flow: skip or switch to prepaid-only for phones flagged Block in `COD Risk (PK)`
- [ ] WhatsApp replies: AI draft reply for free-text messages (Support agent), human approves
- [ ] Daily brief: pagination above 250 orders per day
- [ ] n8n versions of the same scenarios (only if the owner wants n8n; check the Sustainable Use License first)
- [ ] Align KPI row names in `prompts/` with the exact `Metric` values in the base
- [ ] Sample rows for Content Calendar and Ad Experiments

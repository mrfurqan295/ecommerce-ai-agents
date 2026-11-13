# Guardrails (non-negotiable)

These rules apply to every agent, every scenario and every client copy. If a rule and a prompt disagree, the rule wins.

## 1. Checklist

| # | Guardrail | How it is enforced |
|---|---|---|
| 1 | Never activate a scenario, publish content, message customers or change ad spend without the owner's approval. | Scenarios are built inactive; agents start at level 1 or 2; every such request goes through `Approvals Queue` (Make scenario 2). |
| 2 | Hard spending limits are set inside Meta, Google and TikTok themselves, not only in prompts. | Account and campaign spending limits are set in each ad platform during onboarding; the same cap is copied to `KPI Targets & Caps`. |
| 3 | Approval is required for: new campaigns, budgets above cap, price changes over 10%, refunds above limit, new products, public posts in the first month. | Thresholds live in `KPI Targets & Caps`; the request is created in `Approvals Queue`; nothing runs until status is Approved. |
| 4 | No secrets in files. Credentials live only in Make/Airtable connections. | `.env.example` holds placeholder names only; client profile says "no passwords or API keys"; files are checked before handover. |
| 5 | No real client data in the master template. | Placeholders only (`{{client_name}}`, `{{market}}`); real data goes only into the client's own copy and `clients/<client-name>/`. |
| 6 | Official APIs and connectors only. No browser bots on ad or social accounts. | Only Make modules, Shopify apps and official connectors are used; access is granted as admin/partner, never by shared login. |
| 7 | Product facts come only from the Brand Brain. Health, safety and "best / #1" claims are blocked. | Prompts read `Products` (allowed claims, FAQs) and `Brand` (banned words); drafts with a blocked claim are rejected at review. |
| 8 | Reviews only from real customers. No fake reviews or testimonials. AI avatars never pose as real buyers. | Creative and social prompts forbid it; reviewer checks every creative before approval; the FTC rule bans AI-generated reviews. |
| 9 | WhatsApp: opt-in customers and approved templates only. | Templates are submitted for approval in WhatsApp Business before use; scenario 3 sends only approved templates to customers who placed an order or opted in. |
| 10 | Every agent action is logged. | Each scenario and each operator session writes time, agent, action, system, before/after and result to `Agent Action Log`. |

Pre-go-live check (tick per client):
- [ ] All scenarios are inactive until the go-live sign-off.
- [ ] Spending limits are set inside each ad platform in use.
- [ ] `KPI Targets & Caps` is filled and matches the client profile.
- [ ] Approvers and their channels are named in the client profile.
- [ ] No passwords, API keys or tokens in any file.
- [ ] WhatsApp templates are approved (PK) / SMS consent and unsubscribe links are in place (US).
- [ ] `Agent Action Log` receives a row from a test run of each scenario.

## 2. Approval matrix

Seed values. All are editable per client in `KPI Targets & Caps`.

| Action | Threshold | Who approves | Where it is logged |
|---|---|---|---|
| Ad budget change | Over 20% per day, or above the daily ad spend cap | Client approver; agency owner informed | `Approvals Queue` + `Agent Action Log` |
| Price change | Over 10% | Client approver | `Approvals Queue` + `Agent Action Log` |
| Refund | Above US $50 / Rs 3,000 | Client approver | `Approvals Queue` + `Agent Action Log` |
| New campaign | Any | Client approver + agency owner | `Approvals Queue` + `Agent Action Log` |
| New product | Any | Client approver | `Approvals Queue` + `Agent Action Log` |
| Public post | Any, in the first month | Client approver (or agency owner if the client delegates in writing) | `Approvals Queue` + `Content Calendar` status + `Agent Action Log` |
| Activating a scenario | Any | Agency owner, after the client's go-live sign-off | `Agent Action Log` + onboarding checklist sign-off |
| Raising an agent's autonomy level | Any | Agency owner | Client profile + `Agent Action Log` |

Rules for the queue:
- A request with no decision stays Pending. No reply never means yes.
- Approver names and channels come from the client profile. US clients: urgent approvals go to the client's team because US daytime is night in Pakistan.
- Actions inside the limits at level 3 do not need a queue entry, but are still logged.

## 3. Incident steps

Use when an agent or scenario does something wrong (wrong message, wrong price, overspend, bad claim, action without approval).

1. **Pause.** Set the scenario to inactive in Make. If money is being spent, the owner or client pauses the campaign inside the ad platform.
2. **Log.** Add a row to `Agent Action Log`: time, agent, what happened, system, before/after, result = "Incident".
3. **Notify.** Tell the agency owner and the client approver at once, on the channel in the client profile. Say what happened, what is paused and what is next.
4. **Revert.** Use the before/after values in the log to undo the change (price, budget, tag, post). If customers were messaged wrongly, the client approves any correction message before it is sent.
5. **Review.** Find the cause (prompt, missing cap, wrong data in the Brand Brain, scenario logic). Fix it, test on dummy data, and move the agent down one autonomy level.
6. **Restart.** Reactivate only after the agency owner approves. The 2-week clean-work clock starts again.

Incident record (copy into the client folder):

| Field | Value |
|---|---|
| Date and time | |
| Client | `{{client_name}}` |
| Agent / scenario | |
| What happened | |
| Impact (orders, amount, customers) | |
| Paused at | |
| Reverted at | |
| Cause | |
| Fix | |
| Reactivation approved by | |

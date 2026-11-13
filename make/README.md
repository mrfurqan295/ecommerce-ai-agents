# Make scenarios (MASTER TEMPLATE)

All scenarios live in the owner's Make account, folder **MASTER TEMPLATE**, and are **inactive**. Nothing is activated without the owner's approval.

| # | Scenario | Make id | Trigger | Blueprint |
|---|---|---|---|---|
| 1 | Daily brief | 7017636 | Daily 08:00 (scenario time zone) | `blueprints/1-daily-brief.json` |
| 2 | Approval handler | 7017652 | Airtable watch, every 15 min | `blueprints/2-approval-handler.json` |
| 3 | PK order flow: confirm, remind, cancel | 7017680 | Every 15 min | `blueprints/3-pk-order-flow.json` |
| 3b | PK order flow: WhatsApp replies | 7017681 | Instant (WhatsApp webhook) | `blueprints/3b-pk-whatsapp-replies.json` |
| 4 | PK RTO tracker | 7017682 | Instant (custom webhook) | `blueprints/4-pk-rto-tracker.json` |

Scenario 3 is split in two because a Make scenario can have only one trigger: 3 polls Shopify, 3b listens for the customer's Confirm / Cancel tap.

## What each one does
1. **Daily brief:** Shopify orders (yesterday) + Meta ad spend -> revenue, orders, ad spend, MER, COD confirmed % -> AI summary -> `Daily Briefs` row -> email -> `Agent Action Log`.
2. **Approval handler:** watches `Approvals Queue`. Pending -> emails the approver. Approved -> ticks `Executed`, sets `Decided At`, emails the approved action to the operator, logs it. Rejected -> sets `Decided At`, logs "Skipped".
3. **PK order flow:** new COD order -> WhatsApp `order_confirmation` -> tag `cod-pending`. After 4 h -> `confirmation_reminder` + tag `cod-reminded`. After 24 h with no reply -> cancel order, tag `cod-no-reply`, send `order_cancelled_no_reply`, log.
3b. **WhatsApp replies:** Confirm -> tag `cod-confirmed` (the courier app books on this tag), thank-you template, log. Cancel -> cancel order, tag `cod-cancelled`, log. Free text -> emailed to support.
4. **PK RTO tracker:** courier status webhook -> log row -> tag the Shopify order -> on a final status update `COD Risk (PK)`: Orders +1, Refused Count +1 if refused/RTO, Flag = Watch at 1, Block at 2.

Use scenario 3 + 3b **only if the client has no COD confirmation app**. If they use one, keep 1, 2 and 4.

## Per-client setup (click-steps)
1. Client's Make account -> Scenarios -> Create -> ... menu -> **Import blueprint** -> pick the JSON file. Repeat for each file.
2. Open every module that shows a warning and pick the client's **connection** (Shopify, Airtable, Meta, WhatsApp). The blueprints carry no connections and no secrets.
3. Airtable modules: change the base from the master (`appspopIsF0THCKer`) to the client's copy. Table and field ids stay the same in a duplicated base; if Make shows empty fields, re-pick the table once.
4. Replace the placeholders:
   - `CLIENT_NAME`, market (`PK` or `US`) and currency in the first "CONFIG" module of scenario 1.
   - `OWNER_EMAIL` in the email modules ("Send an Email to a Team Member" only accepts a member of that Make team; swap for Gmail or WhatsApp if the client wants).
   - `WHATSAPP_PHONE_NUMBER_ID` in scenarios 3 and 3b.
5. Scenario 1: pick the Business Manager and ad account in the Meta module, and the AI connection + model in the "AI summary" module.
6. Scenario 3b: create the WhatsApp webhook in the trigger module. Scenario 4: create a new custom webhook and give its URL to the courier app.
7. WhatsApp templates must be approved by Meta first (see `packs/pakistan/whatsapp-templates.md`). In `order_confirmation`, set the quick-reply button payloads to `CONFIRM|<order id>` and `CANCEL|<order id>`, mapped from the Shopify order `ID` (gid format).
8. Set the scenario time zone to the client's time zone (Daily brief runs at 08:00 there).
9. Run each scenario once with "Run once" on a test order, check Airtable, then ask the owner before activating.

## Check on the first real run (not yet verified)
- Scenario 1: the revenue sum reads `totalPriceSet.amount` from each order; confirm the number matches Shopify. Max 250 orders per day per search; raise or paginate for bigger stores.
- Scenario 1 covers Meta spend only. ROAS, Google and TikTok spend, Delivered % and RTO % are not filled yet (see BACKLOG.md).
- Scenario 3: COD orders are detected as `financial_status:pending` without the `prepaid` tag. Adjust the search if the store marks COD differently.
- Scenarios 3 and 3b: the `orderCancel` GraphQL mutation arguments depend on the Shopify API version; test on a dummy order before use.
- Scenario 4 expects JSON like `{"order_id": "gid://shopify/Order/123", "order_name": "#1001", "phone": "+92...", "city": "...", "courier": "...", "sku": "...", "status": "delivered"}`. Map the courier app's field names to these.
- Scenario 2 sends approved actions to the operator; it does not change prices, budgets or refunds by itself in v1.

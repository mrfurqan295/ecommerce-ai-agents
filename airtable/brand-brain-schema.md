# Brand Brain - MASTER (Airtable schema)

- Base: `Brand Brain - MASTER`, id `appspopIsF0THCKer`, workspace "My First Workspace" (move it if you prefer another workspace).
- Per client: duplicate the base into the client's own workspace, then fill Brand, Products, Policies & SOPs, KPI Targets & Caps.
- Money fields are plain numbers; the currency is `Brand.Currency`. Percent fields store 0.85 for 85%.
- Date-time fields are set to Asia/Karachi; change per client.

| # | Table (id) | Fields (first = primary) |
|---|---|---|
| 1 | Brand (`tblJFUAzZVPahAz2f`) | Brand Name, Market (PK/US), Voice, Audience, USP, Banned Words, Logo Link, Brand Colors, Currency (PKR/USD), Timezone, Languages, Store URL, Approver Contact |
| 2 | Products (`tbl0ZoZ2938UgaDO5`) | SKU, Title, Description, Price, Cost, Stock, Allowed Claims, FAQs, Status (Active/Draft/Archived), Margin % (formula) |
| 3 | Policies & SOPs (`tblxnIeTxAHyknaIB`) | Topic, Text, Market (PK/US/Both), Last Reviewed |
| 4 | KPI Targets & Caps (`tblBY84YTEDgU9MC2`) | Metric, Market, Target, Hard Limit, Approval Threshold, Unit, Notes |
| 5 | Approvals Queue (`tbl004S8X2Qum9u4G`) | Request, Agent, Action Type, Impact Amount, Details, Action Payload, Status (Pending/Approved/Rejected), Approver, Requested At, Decided At, Executed, Last Modified |
| 6 | Agent Action Log (`tblhK6iEKzos8bAue`) | Action, Time, Agent, System, Before, After, Result (Success/Failed/Skipped), Notes, Approval (link to Approvals Queue) |
| 7 | Daily Briefs (`tblJCw8T8rM3GGmWV`) | Date, Market, Revenue, Orders, Ad Spend, ROAS, MER, Confirmed % (PK), Delivered % (PK), RTO % (PK), Cost per Customer (US), Repeat Rate % (US), Chargebacks (US), Issues, AI Summary |
| 8 | Content Calendar (`tblQ9WgwTrAO6Yk9e`) | Post Title, Date, Channel, Format, Caption, Creative Link, Status (Idea/Draft/Needs approval/Approved/Scheduled/Published) |
| 9 | Ad Experiments (`tblWkrh9tRLPezkRt`) | Hypothesis, Platform, Creative, Audience, Budget, Start Date, End Date, Result, Decision (Pending/Scale/Iterate/Kill) |
| 10 | COD Risk (PK) (`tblPflZUQ9dP2Bh0U`) | Phone, City, Orders, Refused Count, Flag (OK/Watch/Block), Last Order Date, Notes, Refusal Rate (formula) |

## Formulas
- Products `Margin %`: `IF({Price}>0, ROUND(({Price}-{Cost})/{Price}*100, 1), BLANK())`
- COD Risk `Refusal Rate`: `IF({Orders}>0, ROUND({Refused Count}/{Orders}*100, 1), 0)`

## Seed data already in the base
- Brand: 1 placeholder row (`{{client_name}}` ...).
- Policies & SOPs: 9 placeholder topics (shipping, returns, refunds, support, COD confirmation, prepaid discount, repeat refusers, email/SMS consent, reviews).
- KPI Targets & Caps: 19 rows. Seed limits: max budget change 20%/day; price change over 10% needs approval; refunds above US $50 / Rs 3,000 need approval; COD reminder 4 h; COD auto-cancel 24 h; COD Risk Watch at 1 refusal, Block at 2. `Daily ad spend cap` is empty on purpose: set it per client (and inside Meta/Google/TikTok). KPI targets are empty: set per client.

## Added after the first pass
- Approvals Queue has a `Last Modified` (lastModifiedTime) field. It is the trigger field for the Make approval handler.
- Dummy test rows, all marked SAMPLE (delete per client): 1 product, 1 pending approval, 1 action log row linked to that approval, 1 daily brief, 1 COD Risk phone (`+920000000000`).
- Content Calendar and Ad Experiments have no rows yet.

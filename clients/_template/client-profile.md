# Client profile: {{client_name}}

> **No passwords or API keys in this file.** Credentials live only in Make / Airtable connections inside the client's own accounts. Record who owns an account and whether access is granted, nothing more.

Copy this folder to `clients/<client-name>/` and replace every `{{placeholder}}`. The Airtable Brand Brain is the working copy; keep this file in step with it.

## 1. Business basics

| Field | Value |
|---|---|
| Client / brand name | `{{client_name}}` |
| Legal business name | `{{legal_name}}` |
| Market | `{{market}}` (PK / US) |
| Store URL | `{{store_url}}` |
| Time zone | `{{timezone}}` |
| Currency | `{{currency}}` |
| Main contact | `{{contact_name}}`, `{{contact_role}}` |
| Contact channel | `{{contact_channel}}` (WhatsApp / email) |
| Start date | `{{start_date}}` |
| Go-live date | `{{go_live_date}}` |

## 2. Products summary

| Field | Value |
|---|---|
| Category | `{{product_category}}` |
| Number of SKUs | `{{sku_count}}` |
| Price range | `{{price_range}}` |
| Top sellers | `{{top_products}}` |
| Stock held by | `{{stock_location}}` (own / supplier / 3PL) |
| Allowed claims (source) | `Products` table in the Brand Brain |

Product facts come only from the Brand Brain. No health, safety or "best / #1" claims.

## 3. Brand

| Field | Value |
|---|---|
| Brand voice | `{{brand_voice}}` |
| Audience | `{{audience}}` |
| USP | `{{usp}}` |
| Banned words | `{{banned_words}}` |
| Customer languages | `{{languages}}` (PK: Urdu / Roman Urdu / English) |
| Logo link | `{{logo_link}}` |
| Brand colors link | `{{colors_link}}` |

## 4. Accounts and access

Every account is owned by the client. The agency is invited as admin / partner. Mark rows that do not apply to this market as N/A.

| Account | Owner | Access granted (yes/no) | Notes |
|---|---|---|---|
| Shopify | `{{client_name}}` | `{{yes_no}}` | `{{notes}}` |
| Meta (Business Manager, ad account, Pixel + Conversions API) | `{{client_name}}` | `{{yes_no}}` | Verification status: `{{meta_verification_status}}` |
| Google (Ads + Merchant Center) | `{{client_name}}` | `{{yes_no}}` | `{{notes}}` |
| TikTok (Ads; posting audit) | `{{client_name}}` | `{{yes_no}}` | Audit status: `{{tiktok_audit_status}}` |
| WhatsApp Business API | `{{client_name}}` | `{{yes_no}}` | Template status: `{{whatsapp_template_status}}` |
| Klaviyo | `{{client_name}}` | `{{yes_no}}` | `{{notes}}` |
| Gorgias | `{{client_name}}` | `{{yes_no}}` | `{{notes}}` |
| Couriers | `{{client_name}}` | `{{yes_no}}` | Couriers used: `{{courier_list}}` |
| Payment gateway | `{{client_name}}` | `{{yes_no}}` | Gateway: `{{payment_gateway}}` |
| Make (Core plan) | `{{client_name}}` | `{{yes_no}}` | Agency owner invited as admin |
| Airtable (Brand Brain copy) | `{{client_name}}` | `{{yes_no}}` | Base name: `{{airtable_base_name}}` |

## 5. KPI targets and caps

Seed values are shown in brackets. Edit per client; keep the same numbers in the `KPI Targets & Caps` table and inside the ad platforms.

| Cap / threshold | Value |
|---|---|
| Daily ad spend cap | `{{daily_ad_spend_cap}}` |
| Max budget change per day | `{{max_budget_change_pct}}` (seed: 20%) |
| Price-change approval threshold | `{{price_change_threshold_pct}}` (seed: over 10%) |
| Refund approval threshold | `{{refund_threshold}}` (seed: above US $50 / Rs 3,000) |
| Spending limit set inside Meta | `{{yes_no}}` |
| Spending limit set inside Google | `{{yes_no}}` |
| Spending limit set inside TikTok | `{{yes_no}}` |

| KPI | Target |
|---|---|
| PK: confirmation rate | `{{target_confirmation_rate}}` |
| PK: delivered % | `{{target_delivered_pct}}` |
| PK: RTO % | `{{target_rto_pct}}` |
| PK: cost per delivered order | `{{target_cost_per_delivered_order}}` |
| US: MER / ROAS | `{{target_mer_roas}}` |
| US: cost per customer | `{{target_cost_per_customer}}` |
| US: AOV | `{{target_aov}}` |
| US: repeat rate | `{{target_repeat_rate}}` |
| US: chargebacks | `{{target_chargebacks}}` |

Targets are goals to track, not promises.

## 6. Approvers

| What | Approver name | Channel | Backup |
|---|---|---|---|
| Ad budgets and new campaigns | `{{approver_ads}}` | `{{channel}}` | `{{backup}}` |
| Price changes and new products | `{{approver_catalog}}` | `{{channel}}` | `{{backup}}` |
| Refunds above threshold | `{{approver_refunds}}` | `{{channel}}` | `{{backup}}` |
| Public posts (first month) | `{{approver_content}}` | `{{channel}}` | `{{backup}}` |
| Urgent, outside agency hours | `{{approver_urgent}}` | `{{channel}}` | `{{backup}}` |
| Daily brief recipients | `{{brief_recipients}}` | `{{brief_channel}}` | |

## 7. Agent autonomy levels

1 Watch, 2 Draft, 3 Act within limits, 4 Autonomous. Agents that spend money stop at 3. Moving up needs about 2 weeks of clean work and the agency owner's sign-off.

| Agent | Current level | Since (date) | Next review | Signed off by |
|---|---|---|---|---|
| Orchestrator + finance & KPIs | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| Catalog & pricing | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| SEO & AI search | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| Creative studio | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| Paid ads | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| Social | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| Email & SMS (US) | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| Support | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| Orders & shipping | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |
| Product research | `{{level}}` | `{{date}}` | `{{date}}` | `{{name}}` |

## 8. Go-live

| Field | Value |
|---|---|
| Go-live date | `{{go_live_date}}` |
| Test orders run (5-10) | `{{test_order_count}}` |
| Sign-off by | `{{client_approver_name}}` |
| Sign-off link | `{{signoff_link}}` |

## 9. Notes

- `{{notes}}`

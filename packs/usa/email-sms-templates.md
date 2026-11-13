# Email and SMS Starter Copy: USA

Starter skeletons for the five Klaviyo flows for `{{client_name}}`. First message of each flow only; later messages reuse the same pattern.
Drafts only. Nothing is sent until the owner approves and the flow is turned live.

## Rules

- [ ] Fill every placeholder from the Brand Brain. Rewrite in the brand voice from Airtable `Brand`.
- [ ] Placeholders here are plain names (`{{first_name}}`). Map them to Klaviyo's own template tags when building: verify at onboarding.
- [ ] No health, safety or "best / #1" claims. No invented numbers, deadlines or stock warnings.
- [ ] No fake reviews or testimonials. Quote a review only if it is from a real customer and you have the right to use it.
- [ ] Discounts only if the client approved them in `KPI Targets & Caps`. No discount approved: delete the discount line.
- [ ] Every email ends with the footer below. Every SMS names the brand and gives opt-out wording.
- [ ] SMS goes only to profiles with explicit SMS consent.
- [ ] Not legal advice; client confirms consent wording with counsel.

**Email footer (all emails)**
```
{{client_name}} | {{company_mailing_address}}
You are receiving this email because you signed up at {{store_url}}.
Unsubscribe: {{unsubscribe_link}}
```

---

## 1. Welcome

- Trigger: subscribes to the email list.
- Subject: `Welcome to {{client_name}}`
- Preview: `Here is what to expect from us.`

```
Hi {{first_name}},

Thanks for signing up. {{client_name}} makes {{product_category}} for {{audience}}.
{{brand_usp_one_line}}
We will email you about new products, how-to tips and the occasional offer.
{{optional_welcome_offer_line: Use code {{discount_code}} on your first order.}}

[Shop now -> {{store_url}}]
```

## 2. Abandoned cart

- Trigger: started checkout, no order placed.
- Subject: `You left something in your cart`
- Preview: `{{product_title}} is still saved for you.`

```
Hi {{first_name}},

You left {{product_title}} in your cart at {{client_name}}.
Your cart is saved, so you can pick up where you stopped.
Questions about shipping or returns? Reply to this email or see {{policy_url}}.

[Return to cart -> {{cart_url}}]
```

## 3. Browse abandonment

- Trigger: viewed a product, no cart and no order.
- Subject: `Still thinking about {{product_title}}?`
- Preview: `A quick look at the details.`

```
Hi {{first_name}},

You recently looked at {{product_title}}.
{{product_fact_1}}
{{product_fact_2}}
If you have a question before you decide, reply to this email and we will help.

[View {{product_title}} -> {{product_url}}]
```

## 4. Post-purchase

- Trigger: order placed (email 1); order delivered (review request, later email).
- Subject: `Thank you for your order, {{first_name}}`
- Preview: `What happens next with order {{order_number}}.`

```
Hi {{first_name}},

Thank you for ordering {{product_title}} from {{client_name}}.
Order {{order_number}} is being prepared. We will email tracking details when it ships.
Getting started: {{product_usage_tip}}
Need help? Reply to this email or visit {{support_url}}.

[View your order -> {{order_status_url}}]
```

Review request (later email, after delivery)
- Subject: `How is your {{product_title}}?`

```
Hi {{first_name}},

You have had {{product_title}} for a little while now.
Would you share an honest review? Good or bad, it helps other shoppers and helps us improve.

[Write a review -> {{review_url}}]
```

## 5. Win-back

- Trigger: no order for `{{winback_days}}` days (set per client).
- Subject: `It has been a while, {{first_name}}`
- Preview: `Here is what is new at {{client_name}}.`

```
Hi {{first_name}},

We have not seen you at {{client_name}} for a while.
Since your last order we have added {{new_product_or_update}}.
{{optional_winback_offer_line: Use code {{discount_code}} on your next order.}}
Not interested anymore? You can unsubscribe below at any time.

[See what is new -> {{store_url}}]
```

---

## SMS

### Opt-in line (signup form or checkout, unchecked by default, separate from email consent)

```
By checking this box and entering your phone number, you agree to receive recurring automated marketing text messages from {{client_name}} at the number provided. Consent is not a condition of purchase. Message frequency varies. Message and data rates may apply. Reply STOP to unsubscribe or HELP for help. See our Privacy Policy ({{privacy_policy_url}}) and Terms ({{terms_url}}).
```

### SMS example 1: abandoned cart

```
{{client_name}}: Hi {{first_name}}, you left {{product_title}} in your cart. Finish checkout here: {{cart_url}} Reply STOP to opt out.
```

### SMS example 2: welcome

```
{{client_name}}: Thanks for signing up for texts, {{first_name}}. Expect news and offers from us. Shop: {{store_url}} Msg and data rates may apply. Reply STOP to opt out, HELP for help.
```

SMS checklist
- [ ] Brand name at the start of every message.
- [ ] Opt-out wording in every marketing message.
- [ ] Sent in the recipient's local daytime only.
- [ ] Short link goes to the client's own domain or the Klaviyo-provided link: verify at onboarding.
- [ ] STOP replies are honored automatically by Klaviyo: verify at onboarding.

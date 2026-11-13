# WhatsApp Business Templates: Pakistan

Drafts for `{{client_name}}`. Each template has three versions: Urdu, Roman Urdu, English.
These are drafts. Nothing is sent until Meta approves the template and the owner approves going live.

## Rules (read first)

- [ ] **Opt-in customers only.** Send only to customers who agreed to WhatsApp messages (for example a checkbox at checkout). Keep proof of opt-in.
- [ ] **Meta approval first.** Every template must be approved by Meta before use. Approval times and message fees change: check current Meta policy.
- [ ] **Utility templates carry no promotion.** No discounts, offers, upsells or "shop now" lines in a Utility template. Meta may re-categorise or reject it. Promotions go in Marketing templates only.
- [ ] **24-hour customer service window.** After a customer messages the business, free-form replies are allowed for 24 hours. Outside that window, only approved templates can be sent. Check current Meta policy for details.
- [ ] **One language per template submission.** Submit each language version separately under the same template name. Roman Urdu has no clear language option of its own: verify at onboarding which language to file it under, or submit it under a separate name such as `order_confirmation_roman`.
- [ ] **Variables.** Meta uses numbered variables: `{{1}}`, `{{2}}`. Do not start or end the body with a variable. Give Meta a sample value for each one when submitting.
- [ ] **Same variable order in all three languages**, so one Make mapping works for every version.
- [ ] **Facts only from the Brand Brain.** No health, safety or "best / #1" claims. No fake reviews.
- [ ] **Marketing templates need an easy opt-out** and respect a customer who asks to stop.
- [ ] Keep button text short. Button limits and allowed button combinations: check current Meta policy.
- [ ] No real customer data in this file. Sample values only.

How the variables are filled: `{{1}}`, `{{2}}` are Meta's slots. The line under each template says which Shopify or Brand Brain field goes into each slot.

The English versions open with "Hello". Change the greeting per client if the brand voice in Airtable `Brand` says otherwise.

---

## 1. order_confirmation

- **Category:** Utility
- **When:** new COD order (flow step 2)
- **Variables:** `{{1}}` customer first name; `{{2}}` order number; `{{3}}` store name (`{{client_name}}`); `{{4}}` order total in rupees
- **Buttons:** two quick replies (Confirm, Cancel)

**Urdu**
```
السلام علیکم {{1}}، {{3}} پر آرڈر {{2}} دینے کا شکریہ۔ کل رقم {{4}} روپے ہے، ادائیگی کیش آن ڈیلیوری۔ آرڈر کنفرم کرنے کے لیے نیچے "کنفرم کریں" دبائیں۔ اگر آرڈر نہیں چاہیے تو "کینسل کریں" دبائیں۔
```
Buttons: `کنفرم کریں` | `کینسل کریں`

**Roman Urdu**
```
Assalam o Alaikum {{1}}, {{3}} par order {{2}} dene ka shukriya. Total Rs {{4}} hai, payment cash on delivery. Order confirm karne ke liye neeche "Confirm karein" dabayein. Agar order nahi chahiye to "Cancel karein" dabayein.
```
Buttons: `Confirm karein` | `Cancel karein`

**English**
```
Hello {{1}}, thank you for your order {{2}} at {{3}}. The total is Rs {{4}}, cash on delivery. Please tap "Confirm" below to confirm your order, or "Cancel" if you do not want it.
```
Buttons: `Confirm` | `Cancel`

---

## 2. confirmation_reminder

- **Category:** Utility
- **When:** no reply 4 h after the order (editable)
- **Variables:** `{{1}}` customer first name; `{{2}}` order number; `{{3}}` store name; `{{4}}` auto-cancel window in hours (default 24, from Airtable `KPI Targets & Caps`)
- **Buttons:** two quick replies (Confirm, Cancel)

**Urdu**
```
السلام علیکم {{1}}، {{3}} پر آپ کا آرڈر {{2}} ابھی تک کنفرم نہیں ہوا۔ براہِ کرم "کنفرم کریں" دبائیں تاکہ ہم آرڈر روانہ کر سکیں۔ جو آرڈر {{4}} گھنٹے کے اندر کنفرم نہ ہو، وہ خود بخود کینسل ہو جاتا ہے۔
```
Buttons: `کنفرم کریں` | `کینسل کریں`

**Roman Urdu**
```
Assalam o Alaikum {{1}}, {{3}} par aap ka order {{2}} abhi tak confirm nahi hua. Barah-e-karam "Confirm karein" dabayein taake hum order rawana kar sakein. Jo order {{4}} ghantay ke andar confirm na ho, woh khud cancel ho jata hai.
```
Buttons: `Confirm karein` | `Cancel karein`

**English**
```
Hello {{1}}, your order {{2}} at {{3}} is still waiting for confirmation. Please tap "Confirm" so we can dispatch it. Orders that are not confirmed within {{4}} hours are cancelled automatically.
```
Buttons: `Confirm` | `Cancel`

---

## 3. order_cancelled_no_reply

- **Category:** Utility
- **When:** no reply 24 h after the order (editable); order auto-cancelled
- **Variables:** `{{1}}` customer first name; `{{2}}` order number; `{{3}}` store name
- **Buttons:** none

**Urdu**
```
السلام علیکم {{1}}، ہمیں آپ کی کنفرمیشن موصول نہیں ہوئی، اس لیے {{3}} پر آپ کا آرڈر {{2}} کینسل کر دیا گیا ہے۔ آپ کو کوئی ادائیگی نہیں کرنی۔ اگر آپ کو یہ آرڈر چاہیے تو اسی میسج کا جواب دیں، ہماری ٹیم آپ کی مدد کرے گی۔
```

**Roman Urdu**
```
Assalam o Alaikum {{1}}, humein aap ki confirmation nahi mili, is liye {{3}} par aap ka order {{2}} cancel kar diya gaya hai. Aap ko koi payment nahi karni. Agar aap ko yeh order chahiye to isi message ka reply karein, hamari team aap ki madad karegi.
```

**English**
```
Hello {{1}}, we did not receive your confirmation, so your order {{2}} at {{3}} has been cancelled. You do not need to pay anything. If you still want this order, reply to this message and our team will help you.
```

---

## 4. order_confirmed_thanks

- **Category:** Utility
- **When:** customer taps Confirm
- **Variables:** `{{1}}` customer first name; `{{2}}` order number; `{{3}}` order total in rupees
- **Buttons:** none

**Urdu**
```
شکریہ {{1}}، آپ کا آرڈر {{2}} کنفرم ہو گیا ہے۔ ہم اسے روانہ کرنے کی تیاری کر رہے ہیں اور ٹریکنگ کی تفصیل اسی نمبر پر بھیجیں گے۔ ڈیلیوری کے وقت {{3}} روپے نقد تیار رکھیں۔
```

**Roman Urdu**
```
Shukriya {{1}}, aap ka order {{2}} confirm ho gaya hai. Hum isay rawana karne ki tayyari kar rahe hain aur tracking ki tafseel isi number par bhejenge. Delivery ke waqt Rs {{3}} cash tayyar rakhein.
```

**English**
```
Thank you {{1}}, your order {{2}} is confirmed. We are preparing it for dispatch and will send the tracking details to this number. Please keep Rs {{3}} in cash ready for delivery.
```

---

## 5. order_dispatched

- **Category:** Utility
- **When:** courier booked and parcel handed over
- **Variables:** `{{1}}` customer first name; `{{2}}` order number; `{{3}}` courier name; `{{4}}` tracking number
- **Buttons:** optional URL button "Track order" pointing to the courier's tracking page (only if the courier app gives a tracking link: verify at onboarding)

**Urdu**
```
السلام علیکم {{1}}، آپ کا آرڈر {{2}} روانہ کر دیا گیا ہے۔ کورئیر: {{3}}۔ ٹریکنگ نمبر: {{4}}۔ ڈیلیوری کے دن ہم آپ کو دوبارہ میسج کریں گے۔
```
Button (optional): `آرڈر ٹریک کریں`

**Roman Urdu**
```
Assalam o Alaikum {{1}}, aap ka order {{2}} rawana kar diya gaya hai. Courier: {{3}}. Tracking number: {{4}}. Delivery ke din hum aap ko dobara message karenge.
```
Button (optional): `Order track karein`

**English**
```
Hello {{1}}, your order {{2}} has been dispatched. Courier: {{3}}. Tracking number: {{4}}. We will message you again on the day of delivery.
```
Button (optional): `Track order`

---

## 6. out_for_delivery

- **Category:** Utility
- **When:** courier status = out for delivery
- **Variables:** `{{1}}` customer first name; `{{2}}` order number; `{{3}}` amount to pay in rupees
- **Buttons:** none
- Prepaid orders: use a version without the cash line, or skip this template.

**Urdu**
```
السلام علیکم {{1}}، آپ کا آرڈر {{2}} آج ڈیلیوری کے لیے نکل چکا ہے۔ براہِ کرم {{3}} روپے نقد تیار رکھیں اور اپنا فون آن رکھیں تاکہ رائیڈر آپ سے رابطہ کر سکے۔ شکریہ۔
```

**Roman Urdu**
```
Assalam o Alaikum {{1}}, aap ka order {{2}} aaj delivery ke liye nikal chuka hai. Barah-e-karam Rs {{3}} cash tayyar rakhein aur apna phone on rakhein taake rider aap se rabta kar sake. Shukriya.
```

**English**
```
Hello {{1}}, your order {{2}} is out for delivery today. Please keep Rs {{3}} in cash ready and keep your phone on so the rider can reach you. Thank you.
```

---

## 7. delivery_failed_reattempt

- **Category:** Utility
- **When:** courier status = failed delivery attempt
- **Variables:** `{{1}}` customer first name; `{{2}}` order number
- **Buttons:** three quick replies (deliver again, change address, cancel order)
- "Change address" and "Cancel order" replies go to a human; the agent does not change the booking itself.

**Urdu**
```
السلام علیکم {{1}}، کورئیر نے آپ کا آرڈر {{2}} ڈیلیور کرنے کی کوشش کی لیکن آپ سے رابطہ نہیں ہو سکا۔ ہم دوبارہ کوشش کرنا چاہتے ہیں۔ براہِ کرم نیچے سے ایک آپشن منتخب کریں۔
```
Buttons: `دوبارہ ڈیلیور کریں` | `ایڈریس تبدیل کریں` | `آرڈر کینسل کریں`

**Roman Urdu**
```
Assalam o Alaikum {{1}}, courier ne aap ka order {{2}} deliver karne ki koshish ki lekin aap se rabta nahi ho saka. Hum dobara koshish karna chahte hain. Barah-e-karam neeche se aik option chunein.
```
Buttons: `Dobara deliver karein` | `Address change karein` | `Order cancel karein`

**English**
```
Hello {{1}}, the courier tried to deliver your order {{2}} but could not reach you. We would like to try again. Please choose an option below.
```
Buttons: `Deliver again` | `Change address` | `Cancel order`

---

## 8. prepaid_discount_offer

- **Category:** Marketing
- **When:** campaign to opted-in customers only, after owner approval. Not part of the automatic order flow.
- **Variables:** `{{1}}` customer first name; `{{2}}` store name; `{{3}}` prepaid discount as text, for example a percentage or a rupee amount (from Airtable `KPI Targets & Caps`, approved by the client)
- **Buttons:** URL button to `{{store_url}}`, plus a quick reply to stop offers. Check current Meta policy for allowed button combinations.
- Name the payment methods (JazzCash, EasyPaisa, cards) only after the client's aggregator is live and the methods are confirmed.
- A customer who taps the stop button is removed from marketing sends and logged.

**Urdu**
```
السلام علیکم {{1}}، {{2}} پر اپنے اگلے آرڈر کی آن لائن ادائیگی کریں اور {{3}} کی بچت حاصل کریں۔ ڈیلیوری کے وقت نقد رقم کی ضرورت نہیں۔ آرڈر کرنے کے لیے نیچے بٹن دبائیں۔
```
Buttons: `ابھی آرڈر کریں` (URL) | `آفرز بند کریں` (quick reply)

**Roman Urdu**
```
Assalam o Alaikum {{1}}, {{2}} par apne agle order ki online payment karein aur {{3}} ki bachat hasil karein. Delivery ke waqt cash ki zaroorat nahi. Order karne ke liye neeche button dabayein.
```
Buttons: `Abhi order karein` (URL) | `Offers band karein` (quick reply)

**English**
```
Hello {{1}}, pay online for your next order at {{2}} and save {{3}}. No cash needed at the door. Tap the button below to order.
```
Buttons: `Order now` (URL) | `Stop offers` (quick reply)

---

## 9. support_first_reply

- **Category:** Utility
- **When:** first reply to a customer's support message. Inside the 24-hour window this can also be sent as a normal free-form message; the template is for cases outside the window.
- **Variables:** `{{1}}` customer first name; `{{2}}` store name
- **Buttons:** none
- Do not promise a reply time unless it is in Airtable `Policies & SOPs`.

**Urdu**
```
السلام علیکم {{1}}، {{2}} سے رابطہ کرنے کا شکریہ۔ آپ کا میسج ہمیں مل گیا ہے۔ اگر ضرورت ہوئی تو ہماری ٹیم کا ایک رکن اسی چیٹ میں آپ کو جواب دے گا۔
```

**Roman Urdu**
```
Assalam o Alaikum {{1}}, {{2}} se rabta karne ka shukriya. Aap ka message humein mil gaya hai. Agar zaroorat hui to hamari team ka aik member isi chat mein aap ko jawab dega.
```

**English**
```
Hello {{1}}, thank you for contacting {{2}}. We have received your message. If needed, a member of our team will reply to you in this chat.
```

---

## Submission checklist

- [ ] Urdu versions reviewed by a native Urdu reader before submission (these are drafts).
- [ ] Store name, greeting and tone match Airtable `Brand`.
- [ ] Each template submitted once per language, with a sample value for every variable.
- [ ] Categories match the list above; no promotion inside Utility templates.
- [ ] Approved template names and languages recorded in the client profile.
- [ ] Rejected template: read Meta's reason, edit, resubmit. Do not send a look-alike free-form message outside the 24-hour window.
- [ ] Test send to an internal opted-in number in all three languages before go-live.

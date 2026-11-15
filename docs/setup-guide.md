# Setup guide

About 45–60 minutes the first time, most of it creating accounts. Use a laptop: the n8n editor is hard to use on a phone. n8n's menus change between versions, so if a label differs slightly, look for the nearest match.

## What you need
| Account | Used for | Cost to try |
|---|---|---|
| n8n Cloud (or self-hosted n8n 2.x) | Runs the workflows | 14-day free trial |
| Anthropic | Claude reads customer messages | Pay as you go (small amounts per message) |
| Gmail (or any SMTP mailbox) | Email replies | Free |
| Meta for Developers | WhatsApp Cloud API: customer replies and owner alerts | Free test number |

## 1. Import the six workflows
1. In n8n, open **Overview** and click **Create workflow**.
2. In the empty editor, open the **⋯** menu (top right) → **Import from URL…**
3. Paste the raw link of the first file, for example
   `https://raw.githubusercontent.com/costasxeras-stack/Garage-quote-agent/main/workflows/00-setup.json`
   (the repo must be public; otherwise download the file and use **Import from File…**).
4. Click **Save** (top right). You should see the workflow with its yellow notes.
5. Repeat for `01-…`, `02-…`, `03-…`, `04-…` and `99-…`.

✅ Overview lists six workflows starting with **Garage Quote Agent ·**

## 2. Create the data tables
1. Open **Garage Quote Agent · 00 Setup (run once)**.
2. Click **Execute workflow**.
3. Every node turns green. Under **Overview → Data tables** you now see `garage_settings`, `garage_price_book`, `garage_leads` and `garage_events`.

## 3. Add the credentials
Open each node listed below, click **Credential to connect with → Create new credential**, fill it in, then **Save**.

### Claude (workflow 01, node **Claude**)
1. Go to console.anthropic.com → **API keys** → **Create key**. Copy it.
2. In n8n paste it into **API Key**. Leave Base URL as is.

### Email (nodes **Reply by email**, **Remind by email**)
For Gmail: Google Account → **Security** → turn on **2-Step Verification** → **App passwords** → create one called n8n.
In n8n create an **SMTP** credential: User = your Gmail address, Password = the app password, Host = `smtp.gmail.com`, Port = `465`, SSL/TLS = on.

### WhatsApp (trigger **WhatsApp message**, and every node that sends a WhatsApp message to customers or the owner)
1. Go to developers.facebook.com → **My Apps → Create app** → choose the **Business** type → add the **WhatsApp** product.
2. Open **WhatsApp → API Setup**. Note the **Phone number ID** and **WhatsApp Business Account ID**, and copy the **temporary access token** (it expires after 24 hours; create a permanent system-user token later).
3. Under **To**, add the owner's phone number (and any test customer numbers) as test recipients and confirm the codes.
4. In n8n, **Overview → Credentials → Create credential → WhatsApp API**: Access Token and Business Account ID. Then pick this credential in every WhatsApp node.
5. Open **App settings → Basic** and copy the **App ID** and **App Secret**.
6. In n8n, **WhatsApp message** (the trigger) → new **WhatsApp OAuth API** credential (the trigger's credential): Client ID = App ID, Client Secret = App Secret.

Meta allows one WhatsApp trigger per Meta app.

**Keep the owner's window open:** WhatsApp only lets the garage number message the owner within 24 hours of the owner's last message to it. The owner should send any short message (e.g. "hi") to the garage number once a day. The workflow ignores these messages.

## 4. Fill in your settings
Open **Overview → Data tables → garage_settings** and replace every [bracketed] value:

| Column | What to put |
|---|---|
| garage_name, garage_phone | Shown to customers |
| labour_rate_eur, vat_rate | Your hourly rate and VAT % |
| confidence_threshold | 0.75 to start; higher sends more requests to you |
| premium_brands, premium_multiplier | Brands that cost more to work on, and by how much |
| owner_whatsapp_number | The owner's mobile in international format, e.g. +30 69… |
| from_email | The Gmail address from the email step |
| booking_form_url | Leave for now, filled in step 6 |
| whatsapp_phone_number_id | From WhatsApp step 2 |
| followup_hours, final_followup_days | When reminders go out (WhatsApp reminders always fall inside 24 hours) |

Then open **garage_price_book** and replace the sample prices with yours. Set `auto_quote` to false for any job you always want to price yourself.

## 5. Publish
Publish in this order (button **Publish**, top right of each workflow):
1. **99 Error alerts**
2. **01**, **02**, **03**, **04**

Then in each of 01–04: **⋯ → Settings → Error workflow → Garage Quote Agent · 99 Error alerts → Save**.

## 6. Connect the booking form
1. Open **02 Booking requests** → double-click **Booking form** → choose the **Production URL** tab and copy it.
2. Paste it into `booking_form_url` in **garage_settings**.

## 7. Try it
1. Open **01** → double-click **Web form** → **Production URL** → open it in a browser and send a request for a routine job, for example front brake pads on a car you know.
   ✅ An email estimate arrives, and the owner's WhatsApp shows "Estimate sent automatically…"
2. Send a vague one ("strange noise").
   ✅ The owner's WhatsApp shows "New quote request needs your decision" with a **Decide** link.
3. From your phone, send a WhatsApp message to the Meta test number.
   ✅ You get an estimate back on WhatsApp.
4. Check **Data tables → garage_leads**: every request is a row with its status.

## Troubleshooting
- **No reply at all:** open the workflow → **Executions** and click the latest run; the red node shows the error.
- **Owner gets nothing on WhatsApp:** the owner has not messaged the garage number in the last 24 hours, or owner_whatsapp_number is wrong.
- **WhatsApp error 131030 (recipient not allowed):** add the number under **To** in API Setup.
- **WhatsApp stopped after a day:** the temporary token expired.

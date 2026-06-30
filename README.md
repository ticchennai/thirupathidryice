# Thirupathi Dry Ice — Order Portal

A single-page ordering site for **Thirupathi Dry Ice**, built to run on a subdomain (e.g. `order.thirupathiicecream.in`) alongside the main site at [dryice.thirupathiicecream.in](https://dryice.thirupathiicecream.in/).

Customers pick a quantity in kg, see the live total at ₹50/kg, fill in their details, and place the order directly over WhatsApp — no backend, no database, no app required.

---

## What's inside

This is a **single static file**: `index.html`. All CSS and JavaScript are embedded — no build step, no dependencies, no npm install.

| Feature | Details |
|---|---|
| **Order form** | Quantity stepper (+ / − and 1 / 5 / 10 kg presets), name, phone, optional email, mandatory delivery address, optional notes |
| **Live pricing** | Fixed rate of ₹50/kg, calculated automatically |
| **Unique order ID** | Auto-generated sequence starting at `T-0001`, incrementing on every order sent |
| **WhatsApp checkout** | "Send Order on WhatsApp" opens `wa.me/919840578832` with a pre-filled message containing the order ID, quantity, total, and customer details |
| **Floating WhatsApp button** | Sticky button on every screen for quick chat access |
| **Pickup address card** | Displays the pickup location with an embedded Google Map and a "Get Directions" link |
| **Google review CTA** | One-tap link to the business's Google review page |
| **Social links** | Facebook, Twitter/X, Instagram, Pinterest, YouTube, LinkedIn — matching the main site |
| **SEO content** | "About Dry Ice" section, areas-served pills, FAQ accordion, meta tags, Open Graph tags, and JSON-LD structured data (`Product`, `LocalBusiness`, `FAQPage`) |

---

## File structure

```
index.html   ← everything: markup, styles, and scripts in one file
README.md    ← this file
```

---

## Local preview

No build tools needed. Just open the file in a browser:

```bash
open index.html        # macOS
start index.html        # Windows
xdg-open index.html     # Linux
```

Or serve it locally to test things like the Google Map embed and WhatsApp links properly:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Deploying to a subdomain

1. Upload `index.html` to your hosting provider (or a static host like Netlify, Vercel, GitHub Pages, or your existing cPanel/Hostinger account).
2. Point a **CNAME or A record** for `order.thirupathiicecream.in` (or whatever subdomain you choose) at that hosting location.
3. Make sure the file is served as `index.html` at the domain root.
4. Once live, update the canonical URL and Open Graph `url` tags in the `<head>` if your final subdomain differs from `order.thirupathiicecream.in` (see **Things to update before going live** below).

---

## Things to update before going live

Search for these in `index.html` and adjust if needed:

- **Canonical / OG URLs** — currently set to `https://order.thirupathiicecream.in/`. Update if you use a different subdomain.
- **WhatsApp number** — `919840578832` appears in the floating button, the order button, and the `tel:` links. Update in all places if the number changes.
- **Google review link** — `https://share.google/bbP0p43OMmSTd7BxZ`.
- **Pickup address & map** — the map uses a text search for `Thirupathi Dry Ice` on Google Maps (`https://www.google.com/maps?q=Thirupathi+Dry+Ice&output=embed`), so it will continue to work as long as that business listing exists and stays accurate.
- **Price per kg** — set in the JavaScript as `const RATE = 50;` near the bottom of the file. Change this single value to update pricing everywhere (price tag, calculations, WhatsApp message).

---

## How the order ID works

- The first order from a browser is `T-0001`. Each subsequent order sent from that same browser increments the number (`T-0002`, `T-0003`, ...).
- The counter is stored in the browser's `localStorage`, so it's **per-device**, not a single global counter shared across all customers. If you need one continuous sequence across every customer (e.g. for accounting), you'll need a small backend — a free option is a Google Sheet + Apps Script webhook that assigns and logs each order ID server-side. Let me know if you'd like this built.

---

## Notes on WhatsApp ordering

- The "Send Order on WhatsApp" button requires the customer to have WhatsApp installed (mobile) or WhatsApp Web set up (desktop), since it relies on the standard `wa.me` deep link.
- The delivery address field is required before the button will proceed; email is optional.

---

## Credits

Developed by [Ramesh Kumar P & Co](https://publisher.rameshkumarp.in/) for Thirupathi Dry Ice.

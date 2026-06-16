# Hybrid Dental Clinic — Website Preview

A mobile-first, production-ready **demo/preview** site for **Hybrid Dental Clinic, Lagos**.
Patients pick a treatment and book by **form or WhatsApp** — no long back-and-forth DMs.

Pure **HTML + CSS + vanilla JS**. No framework, no build step, no dependencies.

Suggested live route/slug: **`/prime-dental-clinic-lagos`**

---

## ▶️ Run it locally

It's a static site — just open `index.html` in a browser. For correct behaviour
(WhatsApp links, map, fonts) serve it over HTTP:

```bash
# from inside the "site" folder — pick ONE:

# Python (most machines already have it)
python -m http.server 8000
#   then open  http://localhost:8000

# Node
npx serve .

# VS Code: install the "Live Server" extension → right-click index.html → "Open with Live Server"
```

## 🏗️ Build command

**None.** There is no build step — the files in this folder *are* the site.
To deploy, upload the whole `site/` folder to any static host
(Netlify, Vercel, GitHub Pages, cPanel, etc.). For the suggested slug, serve it at
`/prime-dental-clinic-lagos`.

---

## 📁 Structure

```
site/
├── index.html             Landing page (all sections)
├── book-appointment.html  4-step booking flow + WhatsApp option
├── css/style.css          Design system (brand colours at the top in :root)
├── js/main.js             Nav, reveal, booking engine, WhatsApp link builder
└── assets/
    ├── logo.jpg           Brand logo (header + footer + favicon)
    ├── gallery/           Smile-gallery images
    └── video/             Patient video clip
```

---

## ✏️ What to edit before going live (easy stuff first)

| What | Where |
|------|-------|
| **WhatsApp number** | `js/main.js` → top of file → `window.HDC.WHATSAPP` (format `2348031234567`, no `+`/spaces). Every WhatsApp button uses this one value. |
| **Phone number** | Find/replace `+2348000000000` and `+234 800 000 0000` across both `.html` files |
| **Address / map** | Search `109 Akowonjo Road` in both HTML files; update the `<iframe>` map `src` in `index.html` (Google Maps → Share → Embed) |
| **Opening hours** | The top bar, the `#location` section, and the footer `.footer__hours` |
| **Prices** | `#pricing` table + each `.treatment-card__price` in `index.html`, and the option tiles in `book-appointment.html` |
| **Doctor names** | Step 2 of `book-appointment.html` (`Dr. Adaeze Okafor`, etc.) |
| **HMO details** | `#pricing` callout text in `index.html` |
| **Logo** | Replace `assets/logo.jpg`. A **transparent PNG** is ideal — it removes the small white tile behind the mark. Keep the same filename or update the `<img class="brand-mark">` / favicon `src` |
| **Smile gallery photos** | Replace files in `assets/gallery/` (real before/after — get patient consent). The last tile is an "add your photo" placeholder |
| **Patient video** | Replace `assets/video/patient-testimonial.mp4` |
| **Reviews** | `#reviews` section in `index.html` |
| **Brand colours** | `css/style.css` → `:root` → `--color-primary` (blue) and `--color-accent` (teal), derived from the logo |
| **SEO / domain** | `<title>`, `<meta name="description">`, `<link rel="canonical">`, and the JSON-LD block in `index.html` |

---

## 💬 How WhatsApp booking works

- Set the number once in `js/main.js` (`window.HDC.WHATSAPP`).
- Any link with `data-wa` becomes a WhatsApp link.
  - `data-wa-service="Teeth Whitening"` → auto-builds a booking message for that treatment.
  - `data-wa-msg="...custom..."` → sends your exact message.
- On the booking page, completing the form builds a **pre-filled summary** message;
  the success screen's **“Send on WhatsApp”** button opens the chat with all details ready.

> The form itself is front-end only (it simulates submission). To store bookings or
> send email/SMS, POST the `state` object in `initBooking()` (`js/main.js`) to your backend.

---

## 📱 Responsive

Mobile-first. Includes a sticky bottom action bar (Call · WhatsApp · Book) on phones,
a floating WhatsApp button, an overlay menu, and a compact bold logo lockup.
Breakpoints: 1024px (tablet), 768px (mobile), 480px (small).

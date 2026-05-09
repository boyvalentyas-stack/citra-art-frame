# 🖼️ Citra Art Frame — Business Website

A bilingual (English / Indonesian) static business website built with HTML, CSS, and Vanilla JavaScript, hosted for free on GitHub Pages. Built by a son to help his father's custom photo frame business reach customers online.

🌐 **Live site:** [boyvalentyas-stack.github.io/citra-art-frame](https://boyvalentyas-stack.github.io/citra-art-frame)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Structure](#project-structure)
- [Technology Stack](#technology-stack)
- [Design System](#design-system)
- [Pages](#pages)
  - [index.html — Company Profile](#indexhtml--company-profile)
  - [get-yours.html — Price Calculator](#get-yourshtml--price-calculator)
- [Bilingual System (i18n)](#bilingual-system-i18n)
- [Price Calculation Logic](#price-calculation-logic)
- [SEO & Metadata](#seo--metadata)
- [Responsive Behavior](#responsive-behavior)
- [Business Information](#business-information)
- [Deployment Guide](#deployment-guide)
- [Maintenance Guide](#maintenance-guide)
- [Known Limitations](#known-limitations)
- [Changelog](#changelog)

---

## Project Overview

Citra Art Frame is a custom photo frame workshop established in **1993**, based in **Rawamangun, Jakarta Timur**. This website is the business's digital presence and consists of two pages:

1. **Company profile page** (`index.html`) — business story, statistics, workshop location with embedded Google Maps, and contact information.
2. **Price calculator page** (`get-yours.html`) — a live interactive estimator where customers select frame dimensions, glass type, and frame material, receive an instant price breakdown, and send their order directly via a pre-filled WhatsApp message.

The entire site is built without any framework, build tool, or backend. All logic runs in the browser using plain JavaScript.

---

## Project Structure

```
citra-art-frame/
│
├── index.html              ← Company profile page
├── get-yours.html          ← Live price calculator page
├── citra-art-favicon.ico   ← Browser tab icon (used on both pages)
└── README.md               ← This file
```

Both HTML files are self-contained — all CSS and JavaScript are embedded inside each file. There are no external stylesheets, no JavaScript modules, and no dependency manifests beyond Google Fonts.

---

## Technology Stack

| Layer | Technology | Notes |
|---|---|---|
| Markup | HTML5 | Two standalone files |
| Styling | CSS3 | Embedded `<style>` block; CSS custom properties for design tokens |
| Scripting | Vanilla JavaScript | Embedded `<script>` block; no libraries |
| Fonts | Google Fonts | Playfair Display + DM Sans; loaded with `preconnect` |
| Maps | Google Maps Embed API | `<iframe>` pointed at actual workshop coordinates |
| Hosting | GitHub Pages | Free static hosting; auto-deploys on push to `main` |
| Version Control | Git / GitHub | Managed via GitHub web interface |
| Favicon | `.ico` | `citra-art-favicon.ico`; present on both pages |

---

## Design System

All design tokens are defined identically in the `:root` block on both files.

### Color Palette

| Variable | Value | Usage |
|---|---|---|
| `--cream` | `#F5F0E8` | Section backgrounds, input backgrounds, lang toggle |
| `--warm-white` | `#FDFAF5` | Page body, hero left panel, about section, form inputs |
| `--gold` | `#C9A84C` | Primary accent — CTA buttons, dividers, radio highlight, stats |
| `--dark` | `#1A1410` | `get-yours.html` hero, contact section, result card |
| `--brown` | `#4A3728` | Nav logo, primary buttons, active lang button, frame illustration |
| `--brown-light` | `#7A5C48` | Form field labels |
| `--text` | `#2C2018` | Primary body text |
| `--text-muted` | `#8A7060` | Secondary text, nav links, descriptions, radio labels |
| `--border` | `#E0D5C5` | All borders — cards, inputs, nav, dividers |

### Typography

| Font | Family | Usage |
|---|---|---|
| Playfair Display | Serif | All headings, nav logo, frame quote, stat numbers, result price |
| DM Sans | Sans-serif | All body text, nav links, form labels, inputs, buttons |

---

## Pages

### index.html — Company Profile

**Navigation Bar** — Fixed. Contains brand logo, nav links (About, Location, Contact, Get Yours CTA), EN/ID language toggle, and a hamburger menu for mobile.

**Hero Section** — Full-viewport two-column grid. Left column: headline, description, two CTA buttons. Right column: CSS-drawn frame illustration with an italic quote and a circular badge showing `30+ Years of craft`.

**About Section (`#about`)** — Two-column grid. Left: placeholder for a business photo with a gold accent stamp. Right: three body paragraphs and four statistics.

| Statistic | Value |
|---|---|
| Frames crafted | 1,000,000+ |
| Years experience | 30+ |
| Frame materials | 3 |
| Custom made | 100% |

**Location Section (`#location`)** — Two-column grid. Left: workshop address, phone, WhatsApp, and opening hours. Right: live Google Maps `<iframe>` pointed at the actual Citra Art pin in Rawamangun, with an "Open in Google Maps" button linking directly to the business pin coordinates.

**Contact Section (`#contact`)** — Three-column grid of contact cards for WhatsApp, Email, and Instagram. Each card has an icon, channel label, linked value, and a short descriptor. Below: copyright line and a CTA link to the calculator page.

**Footer** — Credit strip with links to GitHub Pages and Claude.AI.

---

### get-yours.html — Price Calculator

**Navigation Bar** — Fixed. Brand logo (links to `index.html`), "← Back to Home" link, and EN/ID language toggle.

**Page Hero** — Dark banner with page title and description.

**Main Content** — Two-column layout (collapses to single column on tablet and mobile).

**Left: Configuration Form**

| Field | Type | Behavior |
|---|---|---|
| Customer Name | Text input | Updates order summary live; `autocomplete="given-name"` |
| Horizontal / Width | Number (cm, step 0.1) | Triggers recalculation on every keystroke |
| Vertical / Height | Number (cm, step 0.1) | Triggers recalculation on every keystroke |
| Glass Type | Radio group (3 options) | Triggers recalculation on change |
| Frame Material | Radio group (3 options) | Triggers recalculation on change |

**Right: Result Card**

Updates live on every input change. Displays:
- Customer name (prefixed with "for" in EN, "untuk" in ID)
- Estimated total price (grayed when zero)
- Disclaimer: "Starting from · excl. delivery"
- Price breakdown: Frame cost, Back cover, Front cover / Glass
- Order summary: Customer, Size, Glass, Frame
- WhatsApp button with pre-filled message (language-aware)

---

## Bilingual System (i18n)

Both pages implement a custom lightweight i18n system using `data-i18n` HTML attributes and a JavaScript translation object. No external library is used.

### How It Works

Every translatable element carries a `data-i18n` attribute with a key:

```html
<h1 class="hero-title" data-i18n="hero.title">Your Memories,<br><em>Beautifully</em><br>Preserved.</h1>
```

All strings are stored in a `const i18n` object with two top-level keys — `en` and `id`. The `setLang(lang)` function iterates all `[data-i18n]` elements and sets their `innerHTML`. Input placeholders use `data-i18n-placeholder` and are updated via `el.placeholder`.

### Language Persistence

| Storage | Key | Purpose |
|---|---|---|
| `localStorage` | `caf-lang` | Persists across browser sessions |
| `sessionStorage` | `caf-lang` | Passes language from `index.html` to `get-yours.html` within the same tab |

### Translation Keys — index.html

`nav.about` · `nav.location` · `nav.contact` · `nav.cta` · `hero.tag` · `hero.title` · `hero.desc` · `hero.btn1` · `hero.btn2` · `hero.quote` · `hero.badge` · `about.tag` · `about.title` · `about.accent` · `about.p1` · `about.p2` · `about.p3` · `about.stat1` · `about.stat2` · `about.stat3` · `about.stat4` · `location.tag` · `location.title` · `location.desc` · `location.address` · `location.mapBtn` · `contact.tag` · `contact.title` · `contact.waNote` · `contact.emailNote` · `contact.igNote` · `contact.copy` · `contact.cta` · `footer.built` · `footer.link`

### Translation Keys — get-yours.html

`nav.back` · `hero.tag` · `hero.title` · `hero.desc` · `form.badge` · `form.title` · `form.subtitle` · `form.nameLabel` · `form.namePlaceholder` · `form.sizeLabel` · `form.widthLabel` · `form.heightLabel` · `form.glassLabel` · `form.frameLabel` · `glass.none` · `glass.none.price` · `glass.clear` · `glass.doff` · `frame.fiber` · `frame.wood` · `frame.aluminium` · `result.title` · `result.priceLabel` · `result.priceNote` · `result.frameCost` · `result.backCover` · `result.frontCover` · `summary.title` · `summary.customer` · `summary.notFilled` · `summary.size` · `summary.glass` · `summary.frame` · `wa.btn` · `wa.note`

JS-only keys (not bound to DOM elements): `js.forName` · `js.glass.none` · `js.glass.clear` · `js.glass.doff` · `js.frame.fiber` · `js.frame.wood` · `js.frame.aluminium` · `js.summaryFiber` · `js.summaryWood` · `js.summaryAluminium` · `js.notFilled` · `js.waMsg`

---

## Price Calculation Logic

All pricing is calculated in real time inside the `calculate()` function. Prices are stored in a single `PRICES` constant at the top of the `<script>` block — the only place to edit when prices change.

### Price Configuration (current values)

```javascript
const PRICES = {
  backCover: 85000,          // IDR per m² — fixed for all orders
  glass: {
    none:       0,           // IDR per m²
    clear:  150000,          // IDR per m²
    doff:   200000,          // IDR per m²
  },
  frame: {
    fiber:   35000,          // IDR per meter (starting price)
    wood:    75000,          // IDR per meter (starting price)
    aluminium: 250000,       // IDR per meter (starting price)
  }
};
```

### Formula

All dimensions entered in centimeters are converted to meters (`÷ 100`) before calculation.

```
Frame price  = ((2 × width_m) + (2 × height_m) + 0.21) × frame_price_per_meter
Back cover   = width_m × height_m × 85,000
Front cover  = width_m × height_m × glass_price_per_m²
─────────────────────────────────────────────────────────────────────────────────
Total price  = Frame price + Back cover + Front cover
```

The `0.21` coefficient accounts for corner joining material consumed during frame assembly.

### Zero-Value Guard

If either width or height is empty, zero, or non-numeric, the total is forced to `Rp 0` and all breakdown values show zero. Selecting "No Glass" sets the glass component to zero without affecting the rest of the formula.

### WhatsApp Message Template

**English:**
> Hello Citra Art Frame, My name is {name} and I see your estimation of my photo frame with the size {width} cm long and {height} cm wide, with {glass_type}, and a {frame_type} starting from {total_price}.

**Indonesian:**
> Halo Citra Art Frame, nama saya {name} dan saya melihat estimasi harga bingkai foto saya dengan ukuran {width} cm lebar dan {height} cm tinggi, dengan {glass_type}, dan bingkai {frame_type} mulai dari {total_price}.

---

## SEO & Metadata

### index.html

| Tag | Value |
|---|---|
| `<title>` | Citra Art Frame – Custom Photo Frames Jakarta |
| `<meta name="description">` | Citra Art Frame — Handcrafted custom photo frames since 1993. Based in Rawamangun, Jakarta Timur. Choose your material, glass, and size. Get an instant price estimate online. |
| `<meta name="author">` | Citra Art Frame |
| `<meta name="robots">` | index, follow |
| `<link rel="canonical">` | https://boyvalentyas-stack.github.io/citra-art-frame/ |
| `og:title` | Citra Art Frame – Custom Photo Frames Jakarta |
| `og:description` | Handcrafted custom photo frames since 1993. Rawamangun, Jakarta Timur. Order online and get an instant price estimate. |
| `og:url` | https://boyvalentyas-stack.github.io/citra-art-frame/ |
| `og:type` | website |
| `og:locale` | id_ID |
| `og:locale:alternate` | en_US |

### get-yours.html

| Tag | Value |
|---|---|
| `<title>` | Get Yours – Citra Art Frame \| Custom Frame Price Estimator |
| `<meta name="description">` | Calculate the price of your custom photo frame instantly. Choose size, glass type, and frame material. Order via WhatsApp — Citra Art Frame, Jakarta. |
| `<meta name="robots">` | index, follow |
| `<link rel="canonical">` | https://boyvalentyas-stack.github.io/citra-art-frame/get-yours.html |
| `og:title` | Get Yours – Citra Art Frame \| Custom Frame Price Estimator |
| `og:description` | Calculate your custom photo frame price instantly. Choose size, glass, and material. Order via WhatsApp. |

---

## Responsive Behavior

### index.html

| Breakpoint | Changes |
|---|---|
| Desktop (> 900px) | Two-column hero; two-column about; side-by-side location; three-column contact; full nav visible |
| Tablet (≤ 900px) | Single-column hero; single-column about; single-column location; two-column contact; nav links compressed |
| Mobile (≤ 600px) | Nav links hidden, hamburger menu shown; hero buttons stack vertically; about accent card goes static; contact grid single column |

### get-yours.html

| Breakpoint | Changes |
|---|---|
| Desktop (> 800px) | Two-column layout; result card is `position: sticky` at `top: 100px` |
| Tablet (≤ 800px) | Single-column layout; result card becomes static; reduced padding |
| Mobile (≤ 600px) | Tighter padding on all elements; reduced font sizes on nav, hero, form, and result card |

---

## Business Information

| Field | Value |
|---|---|
| Business name | Citra Art Frame |
| Established | 1993 |
| Address | Jl. Balap Sepeda Raya No. 14, Kelurahan Rawamangun, Kecamatan Pulogadung, Kota Jakarta Timur, DKI Jakarta, Indonesia 13220 |
| Phone | (021) 4756820 |
| WhatsApp | +62 877-8291-3323 |
| WhatsApp link number | `6287782913323` |
| Email | dev.boyvalentyas@gmail.com |
| Instagram | @aceblanc.toujo |
| Opening hours | Monday – Saturday, 09.00 – 17.30 WIB |
| Closed | Sundays and Public Holidays |
| Google Maps pin | Citra Art, Rawamangun, Jakarta Timur |
| Google Maps link | https://www.google.com/maps/place/Citra+Art/@-6.1891296,106.8921970,17z |

---

## Deployment Guide

Hosted on GitHub Pages from the `main` branch root. No build step required.

### Prerequisites
- GitHub account with a repository named `citra-art-frame` under `boyvalentyas-stack`
- GitHub Pages enabled: **Settings → Pages → Source: Deploy from branch → main → / (root)**

### Deploying a Change (via GitHub web interface)
1. Navigate to the repository on GitHub.
2. Click the file to edit → pencil icon.
3. Make changes.
4. Click **Commit changes**.
5. Wait 1–3 minutes. Monitor under the **Actions** tab — green ✅ means live.
6. Verify at `https://boyvalentyas-stack.github.io/citra-art-frame`.

---

## Maintenance Guide

### Update Prices

Open `get-yours.html` and find the `PRICES` constant near the top of the `<script>` block. Edit only the numeric values:

```javascript
const PRICES = {
  backCover: 85000,      // ← edit this
  glass: {
    none: 0,
    clear: 150000,       // ← edit this
    doff: 200000,        // ← edit this
  },
  frame: {
    fiber: 35000,        // ← edit this
    wood: 75000,         // ← edit this
    aluminium: 250000,   // ← edit this
  }
};
```

> ⚠️ The price range labels on each radio button (e.g., `"Starting from Rp 35.000/m ~ 165.000/m"`) are **static HTML text** and must also be updated manually — they are not driven by the `PRICES` constant.

### Update Contact Information

Contact details appear in two places in `index.html`: the HTML anchor tags and the i18n translation strings. Both must be updated when contact information changes.

**HTML anchor tags** — find and update in the contact section:
```html
<a href="https://wa.me/6287782913323">...</a>
<a href="mailto:dev.boyvalentyas@gmail.com">...</a>
<a href="https://instagram.com/aceblanc.toujo">...</a>
```

**i18n strings** — update `location.address` in both `en` and `id` objects inside the `<script>` block.

**In `get-yours.html`** — update the `WA_NUMBER` constant:
```javascript
const WA_NUMBER = '6287782913323'; // ← update this (no + or spaces)
```

### Update Google Maps Embed

1. Go to [maps.google.com](https://maps.google.com) and search for the address.
2. Click **Share → Embed a map → Copy HTML**.
3. Replace the `src` attribute of the `<iframe>` in `index.html`.
4. Also update the `href` of the `.map-overlay-btn` anchor to the new location link.

### Add a Translation Key

1. Add `data-i18n="your.key"` to the HTML element.
2. Add `'your.key': 'English text'` to the `en` object in the `i18n` constant.
3. Add `'your.key': 'Indonesian text'` to the `id` object in the `i18n` constant.

---

## Known Limitations

| Limitation | Detail |
|---|---|
| Prices are estimates only | The calculator uses fixed starting prices. Actual prices vary by frame profile, glass quality, and order quantity. Final price is confirmed by the business on order. |
| Radio button price labels are static | The range text shown on each radio option (e.g., `"Starting from Rp 35.000/m ~ 165.000/m"`) is hardcoded HTML. It must be updated manually when prices change — it is not driven by the `PRICES` constant. |
| About section photo is a placeholder | The about section image uses a CSS placeholder with a 🖼️ emoji. No actual business photo has been added. |
| Page title not translated | The `<title>` tag is hardcoded in English on both pages. It is not part of the i18n system and does not change when the language is switched to Indonesian. |
| No offline support | No service worker or caching strategy. The site is not available offline. |

---

## Changelog

| Version | Date | Changes |
|---|---|---|
| 1.1 | May 2026 | SEO pass on both pages: added `<meta name="description">`, `<meta name="author">`, `<meta name="robots">`, `<link rel="canonical">`, full Open Graph tags, and `<link rel="preconnect">` for Google Fonts. Fixed `Keluarahan` → `Kelurahan` and `Pulo Gadung` → `Pulogadung` typos in EN and ID i18n address strings. Fixed Google Maps overlay button `href` from generic `?q=Jakarta` to actual Citra Art pin coordinates. Added `title` attributes to all contact links and the Google Maps `<iframe>`. Added `autocomplete="given-name"` to name input. Added missing favicon `<link>` to `get-yours.html`. Fixed `IntersectionObserver` memory leak by adding `observer.unobserve(e.target)`. Fixed wooden frame price label typo `365.0000` → `365.000`. |
| 1.0 | Apr 2026 | Initial release: bilingual company profile, live price calculator with WhatsApp integration, embedded Google Maps, hamburger mobile menu, EN/ID language toggle with localStorage + sessionStorage persistence. |

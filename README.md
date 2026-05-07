# 🖼️ Citra Art Frame — Business Website

A bilingual (English / Indonesian) static business website built with HTML, CSS, and Vanilla JavaScript, hosted for free on GitHub Pages. Built by a son to help his father's custom photo frame business reach customers online.

🌐 **Live site:** [boyvalentyas-stack.github.io/citra-art-frame](https://boyvalentyas-stack.github.io/citra-art-frame)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Structure](#project-structure)
- [Pages](#pages)
  - [index.html — Company Profile](#indexhtml--company-profile)
  - [get-yours.html — Price Calculator](#get-yourshtml--price-calculator)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Design System](#design-system)
- [Bilingual System (i18n)](#bilingual-system-i18n)
- [Price Calculation Logic](#price-calculation-logic)
- [Responsive Behavior](#responsive-behavior)
- [Business Information](#business-information)
- [Maintenance Guide](#maintenance-guide)
- [Known Limitations](#known-limitations)

---

## Project Overview

Citra Art Frame is a custom photo frame workshop based in Jakarta Timur, Indonesia, established in 1993. This website serves as the business's digital presence and consists of two pages:

1. A **company profile page** (`index.html`) that presents the business story, workshop location with an embedded Google Maps widget, and contact information.
2. A **live price calculator page** (`get-yours.html`) that allows potential customers to select frame dimensions, glass type, and frame material, then receive an instant price estimate and send it directly to the business via WhatsApp.

The entire website is built without any framework, build tool, or backend. All logic runs in the browser using plain JavaScript.

---

## Project Structure

```
citra-art-frame/
│
├── index.html              ← Company profile page (Page 1)
├── get-yours.html          ← Live price calculator page (Page 2)
├── citra-art-favicon.ico   ← Browser tab icon (referenced in index.html)
└── README.md               ← This file
```

Both HTML files are self-contained — all CSS styles and JavaScript are embedded directly inside each file. There are no external stylesheets, no JavaScript modules, and no dependency manifests.

---

## Pages

### index.html — Company Profile

The main landing page. It is structured into the following sections, in order:

**Navigation Bar**
Fixed to the top of the viewport. Contains the brand logo, navigation links (About, Location, Contact, Get Yours CTA), an EN/ID language toggle, and a hamburger menu for mobile screens.

**Hero Section**
A full-viewport two-column layout. The left column contains the headline, description, and two call-to-action buttons ("Calculate Your Price" and "Learn More"). The right column contains a decorative CSS-drawn frame illustration with a quote and a circular badge displaying "30+ Years of craft."

**About Section (`#about`)**
A two-column grid. The left column is a placeholder area for a business photo. The right column contains three paragraphs describing the business, followed by four statistics:

| Statistic | Value |
|---|---|
| Frames crafted | 1,000,000+ |
| Years experience | 30+ |
| Frame materials | 3 |
| Custom made | 100% |

**Location Section (`#location`)**
A two-column grid. The left column shows the workshop address, phone, WhatsApp number, and opening hours inside an address card. The right column embeds a live Google Maps iframe pointed at the actual workshop location (Citra Art, Rawamangun, Jakarta Timur), with an "Open in Google Maps" button overlaid on the map.

**Contact Section (`#contact`)**
A three-column grid of contact cards for WhatsApp, Email, and Instagram. Each card displays the contact channel icon, label, value with a hyperlink, and a short descriptor. Below the grid is a copyright line and a CTA link to the calculator page.

**Footer**
A bottom strip crediting the developer and hosting platform.

---

### get-yours.html — Price Calculator

The price estimator page. It is structured as follows:

**Navigation Bar**
Fixed to the top. Contains the brand logo (links back to `index.html`), a "← Back to Home" link, and the EN/ID language toggle.

**Page Hero**
A dark-background banner with the page title "Get Yours / Custom Frame" and a short description of the tool.

**Main Content — Two-Column Layout**
The page splits into a left form column and a right result column. On tablets and mobile, this collapses to a single column.

**Left: Configuration Form**

The form contains four fields:

| Field | Type | Behavior |
|---|---|---|
| Customer Name | Text input | Updates the order summary in real time |
| Horizontal (Width) | Number input (cm, step 0.1) | Triggers price recalculation on every keystroke |
| Vertical (Height) | Number input (cm, step 0.1) | Triggers price recalculation on every keystroke |
| Glass Type | Radio button group | Triggers price recalculation on selection change |
| Frame Material | Radio button group | Triggers price recalculation on selection change |

**Right: Result Card**

The result card updates live with every input change and displays:
- Customer name (italicised, prefixed with "for")
- Estimated total price (large display, grayed out when zero)
- Price disclaimer: "Starting from · excl. delivery"
- Price breakdown: Frame cost, Back cover, Front cover / Glass
- Order summary table: Customer, Size, Glass, Frame
- WhatsApp button with a pre-filled message
- A note explaining the message is auto-filled

---

## Features

- **Bilingual interface** — Full EN/ID language switch on both pages. Language preference is persisted across sessions using `localStorage` and shared between pages using `sessionStorage`.
- **Live price calculator** — Price updates instantly on every keystroke and selection change. No submit button required.
- **WhatsApp integration** — The "Send to WhatsApp" button opens a pre-composed message in WhatsApp with the customer name, dimensions, glass type, frame type, and estimated price already filled in.
- **Embedded Google Maps** — The workshop location is embedded as an interactive iframe from Google Maps, with an overlay button to open directions in the Google Maps app.
- **Scroll animations** — Section content fades in as the user scrolls down, using the `IntersectionObserver` API.
- **Responsive design** — Both pages adapt to tablet (≤900px) and mobile (≤600px) screen sizes with dedicated media query breakpoints.
- **Hamburger menu** — On mobile screens, the navigation links collapse and are accessible via an animated hamburger button that opens a full-width drawer.
- **Language-aware WhatsApp message** — The pre-filled WhatsApp message is written in English when the page is set to EN, and in Indonesian (Bahasa Indonesia) when set to ID.

---

## Technology Stack

| Layer | Technology | Notes |
|---|---|---|
| Markup | HTML5 | Two standalone files; no templating engine |
| Styling | CSS3 | Embedded `<style>` block in each file; CSS custom properties (variables) used for the design system |
| Scripting | Vanilla JavaScript | Embedded `<script>` block; no libraries or frameworks |
| Fonts | Google Fonts | Playfair Display (serif, headings) + DM Sans (sans-serif, body) |
| Maps | Google Maps Embed API | iframe embed pointing to actual workshop coordinates |
| Hosting | GitHub Pages | Free static hosting via GitHub |
| Version Control | Git / GitHub | Managed via GitHub web interface |
| Favicon | `.ico` format | `citra-art-favicon.ico`, referenced in `index.html` only |

---

## Design System

All CSS custom properties are defined in the `:root` block shared identically across both files.

### Color Palette

| Variable | Value | Usage |
|---|---|---|
| `--cream` | `#F5F0E8` | Section backgrounds, input backgrounds, lang toggle background |
| `--warm-white` | `#FDFAF5` | Page body background, hero left panel, about section |
| `--gold` | `#C9A84C` | Primary accent — CTA buttons, dividers, radio selection highlight, stats, badge |
| `--dark` | `#1A1410` | Page hero background (get-yours), contact section background, primary headings |
| `--brown` | `#4A3728` | Navigation logo, primary buttons, hamburger icon, active lang button |
| `--brown-light` | `#7A5C48` | Form field labels |
| `--text` | `#2C2018` | Primary body text |
| `--text-muted` | `#8A7060` | Secondary body text, nav links, descriptions |
| `--border` | `#E0D5C5` | All borders — cards, inputs, nav, dividers |

### Typography

| Font | Family | Usage |
|---|---|---|
| Playfair Display | Serif | All headings (`h1`, `h2`, `h3`), nav logo, frame quote, stat numbers, result price |
| DM Sans | Sans-serif | All body text, navigation links, form labels, buttons, inputs |

### Spacing

Sections use `padding: 6rem 5rem` on desktop, reducing to `4rem 2rem` on tablet and `3rem 1.25rem` on mobile.

---

## Bilingual System (i18n)

Both pages implement a custom lightweight internationalisation system using `data-i18n` HTML attributes and a JavaScript translation object.

### How It Works

Every translatable element in the HTML carries a `data-i18n` attribute with a translation key:

```html
<h1 class="hero-title" data-i18n="hero.title">Your Memories,<br><em>Beautifully</em><br>Preserved.</h1>
```

All translations are stored in a `const i18n` object in JavaScript, containing two top-level keys — `en` and `id` — each holding all string values for that language:

```javascript
const i18n = {
  en: { 'hero.title': 'Your Memories,<br><em>Beautifully</em><br>Preserved.' },
  id: { 'hero.title': 'Kenangan Anda,<br><em>Diabadikan</em><br>dengan Indah.' }
};
```

The `setLang(lang)` function iterates over all `[data-i18n]` elements and sets their `innerHTML` to the matching translation. It also updates `input` placeholders via `data-i18n-placeholder` attributes, updates the `lang` attribute on the `<html>` element, and saves the preference to `localStorage`.

### Language Persistence

- `localStorage` (`caf-lang`) — persists the language choice across browser sessions.
- `sessionStorage` (`caf-lang`) — used by `index.html` to pass the current language to `get-yours.html` within the same tab session.
- On `get-yours.html`, language is loaded from `localStorage` first, falling back to `sessionStorage`.

### Translation Keys Reference

The following keys are defined in both `en` and `id` translation objects on `index.html`:

`nav.about` · `nav.location` · `nav.contact` · `nav.cta` · `hero.tag` · `hero.title` · `hero.desc` · `hero.btn1` · `hero.btn2` · `hero.quote` · `hero.badge` · `about.tag` · `about.title` · `about.accent` · `about.p1` · `about.p2` · `about.p3` · `about.stat1` · `about.stat2` · `about.stat3` · `about.stat4` · `location.tag` · `location.title` · `location.desc` · `location.address` · `location.mapBtn` · `contact.tag` · `contact.title` · `contact.waNote` · `contact.emailNote` · `contact.igNote` · `contact.copy` · `contact.cta` · `footer.built` · `footer.link`

The following additional keys are defined in both `en` and `id` on `get-yours.html`:

`nav.back` · `hero.tag` · `hero.title` · `hero.desc` · `form.badge` · `form.title` · `form.subtitle` · `form.nameLabel` · `form.namePlaceholder` · `form.sizeLabel` · `form.widthLabel` · `form.heightLabel` · `form.glassLabel` · `form.frameLabel` · `glass.none` · `glass.none.price` · `glass.clear` · `glass.doff` · `frame.fiber` · `frame.wood` · `frame.aluminium` · `result.title` · `result.priceLabel` · `result.priceNote` · `result.frameCost` · `result.backCover` · `result.frontCover` · `summary.title` · `summary.customer` · `summary.notFilled` · `summary.size` · `summary.glass` · `summary.frame` · `wa.btn` · `wa.note`

The following keys are used exclusively in JavaScript (not bound to DOM elements via `data-i18n`) and are also translated in both languages:

`js.forName` · `js.glass.none` · `js.glass.clear` · `js.glass.doff` · `js.frame.fiber` · `js.frame.wood` · `js.frame.aluminium` · `js.summaryFiber` · `js.summaryWood` · `js.summaryAluminium` · `js.notFilled` · `js.waMsg`

---

## Price Calculation Logic

All pricing is calculated in real time inside the `calculate()` function in `get-yours.html`. Prices are stored in the `PRICES` constant at the top of the script block — this is the only place prices need to be updated.

### Price Configuration (current values)

```javascript
const PRICES = {
  backCover: 85000,           // IDR per m² — fixed for all orders
  glass: {
    none:       0,            // IDR per m²
    clear:  150000,           // IDR per m²
    doff:   200000,           // IDR per m²
  },
  frame: {
    fiber:   35000,           // IDR per meter (starting price)
    wood:    75000,           // IDR per meter (starting price)
    aluminium: 250000,        // IDR per meter (starting price)
  }
};
```

### Formula

All dimensions entered in centimeters are converted to meters before calculation.

```
Frame price   = ((2 × width_m) + (2 × height_m) + 0.21) × frame_price_per_meter
Back cover    = width_m × height_m × 85,000
Front cover   = width_m × height_m × glass_price_per_m²
─────────────────────────────────────────────────────────
Total price   = Frame price + Back cover + Front cover
```

The coefficient `0.21` added to the perimeter accounts for the corner joining material consumed in frame assembly.

### Zero-Value Guard

If either the width or height input is empty, zero, or non-numeric, the entire total is forced to `Rp 0` and all breakdown values display as zero. This prevents division errors and misleading partial results. Selecting "No Glass" sets the glass price to zero but does not affect the rest of the formula.

### WhatsApp Message Template

**English:**
> Hello Citra Art Frame, My name is {name} and I see your estimation of my photo frame with the size {width} cm long and {height} cm wide, with {glass_type}, and a {frame_type} starting from {total_price}.

**Indonesian:**
> Halo Citra Art Frame, nama saya {name} dan saya melihat estimasi harga bingkai foto saya dengan ukuran {width} cm lebar dan {height} cm tinggi, dengan {glass_type}, dan bingkai {frame_type} mulai dari {total_price}.

The message is URL-encoded before being appended to `https://wa.me/6287782913323`.

---

## Responsive Behavior

### index.html

| Breakpoint | Layout changes |
|---|---|
| Desktop (> 900px) | Two-column hero; two-column about; side-by-side location grid; three-column contact grid; full nav links visible |
| Tablet (≤ 900px) | Single-column hero; single-column about; single-column location; two-column contact grid; nav links compressed |
| Mobile (≤ 600px) | Nav links hidden, hamburger menu shown; hero buttons stack vertically; about image switches to 3:2 aspect ratio; about accent card goes static (no longer overlapping); contact grid becomes single column |

### get-yours.html

| Breakpoint | Layout changes |
|---|---|
| Desktop (> 800px) | Two-column layout; result card is `position: sticky` at `top: 100px` |
| Tablet (≤ 800px) | Single-column layout; result card becomes static; reduced padding throughout |
| Mobile (≤ 600px) | Tighter padding on all elements; reduced font sizes on nav, hero, form, and result card; radio option text and price labels scaled down |

---

## Business Information

The following business information is hardcoded in both HTML files and their respective translation strings:

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
| Opening hours | Monday – Saturday, 09.00–17.30 WIB |
| Closed | Sundays and Public Holidays |
| Google Maps embed | Pointed to "Citra Art" pin, Rawamangun, Jakarta Timur |

---

## Maintenance Guide

### How to Update Prices

Open `get-yours.html` and find the `PRICES` constant near the top of the `<script>` block. Update the numeric values as needed. All calculations will reflect the change automatically — no other code needs to be modified.

```javascript
const PRICES = {
  backCover: 85000,       // ← edit this
  glass: {
    none: 0,
    clear: 150000,        // ← edit this
    doff: 200000,         // ← edit this
  },
  frame: {
    fiber: 35000,         // ← edit this
    wood: 75000,          // ← edit this
    aluminium: 250000,    // ← edit this
  }
};
```

Remember to also update the display price ranges shown in the radio button labels in the HTML (e.g., `"Starting from Rp 35.000/m ~ 165.000/m"`) to match any pricing changes, as those labels are separate static text and are not driven by the `PRICES` constant.

### How to Update Contact Information

Contact details appear in two places: the HTML elements and the i18n translation strings. Both must be updated when contact information changes.

**In `index.html`:**
- The address card (`<p data-i18n="location.address">`) and the contact section anchor tags (`<a href="https://wa.me/...">`, `<a href="mailto:...">`, `<a href="https://instagram.com/...">`) contain the hardcoded values.
- The `i18n` object inside the `<script>` block contains the `location.address` key in both `en` and `id` translations — update both.

**In `get-yours.html`:**
- The `WA_NUMBER` constant controls the WhatsApp destination for the pre-filled message. Update it when the WhatsApp number changes:

```javascript
const WA_NUMBER = '6287782913323'; // ← update this
```

### How to Update the Google Maps Embed

In `index.html`, locate the `<iframe>` inside `.map-container`. To point it to a different location:

1. Open [maps.google.com](https://maps.google.com) and search for the new address.
2. Click **Share → Embed a map → Copy HTML**.
3. Replace the `src` attribute value of the existing `<iframe>` with the new embed URL.
4. Also update the `href` of the `.map-overlay-btn` anchor to open the correct location in the Google Maps app.

### How to Add a Translation Key

1. Add the new `data-i18n="your.key"` attribute to the HTML element.
2. Add `'your.key': 'English text'` to the `en` object in the `i18n` constant.
3. Add `'your.key': 'Indonesian text'` to the `id` object in the `i18n` constant.

### How to Add a New Page

Create a new `.html` file in the repository root. To maintain consistent navigation behavior:
- Copy the `<nav>` block and the `lang-toggle` CSS and JS from one of the existing pages.
- On page load, read `localStorage.getItem('caf-lang')` and call `setLang()` to apply the saved language preference.

---

## Known Limitations

| Limitation | Detail |
|---|---|
| Prices are estimates only | The calculator uses fixed starting prices per meter and per m². Actual prices depend on specific frame profile, glass quality, and order quantity — the final price is confirmed by the business upon order. |
| Display price labels are not driven by `PRICES` | The price range text shown on each radio button (e.g., "Starting from Rp 35.000/m ~ 165.000/m") is static HTML and must be updated manually when pricing changes — it is not linked to the `PRICES` constant. |
| No favicon on get-yours.html | The `<link rel="icon">` tag referencing `citra-art-favicon.ico` is present only in `index.html`. The favicon is absent from `get-yours.html`. |
| No form validation feedback | If the user clicks the WhatsApp button without entering dimensions, the message is still sent with `?` placeholders for the size values. No visual validation error is shown on the form. |
| Google Maps overlay button link | The `.map-overlay-btn` anchor currently links to `https://maps.google.com/?q=Jakarta` — a generic Jakarta query — rather than the specific workshop coordinates or the place ID. It should be updated to point to the exact business pin. |
| Profile photo on about section | The about section image area is a CSS-drawn placeholder with a 🖼️ emoji. No actual business photo has been added yet. |
| No offline support | There is no service worker or caching strategy. The site is not available offline. |
| Language not applied to page title | The `<title>` tag in both pages is hardcoded in English and is not part of the i18n system. It does not change when the language is switched to Indonesian. |

---

## Built With

- HTML & CSS — designed and generated with [Claude.AI](https://claude.ai)
- Hosted on [GitHub Pages](https://pages.github.com)

*Built with ❤️ from Son — to help Dad's business reach more customers.*

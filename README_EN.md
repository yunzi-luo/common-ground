# 🌿 FoodReliefSA · CommonGround

**Bilingual free and low-cost food resource directory for South Australia**

> 🌐 Live site: [https://luoli0530-yunzi.github.io/foodrelief-sa/](https://luoli0530-yunzi.github.io/foodrelief-sa/)
> 📬 Contact: yunziluo520@gmail.com

---

## About

FoodReliefSA (CommonGround) is a single-page bilingual food relief directory designed for both the Chinese-speaking community and English-speaking residents of South Australia. It helps anyone in need quickly find the nearest free or low-cost food services in their area.

---

## Features

### 🔍 Smart Location Search
- Search by **suburb name, postcode, or street address**
- Three-tier geocoding: built-in SA postcode table → suburb name mapping → OpenStreetMap Nominatim API fallback
- Real-time **autocomplete suggestions** as you type (service names + suburbs)

### 📍 Distance-based Display Logic
- Results sorted by straight-line distance using the Haversine formula
- **Within 10km** — shown immediately, with distance labels
- **Fewer than 3 results within 10km** — automatically expands to 25km with a notice banner
- **Beyond the displayed range** — collapsed behind a "Show more services" button

### 🏷️ Filter Chips
7 quick-filter tags:

| Filter | Description |
|--------|-------------|
| All | Show all services |
| Completely free | Free-of-charge services only |
| Low cost | Subsidised or low-cost options |
| North | Northern Adelaide suburbs |
| South | Southern Adelaide suburbs |
| CBD | Adelaide city centre |
| No appointment | Walk-in services only |

### 🌏 Bilingual Support
- Automatically detects browser language preference (`navigator.language`) and defaults to Chinese or English accordingly
- Language toggle button in the top-right corner
- All service cards, search prompts, filter labels, and footer copy are fully translated in both languages

### 🎴 Service Cards
Each card displays: service name, description, address, opening hours, phone number (where available), distance badge, appointment warning, and a link to the official website. All **54 service locations** are included, covering the greater Adelaide metropolitan area and select regional services.

### 🌲 Visual Effects
- Canvas-based leaf particle system (runs only within the hero section; pauses when out of view)
- Click or tap the hero area to trigger a **wind gust effect** with crown sway animation
- **Scroll-reveal fade-in** for cards as they enter the viewport (Intersection Observer)
- All animations respect the `prefers-reduced-motion` accessibility setting

---

## Service Data

**54 service locations** are included, covering organisations such as:

- OzHarvest Free Market
- Heart & Soul (Wingfield / Noarlunga)
- Cos We Care
- Fred's Van (CBD / Kilburn / Salisbury / Elizabeth / Gawler / Semaphore / Aldinga / Christie Downs)
- Foodbank Food Hub (Bowden)
- Baptist Care, Salvation Army
- St Vincent de Paul, Anglicare SA
- Uniting Communities, Hutt St Centre
- Bedford Group, Centacare, Junction Australia
- Meals on Wheels
- Lighthouse Foodbank, Community Centres SA
- And more local food relief providers

Each service entry includes: `name (zh/en)`, `description (zh/en)`, `category (free/low/appt)`, `address`, `opening hours (zh/en)`, `phone`, `website URL`, `area tags`, `GPS coordinates`

---

## Technical Details

| Item | Detail |
|------|--------|
| Architecture | Pure single-file HTML — no framework, no build tool |
| Fonts | Bricolage Grotesque + Plus Jakarta Sans (Google Fonts) |
| Geocoding | Built-in SA postcode table + suburb mapping + Nominatim API fallback |
| Distance | Haversine formula (great-circle distance) |
| Animation | HTML Canvas + `requestAnimationFrame` |
| Scroll reveal | Intersection Observer API |
| SEO | Open Graph, Twitter Card, Schema.org JSON-LD, canonical URL |
| Deployment | GitHub Pages (single file, zero dependencies) |

---

## Deployment

This is a **single-file static website** and deploys directly to GitHub Pages:

```
Repository structure:
/
└── index.html   ← the entire website
```

1. Fork or clone this repository
2. Go to repository **Settings → Pages**
3. Set Source to the `main` branch, `/ (root)` directory
4. Save — your site will be live at `https://<username>.github.io/<repo>/`

---

## Adding a New Service

Add a new entry to the `SITES` array in `index.html`:

```javascript
{
  sid: 54,                          // unique ID (increment)
  zh: { name: "服务名称", desc: "简介" },
  en: { name: "Service Name", desc: "Description" },
  ic: "🏪",                         // emoji icon
  t: "free",                        // "free" | "low" | "appt"
  appt: false,                      // requires appointment?
  addr: "123 Example St, Suburb SA 5000",
  zh_hrs: "周一至周五 9am–5pm",
  en_hrs: "Mon–Fri 9am–5pm",
  ph: "08 8xxx xxxx",               // phone (leave "" if none)
  url: "https://example.org",       // website (leave "" if none)
  areas: ["north"],                 // "north" | "south" | "cbd" | "regional"
  lat: -34.9000,                    // GPS latitude
  lng: 138.6000                     // GPS longitude
}
```

---

## File Structure

```
index.html
├── <head>            — Meta tags, SEO, font imports
├── <style>           — All CSS (design tokens → components)
├── <body>
│   ├── <nav>         — Top navigation bar + language toggle
│   ├── .hero-section — Hero area (headline, search bar, filters, canvas)
│   ├── .cards-area   — Service card grid
│   └── .footer-band  — Footer (quote + email)
└── <script>
    ├── LANG{}        — Bilingual copy object
    ├── SITES[]       — 54 service entries
    ├── POSTCODES{}   — SA postcode → coordinates map
    ├── SUBURBS{}     — Suburb name → postcode mapping
    ├── geocode()     — Three-tier geocoding function
    ├── render()      — Card rendering and distance logic
    ├── Scroll reveal — Fade-in on scroll
    └── Leaf canvas   — Leaf particle system
```

---

## Acknowledgements

Thank you to every organisation and volunteer quietly providing food relief across South Australia.

This site was built in the belief that language and information should never be a barrier to finding help.

---

## Contact

📬 yunziluo520@gmail.com

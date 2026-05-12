# Mellowdee Technologies - Website Redesign

A ground-up redesign of [mellowdeetechnologies.com], built to solve a real problem: the existing store has a full product catalogue that is invinsible to customers, forcing them to WhatsApp before they can even make a decision. This redesign puts every product, every price and every spec front and center - and keeps WhatsApp where it belongs: at the end of the buying decision, not the beginning.

## The Problem

The current Mellowdee site has categories but no visible products. A customer who finds them through Instagram, Google or word of mouth arrives at the store, sees category headings and hits a dead end. The only path forward is a WhatsApp conversation - which defeats the puropse of having an online store entirely.

This redesign fixes that by building a fully browsable product catalogue with real prices, filter and sort controls, and detailed product pages. WhatsApp remains available as a support and checkout channel, but customers are never forced into it just to see what's for sale.

## Tech Stack

| Layer | Choice | Why |
| :----- | :----: | :-----: |
| markup | HTML5 | Semantic, fast, no fremework overhead |
| styling | TailwindCSS v4 | utility-first, consistent spacing, responsive by default |
| logic | vanilla javascript | no build complexity, fast load, matches current skill set |
| data | JSON product catalogue | Easy to update, CMS-ready later |
| deployment | Vercel | Free tier, instant deploys, custom domain |
| CMS (Phase 2) | TBD | To be layered in after static frontend is complete |

## Brand Colors

| Role | Hex | Usage |
| :----: | :----: | :-----: |
| primary | `#13559e` (dusk blue) | Nav, buttons, links, icon fills |
| secondary | `#7ccfed` (sky blue) | accents, hover states, hero text highlights |
| dark base | `#0d1425` (ink black) | hero backgrounds, nav, footer trust bar |
| surface | `#eef4fb` (alice blue) | category section, product image backgrounds |
| text | `#12192b` (prussian blue) | body copy, product names, headings |

## Pages

### Homepage

The entry point. Designed to orient the customer immediately and push them toward browsing.

- sticky nav with logo, links, search icon and whatsapp order button
- hero section with headline, subtext and dual CTAs (Shop Now / Browse Categories)
- 6-category grid: Laptops, desktops, monitors, printers, accessories, gaming
- featured products strip - real products with visible prices
- trust bar: cbd delivery, genuine products, easy returns, repair services
- footer with links, location (Parklands, Nairobi), and socials

### Category Pages (`/laptops`, `/monitors`, etc)

One page per product

- Filter sidebar: price range, brand
- sort controls: price low-to-high, high-to-low, newest
- product grid: 3 columns desktop, 2 columns mobile
- each card shows image/icon, product name, key specs and price

### Product Detail Page

Where the buying decision actually happens

- image gallery with thumbnails
- full product name, price (always visible), and availability status
- Key specs in a clean table
- Primary CTA: "Order via WhatsApp" - pre-fills the product name and price in the message
- secondary CTA: "Enquire" for questions
- related products section below

### Cart + Whatsappp Checkout

static-friendly checkout using `localstorage`

- customer adds items to cart throughout browsing
- cart page shows items, quantities, subtotal
- "checkout" composes a whatsapp message with the full order and opens `wa.me/`
- no backend required in phase 1

### About/contact

simple page covering who mellowdee are, where they are based and how to reac them.

## Project structure

```
mellowdee-redesign/
├── index.html
├── shop.html
├── about.html
├── contact.html
├── categories/
│   ├── laptops.html
│   ├── desktops.html
│   ├── monitors.html
│   ├── printers.html
│   ├── accessories.html
│   └── gaming.html
├── product.html
├── cart.html
├── src/
│   ├── assets/
│   |   └── images/
│   ├── css/
│   │   └── main.css
│   ├── js/
│   │   ├── catalogue.js
│   │   ├── filters.js
│   │   ├── cart.js
│   │   └── whatsapp.js
├── data/
│   └── products.json
├── .gitignore
├── package-lock.json
├── package.json
└── README.md
```

## Product data

Products are stored in `data/products.json`. Each product entry follows this shape:

```json
{
    "id": "hp-elitebook-840-g8",
    "name": "HP EliteBook 840 G8",
    "category": "laptops",
    "brand": "HP",
    "price":  85000,
    "currency": "Ksh",
    "status": "in_stock",
    "specs": {
        "processor": "Intel core i7-1165G7",
        "ram": "16GB DDR4",
        "storage": "512BG SSD",
        "display": "14\" FHD IPS"
    },
    "image": "src/assets/images/products/hp-elitebook-840-g8.webp",
    "featured": true,
    "new_arrival": false
}
```

This structure is designed to be cms-compatible - when phase 2 is ready, the json file is simply replaced by an API endpoint.

## WhatsApp Integration

The site uses whatsapp in two places

**Nav order button** - a general entry point for customers who already know what they want and prefer to chat directly.

**Product page cta** - pre-fills a message with the product name and price so the customer arrives in the conversation ready to buy, not to browse.

**cart checkout** -composes a full order summary from cart state and opens it in whatsapp

## Development phases

### Phase 1 - static frontend

- all HTML pages built and responsive
- product data loaded from `products.json` via `fetch()`
- filters and sort logic in vanilla js
- cart managed in `local storage`
- whatsapp checkout flow working
- deployed to vercel

### Phase 2 - cms integration

- connect a headless CMS (eg sanity, contentful or a simpler option like airtable)
- mellowdee can add and update products without touching code
- product images managed through the cms media library
- json data layer swapper for cms api calls

## Key design decisions

**Products are always visible** - No login, no whatsapp required, no "contact for price". Every product in the catalogue is browsable by anyone.

**Prices are always shown** - Hidden pricing is a trust killer and increases drop-off. Every product card shows its price.

**Whatsapp is support not a gatekeeper** - It's available everywhere, but customers reach it after making their own decision - not as a prerequisite to seeing the catalogue.

**Mobile-first layout** - Majority of Nairobi shoppers browse on their phones. Every layout decision, the 2-column product grid, the hamburger nav, the touch-friendly category cards - is made with mobile as the primary context

**fast and lightweight** - No framework, no heavy dependancies. Static HTML + vanilla JS means the site loads quickly even on slower connections.

## Deployment

The site deploys automatically to vercel on every push to `main`.

## Context

This problem originated from a real customer experience. The developer visited mellowdeetechnologies.com after seeing a monitor on their instagram page at a budget-friendly price. The site had the categories but none of the products. The only option was to contact them via whatsapp - before making any kind of informed decision. This redesign is the direct response to that experience, built as a pitch to the Mellowdee team to show what their store could be.

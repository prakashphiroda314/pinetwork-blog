# Pi Network Knowledge Hub

A premium, fully responsive personal knowledge platform built with HTML5, Tailwind CSS, and Vanilla JavaScript. Styled as a professional editorial publication in the vein of Medium, Hashnode, and Stripe — with a distinctive purple and gold brand identity.

## About

Pi network Knowledge Hub is a static content platform by **Pi Community** — AI Educator, Digital Builder, and Web3 Advocate. The platform covers eight knowledge domains:

- π Pi Network

## Key Features

- **Fully Static** — No backend, no database. Pure HTML + CSS + JS
- **Dark Mode** — System-respecting with manual toggle, persisted in localStorage
- **Instant Search** — Client-side full-text search across title, excerpt, tags, and category
- **Category Filtering** — Filter articles by any of 8 categories
- **Responsive** — Mobile-first, works on all screen sizes
- **Animated** — Intersection Observer scroll animations, hover effects, glassmorphism
- **SEO Ready** — robots.txt, sitemap.xml, Open Graph, Twitter Cards, Schema.org JSON-LD

## Technology Stack

| Technology | Purpose |
|---|---|
| HTML5 | Semantic page structure |
| Tailwind CSS (CDN) | Utility-first styling |
| Vanilla JavaScript | Interactivity, data loading, search |
| JSON | Article data store (`data/articles.json`) |
| Google Fonts | Poppins (headings) + Inter (body) |
| Netlify | Hosting + CDN + headers |

## Project Structure

```
/
├── index.html              # Home page
├── articles.html           # Article listing with filter + sort
├── article.html            # Single article template
├── categories.html         # Category browse page
├── about.html              # About Prakash page
├── search.html             # Search page
├── contact.html            # Contact page
├── data/
│   └── articles.json       # All article data (20 articles, 8 categories)
├── assets/
│   ├── css/
│   │   └── styles.css      # Custom CSS (variables, animations, components)
│   └── js/
│       └── main.js         # Shared JS (header, footer, utilities)
├── netlify.toml            # Netlify config (headers, cache)
├── robots.txt
└── sitemap.xml
```

## Running Locally

Open any HTML file directly in a browser, or use a simple static file server:

```bash
# Using Python
python3 -m http.server 8000

# Using Node.js
npx serve .

# Using Netlify CLI (recommended for full Netlify feature emulation)
netlify dev
```

Then open `http://localhost:8000` (or the port shown).

## Deployment

The site is optimized for:
- **Netlify** (primary) — Push to GitHub, connect to Netlify
- **GitHub Pages** — Set base URL to repo root
- **Cloudflare Pages** — Deploy from GitHub with no build command

No build step required — everything works as static files.

## Color Palette

| Name | Hex |
|---|---|
| Primary Purple | `#6D28D9` |
| Dark Purple | `#5B21B6` |
| Accent Gold | `#F59E0B` |
| Background | `#FFFFFF` |
| Section Background | `#F8FAFC` |
| Text | `#111827` |
| Border | `#E5E7EB` |


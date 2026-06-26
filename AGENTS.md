# AGENTS.md — Prakash Knowledge Hub Architecture

## Overview

This is a **fully static** personal knowledge platform — no build step, no framework, no backend, no database. All interactivity is achieved with Vanilla JavaScript reading from a local JSON data file.

## Key Architecture Decisions

### Static-First
- No Node.js/npm runtime dependencies
- No build pipeline (webpack, vite, etc.)
- Tailwind CSS loaded via CDN in every HTML file
- All pages are `.html` files with inline `<script>` tags for page-specific logic
- Shared functionality lives in `assets/js/main.js` loaded in every page

### Data Layer
- All articles and categories stored in `data/articles.json`
- Loaded at runtime via `fetch('/data/articles.json')` in `main.js`
- Every page calls `initPage()` which calls `loadArticles()` and exposes `ARTICLES` and `CATEGORIES` globals
- No persistence — all filtering, sorting, and searching happens in-memory per page load

### Component Architecture (via JS injection)
- **Header** and **Footer** are injected via `renderHeader()` and `renderFooter()` in `main.js`
- Each HTML page has `<div id="header-mount">` and `<div id="footer-mount">`
- `initPage(activePage)` handles theme, header, footer, scroll-to-top, animations, and data loading
- `createArticleCard(article, size)` is the shared card component rendered as HTML string

### Dark Mode
- Implemented via `class="dark"` on `<html>` (Tailwind `darkMode: 'class'`)
- State persisted in `localStorage` key `theme`
- Initialized on every page with an inline `<script>` before `<body>` to prevent flash
- Toggle button in header switches class and saves preference

### Animations
- Scroll-triggered animations use `IntersectionObserver` on `.animate-on-scroll` elements
- When intersecting, the class `visible` is added, triggering CSS transition
- Hero and initial elements use CSS keyframe animations (`@keyframes slideUp`)

## File Roles

| File | Role |
|---|---|
| `assets/js/main.js` | Shared JS: data loading, header/footer render, utilities (formatNumber, formatDate, etc.), article card component, theme, animations |
| `assets/css/styles.css` | Custom CSS: CSS variables, animations, component classes (`.article-card`, `.btn-primary`, `.hero-section`, etc.) |
| `data/articles.json` | Article data: 20 articles across 8 categories with full metadata and HTML content |
| `index.html` | Homepage: hero, featured article, topic grid, latest articles, popular reads, community CTA |
| `articles.html` | Article listing: filter by category, sort (newest/popular/liked), search |
| `article.html` | Single article: reads `?slug=` param, renders full article with ToC, share buttons, related articles |
| `categories.html` | Browse all categories with article previews per category |
| `search.html` | Full-text search across all article fields with debouncing |
| `about.html` | Prakash bio, stats, expertise tags, Pi Network and portfolio cards |
| `contact.html` | Contact form (frontend-only, shows success state), social link cards |

## Article JSON Schema

```json
{
  "id": number,
  "slug": string,           // URL-safe identifier
  "title": string,
  "excerpt": string,
  "content": string,        // HTML string
  "category": string,       // Display name e.g. "Artificial Intelligence"
  "categorySlug": string,   // URL slug e.g. "artificial-intelligence"
  "tags": string[],
  "author": "Prakash Choudhary",
  "date": "YYYY-MM-DD",
  "readTime": number,       // minutes
  "views": number,
  "likes": number,
  "featured": boolean,
  "coverImage": string      // URL
}
```

## Adding New Articles

Edit `data/articles.json` and add to the `"articles"` array following the schema above. The `categorySlug` must match one of the 8 defined categories. All pages will automatically reflect the new article on next load.

## Adding New Pages

1. Copy the boilerplate from any existing page (header-mount, footer-mount, Tailwind CDN, CSS link, main.js script)
2. Call `initPage('pagename')` — the `pagename` activates the corresponding nav link
3. Use `createArticleCard()`, `searchArticles()`, `formatNumber()`, `formatDate()` from `main.js`

## Coding Conventions

- Class names follow Tailwind utilities + custom CSS class names from `styles.css`
- Custom CSS uses CSS variables (defined in `:root`) for theming
- Dark mode variants use `.dark` prefix in `styles.css` or `dark:` Tailwind prefixes inline
- JS is untyped, no modules, no imports — all functions are global from `main.js`
- `async/await` pattern for data loading; pages call `await initPage()` then render
- No error boundaries — pages fail gracefully to loading/empty states

## SEO Notes

- Schema.org JSON-LD on homepage (WebSite) and about page (Person)
- Every page has `<title>`, `<meta description>`, canonical URL, OG tags, Twitter Card
- `robots.txt` and `sitemap.xml` at root
- Article slugs are URL-safe and descriptive

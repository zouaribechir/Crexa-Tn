# CREXA — Creator & Online Business Calculator Platform

> **"Calculate smarter. Grow faster."**  
> Canonical URL: [https://crexa.tn](https://crexa.tn)

CREXA is a production-ready, global digital calculator platform built for content creators, influencers, affiliates, and small online businesses. It provides 12 precision client-side mathematical calculators covering video monetization, engagement rates, commissions, profit margins, audience growth forecasting, and commercial sponsorship rate quotes.

---

## 1. Features & Architecture

- **100% Client-Side Computation**: All mathematical formulas execute locally in the user's browser with zero network latency, zero server roundtrips, and zero database dependencies.
- **Privacy First**: User inputs, financial numbers, revenues, and views are never transmitted, logged, or stored on any server.
- **12 Comprehensive Calculators**:
  1. **YouTube Money Calculator** (`/youtube-money-calculator`)
  2. **YouTube RPM Calculator** (`/youtube-rpm-calculator`)
  3. **YouTube CPM Calculator** (`/youtube-cpm-calculator`)
  4. **TikTok Money Calculator** (`/tiktok-money-calculator`)
  5. **TikTok Engagement Rate Calculator** (`/tiktok-engagement-calculator`)
  6. **Instagram Engagement Rate Calculator** (`/instagram-engagement-calculator`)
  7. **Affiliate Commission Calculator** (`/affiliate-commission-calculator`)
  8. **Profit Margin Calculator** (`/profit-margin-calculator`)
  9. **Ad Revenue Calculator** (`/ad-revenue-calculator`)
  10. **Subscriber Growth Calculator** (`/subscriber-growth-calculator`)
  11. **Video ROI Calculator** (`/video-roi-calculator`)
  12. **Sponsorship Calculator** (`/sponsorship-calculator`)
- **6 Dedicated Category Hubs**:
  - `/youtube`, `/tiktok`, `/instagram`, `/affiliate`, `/business`, `/social-media`
- **Design System**: Dark theme by default (#0B0D10 background, #12161B surface, #7C5CFC accent, #3CCB8E success accent), working light/dark toggle persisted locally, zero-pill typography, and responsive mobile-first layouts.
- **Multi-Currency Engine**: Support for USD ($), EUR (€), GBP (£), CAD (CA$), AUD (AU$), and TND (DT) with local persistence.
- **Instant Search**: Keyboard-accessible search modal (⌘K / Ctrl+K) filtering across all calculators in real time.
- **Technical & On-Page SEO**:
  - Unique titles (30–60 chars) and meta descriptions (120–160 chars) on every route.
  - OpenGraph & Twitter Cards with 16:9 social share asset (`og-image.png`).
  - Schema.org JSON-LD structured data (`Organization`, `WebSite`, `WebPage`, `SoftwareApplication`, `BreadcrumbList`, `FAQPage`).
  - Production `robots.txt` referencing canonical `sitemap.xml`.
  - Machine-readable `sitemap.xml` listing all 22 canonical indexable routes on `https://crexa.tn`.
  - Google Search Console verification token: `googlea980b655aed97faa.html`.
- **Google Analytics 4**:
  - Measurement ID: `G-X9QZ8256LD`.
  - SPA client-side page view dispatcher with duplicate suppression.
  - Zero PII or financial user input tracking.

---

## 2. Technology Stack

- **Framework**: React 19 + TypeScript
- **Bundler & Dev Server**: Vite 8
- **Styling**: Tailwind CSS v4
- **Icons**: Lucide React
- **Unit Testing**: Vitest 5
- **Hosting / Deploy Target**: Netlify (with clean URL redirects in `_redirects` & `netlify.toml`)

---

## 3. Installation & Local Development

### Prerequisites
- Node.js 18+ (tested on Node v22)
- npm, pnpm, or bun

### Commands

```bash
# 1. Install dependencies
npm install

# 2. Run local development server (port 3000)
npm run dev

# 3. Execute unit test suite
npm run test

# 4. Typecheck TypeScript codebase
npm run typecheck

# 5. Build for production
npm run build

# 6. Preview production build locally
npm run preview
```

---

## 4. Google Analytics 4 Setup & Verification

CREXA implements GA4 measurement ID `G-X9QZ8256LD` with single-tag initialization:

1. **Tag Loading**: Loaded asynchronously from `https://www.googletagmanager.com/gtag/js?id=G-X9QZ8256LD`.
2. **Double-Count Prevention**: Initial configuration disables automatic page views:
   ```javascript
   window.gtag('config', 'G-X9QZ8256LD', { send_page_view: false });
   ```
3. **SPA Route Tracking**: The `GoogleAnalytics` component observes router path changes and fires an explicit `page_view` event once `document.title` and meta tags have synchronized.
4. **Adblocker Resilient**: If a user runs an adblocker or privacy extension, analytics calls fail silently without breaking application math or throwing runtime errors.

### How to Verify in GA4 Realtime and DebugView

1. Open Google Chrome with the [Google Analytics Debugger extension](https://chromewebstore.google.com/detail/google-analytics-debugger/jnnbpmfnfgflnjvfnpfndphdafgapack) enabled, or append `?_dbg=1` to the URL.
2. In your Google Analytics dashboard, navigate to **Admin > Data Display > DebugView**.
3. Open `https://crexa.tn` and navigate between pages (e.g. `/` -> `/youtube-money-calculator` -> `/profit-margin-calculator`).
4. In DebugView, verify that:
   - Exactly one `page_view` event appears per route change.
   - `page_title` reflects the exact title of the active calculator.
   - `page_location` matches the full canonical URL.
   - No financial values or calculator inputs appear in event parameters.
5. In **Reports > Realtime**, verify active user presence on `crexa.tn`.

*Note: Actual live tracking cannot be confirmed from source code alone; you must inspect events in the active Google Analytics console during live user visits.*

---

## 5. SEO & Sitemap Maintenance

- **Canonical Domain**: `https://crexa.tn` (always without `www`).
- **Sitemap Location**: `public/sitemap.xml` (copied to `dist/sitemap.xml` on build).
- **Adding a New Calculator**:
  1. Add the calculator formula to `src/lib/calculatorMath.ts` and write unit tests in `src/lib/calculatorMath.test.ts`.
  2. Add the metadata, worked example, FAQs, and content to `src/data/calculators.ts`.
  3. Create the UI component in `src/components/calculators/` and register in `src/pages/CalculatorDetailPage.tsx`.
  4. Add the canonical URL to `public/sitemap.xml` with appropriate priority.
  5. Add to `src/pages/SitemapPage.tsx`.

---

## 6. Netlify Deployment Instructions

### Automatic Git Deployment
1. Push the repository to GitHub, GitLab, or Bitbucket.
2. Log into [Netlify](https://app.netlify.com/) and click **Add new site > Import an existing project**.
3. Select the repository.
4. Build settings:
   - **Base directory**: `/` (root)
   - **Build command**: `npm run build`
   - **Publish directory**: `dist`
5. Netlify will automatically detect `netlify.toml` and apply:
   - Canonical 301 redirect from `https://www.crexa.tn/*` to `https://crexa.tn/:splat`.
   - Single-Page Application 200 rewrite from `/*` to `/index.html`.
6. Assign custom domain:
   - In **Domain Management**, add custom domain `crexa.tn`.
   - Configure DNS records (Apex `@` pointing to Netlify Load Balancer, `CNAME` for `www`).
   - Enable Netlify Let's Encrypt SSL certificate.

### Manual Drag & Drop Deployment
```bash
npm run build
```
Drag the resulting `dist/` directory directly into Netlify's manual deploy drop zone.

---

## 7. Production QA Checklist

- [x] All 12 calculators implemented with working formulas.
- [x] Zero denominator safeguards active on every formula.
- [x] Negative value rejection on all appropriate numeric inputs.
- [x] Responsive layout tested on desktop, tablet, and mobile viewport widths.
- [x] Dark theme default with instant light/dark toggle and localStorage persistence.
- [x] Multi-currency switcher with USD, EUR, GBP, CAD, AUD, TND support.
- [x] 100% unit test coverage for math utilities passing in Vitest.
- [x] Zero TypeScript compilation errors (`tsc --noEmit`).
- [x] Netlify redirects configured for clean URLs and deep-linking.
- [x] Canonical tags pointing strictly to `https://crexa.tn`.
- [x] `sitemap.xml` and `robots.txt` present and aligned with all indexable routes.
- [x] GA4 Measurement ID `G-X9QZ8256LD` configured with SPA duplicate suppression.
- [x] Zero references to deprecated brand names across production code.

---

## 8. Known Limitations

- **Platform Variance**: Social platforms (YouTube, TikTok, Instagram) adjust monetization algorithms, RPM splits, and qualified view definitions dynamically. Numerical calculations are model benchmarks and should be treated as estimates, not guaranteed earnings.
- **Client-Side SPA SEO**: In browser environments where web crawlers execute JavaScript, dynamic meta tags and JSON-LD update in DOM via `SeoHead.tsx`. For search engine bots with limited JavaScript capabilities, static pre-rendering (SSG) or edge SSR can be layered in future iterations.

---

&copy; 2026 CREXA ([https://crexa.tn](https://crexa.tn)). All rights reserved.

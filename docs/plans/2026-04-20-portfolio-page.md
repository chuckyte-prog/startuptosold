# Portfolio Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a portfolio page at startuptosold.com/portfolio with a card grid linking to detail pages for each project.

**Architecture:** Static HTML pages matching the existing site design system (dark theme, Plus Jakarta Sans, orange accent). Main grid page + individual detail pages in a `/portfolio/` subfolder. No build step, no framework.

**Tech Stack:** HTML, CSS, vanilla JS (scroll reveal, hamburger menu)

---

## Task 1: Create portfolio.html (main grid page)

**Files:**
- Create: `portfolio.html`

**Step 1: Create the file**

Build `portfolio.html` at the site root with:
- Full `<head>` matching subpage pattern (GA4, fonts, meta tags, favicon)
- Canonical URL: `https://startuptosold.com/portfolio`
- Title: "Portfolio — Startup to Sold Consulting"
- Meta description: "Real tools and automations I've built. Live demos, measurable results, no slide decks."

**Step 2: Add nav**

Same nav as other subpages (logo, nav-links with Services/AI Automations/How It Works/About/Contact, phone, hamburger). No "Portfolio" link in nav yet.

**Step 3: Add hero section**

- Eyebrow: "PORTFOLIO"
- H1: "Built. <em>Not Theorized.</em>"
- Subtitle: "Real tools solving real problems. Each one built, deployed, and running."
- No CTA button, no stats column
- Same hero styling as subpages (radial gradient glow, dark-bg)

**Step 4: Add card grid section**

CSS grid: 3 columns desktop, 2 columns tablet (max-width: 1024px), 1 column mobile (max-width: 768px).

Card structure:
```html
<a href="portfolio/valuation-calculator.html" class="portfolio-card">
  <div class="card-image" style="background-image: url('images/portfolio/valuation-thumb.png')"></div>
  <div class="card-body">
    <div class="card-badge">Built in ~8 hours</div>
    <h3 class="card-title">Know Your Business's Worth in 5 Minutes</h3>
    <p class="card-desc">Free valuation tool that gives owners an instant range based on their industry, location, and exit readiness.</p>
    <span class="card-link">View details &rarr;</span>
  </div>
</a>
```

Card styling:
- `--dark-surface` background
- 1px `--dark-rule` border
- `translateY(-3px)` + border-color orange on hover
- Image area: 200px height, `object-fit: cover`, placeholder gradient if no image
- Badge: small, orange text, 0.7rem, uppercase
- Title: 1.05rem, font-weight 700
- Desc: 0.88rem, `--dark-muted`
- Link: orange, 0.8rem, uppercase

Two cards:
1. Valuation Calculator
2. Bushrod Park Court Scraper

**Step 5: Add CTA section**

Same pattern as subpages:
```html
<section class="section-cta">
  <div class="section-inner">
    <div class="section-eyebrow" style="justify-content:center;">Get Started</div>
    <h2>Want something like this <em>for your business?</em></h2>
    <p>I build tools and automations that save time and generate leads. Let's talk about what would move the needle for you.</p>
    <a href="https://calendly.com/chuck-startuptosold/30min" target="_blank" rel="noopener" class="btn-primary">Book a Free Strategy Session</a>
    <p class="cta-secondary">Or reach me at <a href="tel:8585238881">858-523-8881</a> &middot; <a href="mailto:chuck@startuptosold.com">chuck@startuptosold.com</a></p>
  </div>
</section>
```

**Step 6: Add footer + JS**

Standard footer (same as lead-capture.html). Hamburger menu JS + scroll reveal for cards.

**Step 7: Verify in browser**

Open `portfolio.html` locally, check:
- Desktop: 3-column grid renders correctly
- Mobile (resize to 375px): single column, hamburger works
- Hover states on cards
- Links point to correct detail pages (will 404 until built)

**Step 8: Commit**

```bash
git add portfolio.html
git commit -m "feat: add portfolio grid page with 2 project cards"
```

---

## Task 2: Create portfolio directory and valuation calculator detail page

**Files:**
- Create: `portfolio/valuation-calculator.html`

**Step 1: Create portfolio/ directory and the file**

Build detail page following the automations subpage pattern (lead-capture.html as reference).

**Step 2: Hero section**

- Back link: "← Back to Portfolio" → `/portfolio.html`
- Eyebrow: "LEAD GENERATION TOOL"
- H1: "Know Your Business's Worth <em>in 5 Minutes.</em>"
- Subtitle: "A free valuation calculator that combines industry data, metro-level market conditions, and exit readiness assessment to show owners where they stand."
- Stats column:
  - "~8 hrs" / "Time to build"
  - "$0" / "Cost to run (static HTML, no backend)"
  - "5 pillars" / "Exit readiness assessment"

**Step 3: Content sections**

Section 1 — "What It Does" (section-phases pattern, but as prose):
- Users enter revenue, industry, and location
- Answer 10 yes/no questions across 5 pillars
- Get an instant valuation range showing what's pulling the number up or down
- PDF export with full breakdown

Section 2 — "The Problem It Solves" (section-services style):
- Business owners have no idea what their company is worth
- Formal valuations cost $5K-$15K and take weeks
- This gives them a starting point in minutes
- Opens a warm conversation about the gaps the tool identified

Section 3 — "Live Demo":
- Prominent link/button to the live tool: `https://startuptosold.com/business-valuation-calculator.html`
- Or embed in an iframe if it works

**Step 4: CTA + footer**

Same CTA and footer as portfolio.html.

**Step 5: Verify in browser**

Check desktop and mobile rendering. Verify back link works. Verify live demo link works.

**Step 6: Commit**

```bash
git add portfolio/valuation-calculator.html
git commit -m "feat: add valuation calculator portfolio detail page"
```

---

## Task 3: Create Bushrod Park court scraper detail page

**Files:**
- Create: `portfolio/bushrod-court-scraper.html`

**Step 1: Build the page**

Same structure as valuation calculator detail page.

**Step 2: Hero section**

- Back link: "← Back to Portfolio" → `/portfolio.html`
- Eyebrow: "AUTOMATION"
- H1: "Real-Time Court Availability, <em>Zero Manual Checking.</em>"
- Subtitle: "Automated tool that scrapes live court schedules so coaches stop wasting time navigating clunky city booking portals."
- Stats column:
  - "1 afternoon" / "Time to build"
  - "$0/run" / "vs. $0.50/run with AI vision"
  - "5-10 min" / "Saved per schedule check"

**Step 3: Content sections**

Section 1 — "What It Does":
- Pick a date, get available court time slots instantly
- Replaces a multi-step manual process (find the link, log in, navigate calendar, check each slot)
- Runs on a persistent headless browser for fast responses

Section 2 — "The Problem It Solves":
- Coaches and organizers check availability multiple times per week
- The city's booking portal is clunky, requires multiple clicks
- During peak season this adds up to significant wasted time

Section 3 — "Technical Decision":
- Two options evaluated: AI computer-use (~$0.50/run) vs. direct DOM scraping (free)
- Chose the Python + Playwright approach after finding the public widget URL
- Result: same functionality at zero marginal cost

Section 4 — "Live Demo":
- Embed or link to `https://web-production-1d80d.up.railway.app`

**Step 4: CTA + footer**

Same as other pages.

**Step 5: Verify in browser**

Check desktop and mobile. Verify live demo link works.

**Step 6: Commit**

```bash
git add portfolio/bushrod-court-scraper.html
git commit -m "feat: add Bushrod court scraper portfolio detail page"
```

---

## Task 4: Add placeholder images

**Files:**
- Create: `images/portfolio/` directory
- Note: Actual screenshots to be taken later

**Step 1: Create the directory**

```bash
mkdir -p images/portfolio
```

**Step 2: Add CSS placeholder fallback**

In `portfolio.html`, ensure the `.card-image` class has a gradient fallback:
```css
.card-image {
  height: 200px;
  background: linear-gradient(135deg, var(--dark-surface) 0%, rgba(232,93,38,0.1) 100%);
  background-size: cover;
  background-position: center;
}
```

This looks intentional even without screenshots.

**Step 3: Commit**

```bash
git add images/portfolio/.gitkeep portfolio.html
git commit -m "feat: add portfolio image directory with placeholder styling"
```

---

## Task 5: Final responsive QA

**Step 1: Test all three pages at these breakpoints**

- 1440px (large desktop)
- 1024px (tablet landscape)
- 768px (tablet portrait)
- 375px (mobile)

**Step 2: Check against sub-page design rules**

Per established rules:
- `.section-lead` max-width: 720px
- Hero mobile: `padding: 6rem 1.5rem 3rem`, `.hero-inner` gap: 2rem
- Hero stats: `padding-top: 0; margin-top: 0` on mobile
- No flow diagrams

**Step 3: Fix any issues found**

**Step 4: Final commit if changes needed**

```bash
git add -A
git commit -m "fix: responsive adjustments for portfolio pages"
```

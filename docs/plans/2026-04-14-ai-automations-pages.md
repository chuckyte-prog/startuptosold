# AI Automations Pages Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a fully designed AI Automations hub page and 10 sub-pages for startuptosold.com, replacing the current placeholder automations.html.

**Architecture:** Static HTML pages matching the existing site design system (Plus Jakarta Sans, dark bg #0f1623, orange #e85d26). Hub page at `automations.html` links to 10 sub-pages in an `automations/` subdirectory. Each sub-page follows a consistent structure: hero, services list, how it works (3-phase model), who it's for, FAQ, CTA, footer.

**Tech Stack:** Static HTML, inline CSS, vanilla JS only where needed (nav scroll behavior, mobile hamburger, FAQ accordion). Plus Jakarta Sans (Google Fonts). No JS frameworks. Google Analytics G-1XV0PEXSQJ on every page.

**Reference files:**
- Design system: `exit-readiness.html` (dark theme, nav pattern, section structure, eyebrow labels, hero stats column)
- Nav pattern: `index.html` (fixed nav, hamburger mobile menu, orange CTA, scroll behavior)
- Current placeholder: `automations.html` (to be replaced entirely)
- Content source: `c:\Users\chuck\Obsidian Vault\Career\S2S v2.0\Services\AI Services.md`

**Visual Approach:**
- **Service card icons:** Inline SVG, one per category. Hand-crafted, not generic. Examples: lightning bolt (lead capture), calendar (scheduling), document (proposals), chat bubble (customer comms), gear (operations), brain (knowledge base), megaphone (marketing), star (reviews), chart (reporting), eye (competitor intel).
- **3-phase "how it works" strip:** Pure CSS horizontal flow -- three dark-surface boxes connected by orange arrows. No image file.
- **Automation flow diagrams:** Each sub-page gets a CSS diagram showing the specific automation flow (e.g., "Form → AI Score → CRM → Slack"). Dark surface boxes, orange connectors, monospace labels.
- **Background atmosphere:** CSS radial gradients and subtle dot/grid patterns on hero sections. No image files -- all CSS.
- **Screenshot placeholders:** Each sub-page has a styled placeholder block (`<!-- Replace with actual n8n workflow screenshot -->`) where a real screenshot goes once the automation is built. Placeholder styled as a dark-surface box with dashed orange border and label "Live example coming soon."
- **No stock photos.** No AI-generated illustrations. Real screenshots added by Chuck as automations are built.

**Skills applied:**
- `frontend-design` -- distinctive, production-grade aesthetic. Not generic. Commit to the existing site's dark, editorial tone and extend it with intention. Use the orange accent boldly. Section eyebrows, generous whitespace, sharp typographic hierarchy.
- `Landing Page Architect` -- section order: nav → hero → how it works → services → FAQ → CTA → footer. Every page ends with a repeated CTA before the footer.

---

## Design System Reference

From `exit-readiness.html` -- use these consistently across all pages:

```css
:root {
  --ink: #1c1c1e;
  --orange: #e85d26;
  --dark-bg: #0f1623;
  --dark-surface: #162032;
  --dark-text: #f2f2f5;
  --dark-muted: #8e8e99;
  --dark-rule: rgba(255,255,255,0.08);
  --off-white: #f5f4f1;
  --muted: #6b6b72;
}
font-family: 'Plus Jakarta Sans', sans-serif;
font-size: 18px;
line-height: 1.75;
```

**Nav:** Fixed, dark (rgba(15,22,35,0.85) + backdrop-filter blur), logo left with orange dot, links center (uppercase 0.78rem 700 weight), phone right in orange. Mobile hamburger drawer. Matches exit-readiness.html exactly.

**Section eyebrow:** Orange, uppercase, 0.72rem, 0.14em letter-spacing, with a 1.5rem orange line before it.

**Section headings:** `clamp(1.8rem, 3.5vw, 2.6rem)`, weight 800, letter-spacing -0.03em. Key words wrapped in `<em>` render in orange.

**Hero:** Dark bg, padding 9rem top / 6rem bottom. Two-column grid (content + stats column). Stats column has orange numbers, dark-muted labels, separated by dark-rule borders.

**Cards:** Dark surface (#162032), 1px dark-rule border, generous padding. Hover: subtle border-color shift to orange.

**CTA button:** `background: var(--orange)`, white text, uppercase, 0.8rem, 700 weight, no border-radius (sharp edges match the site's editorial feel).

**Footer:** Dark surface, max-width 1100px, links in dark-muted, copyright small. Match existing site footer if one exists -- check `index.html` for footer pattern.

**No pricing section.** No social proof strip (lives on main site). No em-dashes -- use `--` instead.

---

## Page Structure (Hub + Sub-pages)

### Hub page sections (automations.html):
1. Nav (matches site)
2. Hero -- "AI Automations for Bay Area Businesses" -- short punchy headline, sub-headline about time saved
3. The 3-phase model (Assessment & Build → Hand-off → Maintenance) -- visual 3-step strip
4. Services grid -- 10 cards, one per category, each links to its sub-page
5. Case study -- Road to 4.0 court availability automation
6. FAQ -- 5-6 common questions (accordion, vanilla JS)
7. CTA section -- Book a Free Strategy Session (repeated)
8. Footer

### Each sub-page structure:
1. Nav (matches site)
2. Hero -- what problem this automation solves, plain language
3. How it works -- 3-phase model applied to this category
4. Services list -- specific automations in this category
5. Who it's for -- 2-3 sentences on the right client
6. FAQ -- 4-5 questions specific to this category (accordion)
7. CTA -- Book a Free Strategy Session (repeated)
8. Footer
9. Back link -- ← Back to AI Automations (in nav or below hero)

---

## Sub-pages and their files

| # | Category | File |
|---|---|---|
| 1 | Lead Capture & Follow-Up | `automations/lead-capture.html` |
| 2 | Appointment & Scheduling | `automations/scheduling.html` |
| 3 | Estimate & Proposal Automation | `automations/proposals.html` |
| 4 | Customer Communication | `automations/customer-communication.html` |
| 5 | Internal Operations & Admin | `automations/operations-admin.html` |
| 6 | Knowledge Base / Second Brain | `automations/knowledge-base.html` |
| 7 | Marketing | `automations/marketing.html` |
| 8 | Reputation & Reviews | `automations/reviews.html` |
| 9 | Reporting & Visibility | `automations/reporting.html` |
| 10 | Competitor Intelligence | `automations/competitor-intelligence.html` |

---

## Task 1: Create the automations/ subdirectory and shared nav snippet

**Files:**
- Create: `automations/` (directory)

**Step 1: Create the directory**
```bash
mkdir "c:/Users/chuck/startuptosold-site/automations"
```

**Step 2: Verify**
```bash
ls "c:/Users/chuck/startuptosold-site/automations"
```
Expected: empty directory, no error.

---

## Task 2: Build the Hub Page (automations.html)

**Files:**
- Modify: `c:\Users\chuck\startuptosold-site\automations.html` (replace placeholder entirely)

**Step 1: Write the full hub page**

Replace the existing placeholder with a full page. Key content:

- **Title:** `AI Automations — Startup to Sold Consulting`
- **Meta description:** `AI automation services for Bay Area businesses. Save hours every week with custom n8n workflows, AI lead capture, scheduling, proposals, marketing, and more.`
- **Canonical:** `https://startuptosold.com/automations`
- **Hero headline:** `Stop Doing It Manually.`
- **Hero sub-headline:** `Custom AI automations that handle lead follow-up, scheduling, proposals, marketing, and more -- built for Bay Area businesses that have better things to do.`
- **CTA:** `Book a Free Strategy Session` → `tel:8585238881`

**3-phase strip content:**
1. Assessment & Build -- "We audit your business for automation opportunities, prioritize by time saved, and build the system."
2. Hand-off -- "We train you and your team on how it works, what to watch, and when to step in."
3. Maintenance -- "Monthly check-ins to keep it running, catch edge cases, and evolve as your business changes."

**Services grid -- 10 cards:**
| Card | Headline | Sub | Link |
|---|---|---|---|
| Lead Capture | Stop losing leads after hours | Auto-respond, follow-up sequences, lead scoring | automations/lead-capture.html |
| Scheduling | Cut no-shows in half | Reminders, waitlist management, post-appointment follow-up | automations/scheduling.html |
| Proposals | Close faster | AI-drafted proposals and estimates in minutes | automations/proposals.html |
| Customer Comms | Keep customers in the loop | FAQ responder, job status updates, re-engagement | automations/customer-communication.html |
| Operations & Admin | Get your time back | Invoice triggers, KPI summaries, meeting autopilot | automations/operations-admin.html |
| Knowledge Base | Stop answering the same questions | Internal knowledge bot, SOP generation | automations/knowledge-base.html |
| Marketing | Marketing that actually gets done | Content creation, repurposing, programmatic SEO | automations/marketing.html |
| Reviews | More 5-star reviews, less manual work | Auto-request, monitor, AI response drafts | automations/reviews.html |
| Reporting | Know your numbers without pulling them | Weekly dashboards, pipeline snapshots | automations/reporting.html |
| Competitor Intel | Know what your competitors are doing | Weekly intelligence brief, review monitoring | automations/competitor-intelligence.html |

**Case study block:**
- Headline: `Real Example: Road to 4.0`
- Body: Use the case study content from AI Services.md -- the problem (checking multiple city platforms manually), what was built (logs in, navigates, pulls availability automatically), what it signals (no official API needed).

**FAQ section content (hub page):**

| Question | Answer |
|---|---|
| Do I need to change my existing software? | Not necessarily. The first step is always an assessment -- we figure out what you're running and whether we can plug into it. Most common tools (Jobber, QuickBooks, Calendly, HubSpot) have integrations we can use. |
| How long does it take to build an automation? | Most automations take 2-4 weeks from assessment to hand-off. More complex systems like the Internal Knowledge Bot or Meeting Autopilot take 4-8 weeks. |
| What if something breaks after you hand it off? | That's what the maintenance phase is for. Monthly check-ins, monitoring, and fixes are included. You're not on your own once we build it. |
| Do I need to be technical to use these? | No. The whole point is that you don't have to be. We build it, train you on how to use it, and document everything. |
| What does it cost? | Every engagement starts with an AI Assessment ($3,500-$5,000) so we can scope the right solution for your business. We don't quote before we understand the problem. |
| Can you automate something not on this list? | Yes. These are the most common use cases -- but if you have a specific problem, book a call and we'll figure it out. |

**Footer content:**
- Left: "Startup to Sold Consulting" + tagline "Hands-on operations leadership for Bay Area businesses."
- Center: links -- Home, AI Automations, Services, About, Contact
- Right: phone (858-523-8881), email (chuck@startuptosold.com)
- Bottom bar: "© 2026 Startup to Sold Consulting. All rights reserved."

**Step 2: Open in browser and verify**

Open `c:/Users/chuck/startuptosold-site/automations.html` in a browser. Check:
- [ ] Nav renders correctly with logo, links, phone
- [ ] Hero is readable and above the fold
- [ ] 3-phase strip is visible
- [ ] All 10 service cards render and links are correct
- [ ] Case study block renders
- [ ] CTA button is orange and visible
- [ ] Mobile: hamburger menu works, cards stack

---

## Tasks 3-12: Build Each Sub-page

Each sub-page follows the same pattern. Build them in this order (easiest/most sellable first):

### Task 3: Lead Capture & Follow-Up (`automations/lead-capture.html`)

**Hero headline:** `Never Miss Another Lead.`
**Hero sub:** `Most businesses lose 50% of leads simply by responding too slowly. We build automations that respond in 60 seconds, follow up for two weeks, and score every lead against your ideal customer profile -- automatically.`

**Services to list:**
- Auto-respond to web form submissions within 60 seconds (SMS + email)
- Follow-up sequences for leads that don't book -- 3-5 touch cadence over 2 weeks
- Missed call text-back
- Lead routing by service type or geography
- Lead qualification: AI scores against ICP, routes high-scorers to CRM or Slack
- Lead generation pipeline: domain list → enrichment → ICP scoring → CRM
- Personalized cold outreach: AI-written openers, reply classification, task creation

**Who it's for:** Service businesses that generate leads online or by phone -- HVAC, construction, home services, professional services. If you've ever missed a lead because you were on a job, this is for you.

**Step 1: Write the file**
**Step 2: Open in browser, verify all sections render, links work**
**Step 3: Verify back link goes to ../automations.html**

---

### Task 4: Appointment & Scheduling (`automations/scheduling.html`)

**Hero headline:** `No-Shows Are Costing You Money.`
**Hero sub:** `A missed appointment is lost revenue and a wasted slot. We automate reminders, follow-ups, and waitlist management so your calendar stays full without manual babysitting.`

**Services:** reminders (24hr + 2hr), post-appointment follow-up and review request, waitlist management for cancelled slots.

**Who it's for:** Any business that takes appointments -- healthcare practices, consultants, home service companies, fitness studios.

---

### Task 5: Estimate & Proposal Automation (`automations/proposals.html`)

**Hero headline:** `Close Faster. Write Less.`
**Hero sub:** `Writing proposals takes hours you don't have. We build systems that generate polished, branded proposals in minutes -- and follow up automatically when they go unread.`

**Services:** auto-generate draft estimates from intake form data, send/track/follow up on open proposals, notify when viewed but not signed, AI proposal writer (intake → past proposals → polished draft in minutes).

**Who it's for:** Contractors, consultants, agencies, and professional services firms that send proposals regularly. If you write more than 5 proposals a month, this pays for itself.

---

### Task 6: Customer Communication (`automations/customer-communication.html`)

**Hero headline:** `Keep Customers in the Loop -- Without Lifting a Finger.`
**Hero sub:** `Customers who feel informed don't call to check in. We automate the updates, follow-ups, and re-engagement campaigns that keep your customers happy and coming back.`

**Services:** AI FAQ responder, job status updates, post-job satisfaction check-in, re-engagement campaigns for past customers.

**Who it's for:** Field service businesses (HVAC, plumbing, construction) and any company with repeat customers worth re-engaging.

---

### Task 7: Internal Operations & Admin (`automations/operations-admin.html`)

**Hero headline:** `Stop Doing Admin. Start Running Your Business.`
**Hero sub:** `Invoice generation, expense tracking, meeting notes, KPI summaries -- all the stuff that eats your evenings. We automate it so it just happens.`

**Services:** invoice generation on job completion, expense categorization from receipts, weekly KPI summary email, meeting transcription + action items, meeting transcript → HubSpot CRM update, Meeting Autopilot (Zoom → Fireflies → Linear/Asana → CRM → follow-up draft).

**Who it's for:** Owner-operators spending evenings on admin. If you're doing invoices at 10pm, this is for you.

---

### Task 8: Knowledge Base / Second Brain (`automations/knowledge-base.html`)

**Hero headline:** `Stop Answering the Same Questions.`
**Hero sub:** `Every time an employee interrupts you with a question someone else already asked, you're paying for a problem that's already solved. We build AI systems that know your business and answer for you.`

**Services:** searchable internal knowledge base from SOPs/emails/docs, Internal Knowledge Bot (Notion/Drive → Supabase → Slack bot), automatic SOP generation from voice memos or Loom recordings.

**Who it's for:** Businesses with 5+ employees where the owner is still the go-to for questions. Also great for teams with high turnover who need faster onboarding.

---

### Task 9: Marketing (`automations/marketing.html`)

**Hero headline:** `Marketing That Actually Gets Done.`
**Hero sub:** `Most small businesses skip marketing not because they don't want to do it -- but because it takes too long. We build systems that do it for you, with you in the loop at every step.`

**Services:** content creation and publishing (human-in-the-loop), content repurposing (one piece → everywhere), programmatic SEO (location/keyword pages at scale).

**Who it's for:** Small businesses that know they should be posting more but never find the time. Also great for businesses in competitive local markets where search visibility matters.

---

### Task 10: Reputation & Reviews (`automations/reviews.html`)

**Hero headline:** `More 5-Star Reviews. Less Manual Work.`
**Hero sub:** `Reviews are the #1 factor in local search rankings. Most businesses know they should be asking for them -- almost none do it consistently. We automate the ask, the monitoring, and the response.`

**Services:** automated Google review request after job close, review monitoring alert, AI response draft suggestions (owner approves before posting).

**Who it's for:** Any local service business that depends on Google Maps visibility -- HVAC, construction, healthcare, home services, professional services.

---

### Task 11: Reporting & Visibility (`automations/reporting.html`)

**Hero headline:** `Know Your Numbers Without Pulling Them.`
**Hero sub:** `Most business owners fly blind between monthly meetings. We build automated dashboards and weekly summaries that land in your inbox -- no logging in, no spreadsheet wrestling.`

**Services:** automated weekly business dashboard via email, sales pipeline snapshot, job/project status rollup for field businesses.

**Who it's for:** Owner-operators who want visibility into their business without spending time pulling data. Especially useful for businesses with field teams or active sales pipelines.

---

### Task 12: Competitor Intelligence (`automations/competitor-intelligence.html`)

**Hero headline:** `Know What Your Competitors Are Doing Before Your Customers Do.`
**Hero sub:** `New pricing. New services. New marketing campaigns. Most businesses find out two weeks late -- after they've already lost customers. We monitor your competitors automatically and deliver a weekly brief.`

**Services:** monitor competitor websites/reviews/social on a schedule, AI analysis for pricing changes/new services/sentiment shifts, weekly intelligence brief to owner's inbox.

**Who it's for:** Local businesses in competitive markets where a competitor's price drop or new service offering could directly affect your revenue. Construction, home services, professional services, healthcare.

---

## Task 13: Final QA Pass

**Step 1: Check all internal links**
- Hub page → all 10 sub-pages
- All sub-pages → back link to automations.html
- All CTA buttons → `tel:8585238881`

**Step 2: Check nav on every page**
- Logo links to `/`
- Nav links match the rest of the site

**Step 3: Mobile check**
- Open each page at 390px width
- Verify hamburger menu, card stacking, hero text size

**Step 4: Verify Google Analytics tag on every page**
- `G-1XV0PEXSQJ` present in head of all 11 pages

**Step 5: Update index.html nav if needed**
- Verify "AI Automations" link in main site nav points to `automations.html`

---

## Notes

- No JS frameworks. Inline CSS only. Keep it consistent with existing pages.
- Phone number everywhere: 858-523-8881 / `tel:8585238881`
- Email: chuck@startuptosold.com
- Don't use em-dashes (house rule) -- use `--` instead
- Industry-specific automations content gets woven into relevant sub-pages as examples, not its own page
- Case study (Road to 4.0) lives on hub page only for now -- add link to live demo once court availability page is built

---

## Design Rule Learnings (from QA session, 2026-04-14)

These rules apply to ALL sub-pages and should be followed in any future page builds or edits.

### Layout

**Flow diagrams: DO NOT BUILD.** Plan called for CSS flow diagrams on each sub-page. First one built for lead-capture.html looked broken on both desktop and mobile (misaligned boxes, ghost elements visible). Cut entirely. Do not add them to future pages.

**Hero mobile padding:** Use `padding: 6rem 1.5rem 3rem` on mobile (not 9rem top). The original 9rem top created a large blank space between hero and next section on 390px.

**Hero mobile stats column:** Remove `padding-top` and `margin-top` on `.hero-stats` at mobile. Use `border-top` instead of `border-left`. Stats had extra top space causing layout gap on mobile.

**Hero mobile grid gap:** Use `gap: 2rem` (not 4-5rem) when hero grid collapses to single column on mobile.

### Typography

**Section lead text max-width:** Always `max-width: 720px` on `.section-lead`. The plan specified `520px`/`540px` -- too narrow. Creates orphaned narrow text under full-width section headings on desktop. Fix: `max-width: 720px` everywhere.

**Stat labels:** Avoid abbreviations that read ambiguously out loud. "2wk" was read as "two weak." Use full words or choose a different stat entirely.

### "Who It's For" section

**Do NOT use two-column layout** (short heading + tall body text). It looks unbalanced. Use single-column intro paragraph + horizontal 3-criteria strip:

```css
.who-body { max-width: 720px; margin-bottom: 2.5rem; }
.who-criteria { display: grid; grid-template-columns: repeat(3, 1fr); border: 1px solid var(--dark-rule); }
.who-criterion { padding: 1.5rem 2rem; border-right: 1px solid var(--dark-rule); display: flex; align-items: flex-start; gap: 1rem; }
.who-criterion:last-child { border-right: none; }
```

Mobile collapse: `grid-template-columns: 1fr`, `border-right: none`, `border-bottom: 1px solid var(--dark-rule)`.

### Services List

Tighter sizing -- the plan's original values were too spacious on mobile:

```css
.service-item { padding: 1.5rem 1.75rem; grid-template-columns: 16px 1fr; gap: 0.75rem; }
.service-dot { width: 7px; height: 7px; margin-top: 0.45rem; }
.service-content-title { font-size: 0.95rem; }
.service-content-desc { font-size: 0.85rem; line-height: 1.6; }
```

### Playwright QA checklist

When doing visual QA:
- Desktop: 1440px viewport
- Mobile: 390px viewport
- Check: hero padding, stats column, section lead text width, "Who It's For" criteria strip, services list sizing
- Save screenshots to `tmp/playwright/filename.png`

# Portfolio Expansion Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add three new portfolio pages (AI Marketing System, Knowledge Base, Morning Operations System) to startuptosold.com, plus update the portfolio grid page with new cards.

**Architecture:** Each portfolio page is a standalone HTML file in `/portfolio/` following the site's dark theme design system (Plus Jakarta Sans, --orange: #e85d26, --dark-bg: #0f1623, etc.). Each page has a unique section structure -- no cookie-cutter layouts. The portfolio grid page (`portfolio.html`) gets three new cards. Each card needs a thumbnail image generated and saved to `/images/portfolio/`.

**Tech Stack:** Static HTML/CSS, Plus Jakarta Sans font, inline styles, no build step. Image generation via Gemini API (for thumbnails/visual assets). Site deployed manually.

**Key Context for Implementer:**
- Read `c:\Users\chuck\Obsidian Vault\Build\Add to Startuptosold\context.md` before starting any page -- it defines what good portfolio pages look like and what to avoid
- Read `c:\Users\chuck\Obsidian Vault\Resources\AI\writing-style-guide.md` before writing any copy (Chuck's voice)
- Each page MUST have unique section layouts -- check the two existing pages (`bushrod-court-scraper.html` and `valuation-calculator.html`) to see how they differ
- No em-dashes in copy (use --)
- Badge categories: "AI Automation", "Knowledge Ops", "Orchestration"
- CTA always links to Calendly: `https://calendly.com/chuck-startuptosold/30min`
- All pages use the same nav, footer, mobile menu, and hamburger JS as existing portfolio pages

---

## Task 1: Generate Visual Assets

**Files:**
- Create: `c:\Users\chuck\startuptosold-site\images\portfolio\marketing-system-thumb.png`
- Create: `c:\Users\chuck\startuptosold-site\images\portfolio\knowledge-base-thumb.png`
- Create: `c:\Users\chuck\startuptosold-site\images\portfolio\morning-ops-thumb.png`

**Step 1: Generate AI Marketing System thumbnail**

Use the image generator at `c:\Users\chuck\Obsidian Vault\Build\Tools\Image Generator\` to create a dark-themed thumbnail (800x400px or similar 2:1 ratio) showing the concept of one input becoming many outputs. Visual concept: a single document/brief on the left with lines fanning out to multiple channel icons (email, social, blog, notification) on the right. Dark background matching site palette (navy/dark blue tones with orange accents).

**Step 2: Generate Knowledge Base thumbnail**

Create a dark-themed thumbnail showing structured knowledge -- interconnected nodes or a clean wiki-like page structure. Visual concept: scattered documents on one side transforming into an organized, linked network on the other. Same dark palette with orange accent highlights.

**Step 3: Generate Morning Operations thumbnail**

Create a dark-themed thumbnail showing a pipeline/orchestration concept. Visual concept: connected operation blocks flowing vertically or a dashboard showing multiple systems unified. Dark palette, orange accents.

**Step 4: Verify all three images saved correctly**

Run: `ls c:/Users/chuck/startuptosold-site/images/portfolio/`
Expected: All three new -thumb.png files present alongside existing ones.

---

## Task 2: Create AI Marketing System Portfolio Page

**Files:**
- Create: `c:\Users\chuck\startuptosold-site\portfolio\ai-marketing-system.html`
- Reference: `c:\Users\chuck\Obsidian Vault\DailyPB\Projects\AI Marketing System\Readme.md` (for system details)
- Reference: `c:\Users\chuck\Obsidian Vault\Resources\AI\writing-style-guide.md` (for voice)

**Step 1: Read reference materials**

Read the AI Marketing System Readme, the writing style guide, and the portfolio context doc. Understand:
- The full pipeline (intake → brief → channel selection → content generation → publishing)
- The technical depth (Bubble API auto-publishing, Gemini image generation, privacy checks)
- Chuck's voice (direct, confident, no jargon, conversational)

**Step 2: Write the HTML page**

Structure (unique to this page -- NOT the same as court scraper or valuation calc):

1. **Hero** (same structural pattern as other pages -- eyebrow, h1, sub, stats sidebar)
   - Eyebrow: "AI Automation"
   - H1: "AI Marketing System" with an orange em-highlighted tagline
   - Sub: Explain the before (writing the same announcement 15 different ways) and after (one brief, full campaign generated). No build-time stat.
   - Stats: 15+ channels / ~4 hrs eliminated per release / One human checkpoint

2. **Section: "The Input vs. The Output"** (unique visual -- side-by-side)
   - Left: styled text block showing a sample feature brief (3-4 lines)
   - Right: grid of small cards showing output channel names with brief excerpts (Instagram, Blog, Email, Help Article, In-App Notification, etc.)
   - This is the "wow" moment -- visual proof of one-to-many

3. **Section: "It Publishes Itself"** (callout section -- unique layout)
   - Highlight that this isn't just a copy generator -- it auto-publishes:
     - Help articles deployed directly to Bubble CMS via API
     - In-app notifications pushed live to users
     - Images generated, hosted, and embedded automatically
   - Use a bordered callout box or highlight panel to emphasize the technical depth
   - Callout box: "It even scans screenshots for real user names and replaces them with fictional ones before generating marketing images. Privacy-safe by default."

4. **Section: "How It Works"** (vertical timeline -- NOT phases strip)
   - 5 steps as stacked cards with connecting lines (CSS border-left on a container):
     1. Intake -- describe feature, system asks questions, checks for screenshots
     2. Core messaging -- one headline/subheadline/description approved
     3. Channel routing -- evaluates every channel, marks active or skip with reasons
     4. Content generation -- reads channel rules, brand voice, image specs, writes everything
     5. Publishing -- auto-deploys where possible, ready-to-paste elsewhere

5. **Section: "The Pattern"** (prose -- same as court scraper's closer)
   - Short: every business ships updates. Most announce them inconsistently or not at all. This system ensures every feature gets full coverage, on-brand, every time.

6. **CTA** (standard site pattern)
   - "Your business ships updates too. How much time does your team spend rewriting the same announcement for every channel?"
   - Calendly button + phone/email

7. **Footer** (identical to other portfolio pages)

**Step 3: Verify page loads correctly**

Open in browser, check: nav works, mobile responsive, no broken images, CTA links work.

**Step 4: Commit**

```bash
git add portfolio/ai-marketing-system.html
git commit -m "feat: add AI Marketing System portfolio page"
```

---

## Task 3: Create Knowledge Base Portfolio Page

**Files:**
- Create: `c:\Users\chuck\startuptosold-site\portfolio\knowledge-base.html`
- Reference: `c:\Users\chuck\Obsidian Vault\Wiki\CLAUDE.md` (for system details)
- Reference: `c:\Users\chuck\Obsidian Vault\Wiki\wiki\index.md` (for real examples)

**Step 1: Read reference materials**

Read the Wiki CLAUDE.md (full schema), the wiki index (to see real pages created), and a sample source page to understand what the system actually produces. Also read the writing style guide.

**Step 2: Write the HTML page**

Structure (unique to this page):

1. **Hero**
   - Eyebrow: "Knowledge Ops"
   - H1: "Knowledge Base" with orange em-highlight
   - Sub: Books, transcripts, strategy conversations, competitor research -- all go into one folder. The system reads, structures, cross-references, and makes it queryable. Months later, ask a question, get a cited answer.
   - Stats: 11+ sources ingested / 40+ pages auto-generated / Instant cited answers

2. **Section: "Before and After"** (full-width split -- different from court scraper's before/after)
   - Left ("Before"): styled as scattered items -- "podcast transcript sitting in Downloads," "book highlights in an app you'll never open again," "that conversation you had three months ago that had the perfect framework." The problem: knowledge that's technically saved but practically lost.
   - Right ("After"): clean structure showing entities, concepts, cross-references. The system makes everything findable and connected.

3. **Section: "What Happens When You Drop a File In"** (real example walkthrough)
   - Pick a real ingested source (e.g., $100M Offers or a strategy conversation)
   - Show: source summary created → entity pages created/updated → concept pages created/updated → cross-references added → index updated → log entry filed
   - Layout: numbered list with indented detail, or a compact card per output type

4. **Section: "Ask It Anything"** (query examples)
   - 2-3 real-style queries and what the system returns:
     - "What did [source] say about pricing models?" → cited answer with [[wikilinks]]
     - "Compare the positioning frameworks from these two sources" → synthesis with citations
   - Style: code-block-ish display for queries, prose display for answers

5. **Section: "It's a Git Repo. It Goes Anywhere."**
   - Short prose: syncs to cloud, queryable by other tools, can be deployed for a team. Not locked into one app.
   - This is the "for your business" pivot: "I built this for myself. I can build one for your team -- your SOPs, your market research, your vendor evaluations, all structured and queryable."

6. **CTA**
   - "Your company's knowledge is scattered. What if every document, every conversation, every meeting actually made your team smarter -- permanently?"
   - Calendly button + phone/email

7. **Footer** (identical)

**Step 3: Verify page loads correctly**

**Step 4: Commit**

```bash
git add portfolio/knowledge-base.html
git commit -m "feat: add Knowledge Base portfolio page"
```

---

## Task 4: Create Morning Operations System Portfolio Page

**Files:**
- Create: `c:\Users\chuck\startuptosold-site\portfolio\morning-operations.html`
- Reference: `C:\Users\chuck\.claude\skills\start-the-day\prompt.md` (for system details)
- Reference: `C:\Users\chuck\.claude\skills\gtd-triage\` (for GTD triage details)

**Step 1: Read reference materials**

Read the start-the-day skill, the GTD triage skill, and the writing style guide. Understand the full orchestration: calendar sync, archiving, email cleanup, day-specific ops, GTD triage, exercise scheduling.

**Step 2: Write the HTML page**

Structure (unique to this page):

1. **Hero**
   - Eyebrow: "Orchestration"
   - H1: "Morning Operations System" with orange em-highlight
   - Sub: Lead with the CLIENT value, not "here's my morning." Something like: "What if your team's first hour was productive instead of administrative? One command handles calendar sync, email triage, task routing, and daily operations -- so the day starts with a plan, not a scramble."
   - Stats: 5 accounts synced / ~25 min/day saved / Zero manual steps

2. **Section: "What This System Does"** (pipeline visual -- unique to this page)
   - NOT a timeline or phases strip. Vertical pipeline of connected "operation blocks."
   - Each block: dark card with a short bold title and 1-2 sentence description.
   - Connected with thin vertical lines (CSS pseudo-elements or border-left on a wrapper).
   - Blocks:
     1. Archive & Build -- yesterday archived, today created from 5 calendars, unchecked tasks carry forward
     2. Email Cleanup -- noise trashed, errors summarized by type, only signal remains
     3. Day-Specific Ops -- Monday: spam reports processed + apology drafts created. Friday: events email auto-drafted.
     4. GTD Triage -- voice captures from iPhone parsed and routed into projects with next actions defined
     5. Exercise Scheduling -- gym classes booked, conflicts detected, recovery blocks added

3. **Section: "Voice Capture to Structured Task"** (callout/highlight)
   - Zoom in on the GTD triage as a standout feature:
   - "Throughout the day, I capture tasks by voice on my phone. Next morning, the system pulls them from email, parses them, and routes each one to the right project with a defined next action. No inbox processing. No manual sorting."
   - This is the most relatable piece for any busy operator.

4. **Section: "The Real Point"** (prose, client-facing)
   - Short and punchy: "This isn't about my morning. It's about yours. Or your ops manager's. Or your team lead who spends 30 minutes every day getting oriented before they can do real work. Calendar syncing, email triaging, task sorting -- all of it can be one command. Custom-built for whatever YOUR daily operations look like."

5. **CTA**
   - "What does your team's first hour look like? If it involves checking, syncing, sorting, or triaging -- I can make it disappear."
   - Calendly button + phone/email

6. **Footer** (identical)

**Step 3: Verify page loads correctly**

**Step 4: Commit**

```bash
git add portfolio/morning-operations.html
git commit -m "feat: add Morning Operations System portfolio page"
```

---

## Task 5: Update Portfolio Grid Page

**Files:**
- Modify: `c:\Users\chuck\startuptosold-site\portfolio.html`

**Step 1: Add three new portfolio cards to the grid**

After the existing two cards (valuation-calculator and bushrod-court-scraper), add three new cards:

Card 3: AI Marketing System
```html
<a href="portfolio/ai-marketing-system.html" class="portfolio-card reveal">
  <div class="card-image" style="background-image: url('images/portfolio/marketing-system-thumb.png')"></div>
  <div class="card-body">
    <div class="card-badge">AI Automation</div>
    <h3 class="card-title">AI Marketing System</h3>
    <p class="card-desc">One feature brief in. Fifteen channels of on-brand marketing content out -- blog, email, social, help docs, in-app notifications. Some channels auto-publish themselves.</p>
    <span class="card-link">View details &rarr;</span>
  </div>
</a>
```

Card 4: Knowledge Base
```html
<a href="portfolio/knowledge-base.html" class="portfolio-card reveal">
  <div class="card-image" style="background-image: url('images/portfolio/knowledge-base-thumb.png')"></div>
  <div class="card-body">
    <div class="card-badge">Knowledge Ops</div>
    <h3 class="card-title">Knowledge Base</h3>
    <p class="card-desc">Drop a book, transcript, or strategy conversation into a folder. Get structured, cross-referenced, queryable intelligence back -- with cited answers months later.</p>
    <span class="card-link">View details &rarr;</span>
  </div>
</a>
```

Card 5: Morning Operations System
```html
<a href="portfolio/morning-operations.html" class="portfolio-card reveal">
  <div class="card-image" style="background-image: url('images/portfolio/morning-ops-thumb.png')"></div>
  <div class="card-body">
    <div class="card-badge">Orchestration</div>
    <h3 class="card-title">Morning Operations System</h3>
    <p class="card-desc">Five accounts synced, emails triaged, voice captures routed, gym booked -- all before coffee. Custom-built for whatever YOUR daily ops look like.</p>
    <span class="card-link">View details &rarr;</span>
  </div>
</a>
```

**Step 2: Verify grid renders correctly**

Open portfolio.html in browser. Confirm:
- 5 cards display in 3-column grid (desktop), 2-column (tablet), 1-column (mobile)
- All thumbnails load
- All links point to correct pages
- Reveal animations fire on scroll

**Step 3: Commit**

```bash
git add portfolio.html
git commit -m "feat: add 3 new cards to portfolio grid"
```

---

## Task 6: Create Portfolio Draft Docs in Obsidian

**Files:**
- Create: `c:\Users\chuck\Obsidian Vault\Build\Add to Startuptosold\ai-marketing-system.md`
- Create: `c:\Users\chuck\Obsidian Vault\Build\Add to Startuptosold\knowledge-base.md`
- Create: `c:\Users\chuck\Obsidian Vault\Build\Add to Startuptosold\morning-operations.md`

**Step 1: Create draft files using the portfolio piece template from context.md**

For each piece, fill in: Card headline, one-liner, card image path, what it is, problem it solves, how it works, result, live demo status.

**Step 2: Commit Obsidian vault changes**

```bash
cd "c:/Users/chuck/Obsidian Vault"
git add "Build/Add to Startuptosold/"
git commit -m "docs: add portfolio drafts for 3 new pieces"
```

---

## Task 7: Final QA and Screenshots

**Step 1: Take screenshots of each page for verification**

Use Playwright to navigate to each page (via local file or dev server) and capture full-page screenshots. Save to `tmp/playwright/`.

**Step 2: Verify each page against the portfolio context rules**

Check against `Build/Add to Startuptosold/context.md`:
- [ ] Each page has a unique layout (no cookie-cutter)
- [ ] Framing is "look what I can build" not "here's what this tool does for you"
- [ ] No jargon -- language a business owner understands
- [ ] CTA connects to Calendly
- [ ] Mobile responsive (check at 375px width)
- [ ] No em-dashes (use --)

**Step 3: Final commit if any fixes needed**

---

## Execution Order

Tasks 1-4 can be partially parallelized:
- Task 1 (images) should run first since Tasks 2-5 reference the thumbnails
- Tasks 2, 3, 4 (individual pages) are independent of each other
- Task 5 (grid update) depends on Tasks 2-4 being complete
- Task 6 (Obsidian drafts) is independent, can run anytime
- Task 7 (QA) runs last

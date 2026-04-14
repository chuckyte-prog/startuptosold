# Exit Readiness Assessment Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a self-contained `assessment.html` lead-gen page that scores owner-dependency across 12 questions, reveals a score and pillar breakdown, then gates a dollar valuation reveal behind name + email capture, with a Calendly CTA.

**Architecture:** Single static HTML file matching the existing `index.html` design system exactly. All CSS inline. No build step, no external JS libraries. Scoring and valuation logic in vanilla JS. Lead capture uses a simple `mailto:` or `fetch` to a form endpoint (FormSubmit.co free tier — no backend needed).

**Tech Stack:** HTML, CSS (inline, matching brand guide), vanilla JavaScript, Formspree (`https://formspree.io/f/xaqplpgv`) for lead email delivery — same service already used on `index.html`.

---

## Reference: Scoring System

**Questions (12 total, grouped by pillar):**

Each question is phrased so that **Yes = owner is the bottleneck = 1 point of dependency**.

**Pillar 1: Administrative Logic & Gatekeeping**
1. Does pricing rely on your personal judgment rather than a documented, repeatable formula?
2. Is your lead-to-cash process (invoicing, follow-up) handled manually by you?
3. Are you the one dispatching staff or setting appointments?

**Pillar 2: Personnel & Operations**
4. Do your SOPs exist mainly as "tribal knowledge" rather than documented, enforced processes?
5. Do staff or customer disputes typically require your involvement to resolve?
6. Could you train a new operator without being personally involved in the process?  *(Note: No = 1 point — rephrase for scoring clarity, see Task 2)*

**Pillar 3: The Vacation Test**
7. Would your business experience revenue loss or operational failure if you were unreachable for 48 hours?
8. Do you personally hold all passwords, bank access, and key vendor contacts?
9. Is there no clear decision-maker when you are unavailable?

**Pillar 4: Financial & Data Transparency**
10. Can an outsider NOT view your P&L, lead volume, and staff efficiency without calling you?
11. Does any single client represent more than 15% of your revenue?
12. Are personal expenses mixed into your business financials?

**Score → Multiple mapping:**
| Score | Label | Current Multiple (midpoint) | Target Multiple |
|---|---|---|---|
| 8-12 | High Dependency | 1.85x | 4.0x |
| 4-7 | Operational Hybrid | 2.85x | 4.0x |
| 1-3 | Turnkey Asset | 4.0x | 4.0x |
| 0 | Turnkey Asset | 4.0x | 4.0x |

**Lead capture fields:** First Name, Email, SDE (dollar input), Bottleneck (optional textarea)

**Formspree endpoint:** `https://formspree.io/f/xaqplpgv` (same as contact form on index.html)

---

## Task 1: Scaffold the HTML file with nav and hero

**Files:**
- Create: `C:\Users\chuck\startuptosold-site\assessment.html`

**Step 1: Create the file with doctype, head, and nav**

Copy the exact head block from `index.html` (fonts, favicon, CSS variables). Change the title to `Exit Readiness Assessment — Startup to Sold`. Add the same `<nav>` with logo linking back to `index.html` and a "Book a Call" nav-cta linking to `https://calendly.com/chuck-startuptosold`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Exit Readiness Assessment — Startup to Sold</title>
  <meta name="description" content="Find out if your business is sellable — or just a job. The free 12-question Exit Readiness Assessment by Chuck Temple." />
  <link rel="icon" type="image/svg+xml" href="favicon.svg" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
  <style>
    /* --- paste full :root and base styles from index.html --- */
    /* --- add assessment-specific styles below --- */
  </style>
</head>
<body>
  <nav>
    <a href="/" class="nav-logo">Startup to Sold</a>
    <div style="display:flex;gap:2rem;align-items:center;">
      <a href="https://calendly.com/chuck-startuptosold" class="nav-cta" target="_blank" rel="noopener">Book a Call</a>
    </div>
  </nav>
  <!-- sections go here -->
</body>
</html>
```

**Step 2: Add hero section**

Below the nav, add a `<section class="assessment-hero">` with:
- Section label: `— The Assessment`
- `<h1>`: "Is your business <em>sellable</em> — or just a job?"
- Subhead (`.hero-sub`): "Answer 12 questions about your operations. See your Dependency Score and what it means for your exit valuation."
- No buttons — the quiz is immediately below

```html
<section class="assessment-hero">
  <div class="section-inner" style="padding-top:9rem;padding-bottom:5rem;">
    <div class="section-label">— The Assessment</div>
    <h1 style="font-family:'Cormorant Garamond',serif;font-size:clamp(2.6rem,5vw,4rem);font-weight:300;line-height:1.12;letter-spacing:-0.01em;max-width:700px;margin-bottom:1.5rem;">
      Is your business <em>sellable</em> — or just a job?
    </h1>
    <p class="hero-sub" style="max-width:520px;">
      Answer 12 questions about your operations. See your Dependency Score and what it means for your exit valuation.
    </p>
  </div>
</section>
```

**Step 3: Verify the file opens in a browser with correct nav and hero**

Open `assessment.html` in browser. Confirm fonts load, gold accent on `em`, section label pattern matches `index.html`.

**Step 4: Commit**

```bash
cd C:\Users\chuck\startuptosold-site
git add assessment.html docs/plans/2026-03-25-exit-readiness-assessment.md
git commit -m "feat: scaffold assessment page with nav and hero"
```

---

## Task 2: Build the 12-question quiz section

**Files:**
- Modify: `C:\Users\chuck\startuptosold-site\assessment.html`

**Step 1: Add quiz section HTML**

Add a `<section class="section-light" id="quiz">` after the hero. Inside, render 4 pillar groups. Each group has a pillar heading and 3 questions. Each question is a Yes/No toggle using `<button>` elements (not radio inputs — buttons are easier to style on-brand).

Structure per question:
```html
<div class="question" data-question="1">
  <p class="question-text">Does pricing rely on your personal judgment rather than a documented formula?</p>
  <div class="answer-group">
    <button class="answer-btn" data-value="1" onclick="selectAnswer(this)">Yes</button>
    <button class="answer-btn" data-value="0" onclick="selectAnswer(this)">No</button>
  </div>
</div>
```

Note: Question 6 ("Could you train a new operator without being personally involved?") must be **inverted** — "No" = 1 point (dependency). Handle this with `data-value="0"` on "Yes" and `data-value="1"` on "No" for that question only.

**Step 2: Add CSS for pillar headings and answer buttons**

```css
.quiz-pillar {
  margin-bottom: 3.5rem;
}

.pillar-heading {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.5rem;
  font-weight: 400;
  color: var(--ink);
  margin-bottom: 2rem;
  padding-bottom: 0.75rem;
  border-bottom: 1px solid var(--rule);
}

.pillar-number {
  font-size: 0.82rem;
  font-weight: 500;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 0.4rem;
}

.question {
  margin-bottom: 2rem;
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 2rem;
  align-items: center;
  padding: 1.5rem 0;
  border-bottom: 1px solid var(--rule);
}

.question-text {
  font-size: 1rem;
  font-weight: 400;
  color: #4a4540;
  line-height: 1.65;
}

.answer-group {
  display: flex;
  gap: 0.5rem;
}

.answer-btn {
  font-family: 'DM Sans', sans-serif;
  font-size: 0.82rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 0.65rem 1.25rem;
  border: 1px solid var(--rule);
  background: transparent;
  color: var(--muted);
  cursor: pointer;
  transition: background 0.15s, color 0.15s, border-color 0.15s;
}

.answer-btn:hover {
  border-color: var(--ink);
  color: var(--ink);
}

.answer-btn.selected-yes {
  background: var(--ink);
  color: var(--cream);
  border-color: var(--ink);
}

.answer-btn.selected-no {
  background: var(--gold);
  color: var(--ink);
  border-color: var(--gold);
}
```

**Step 3: Add "See My Score" button**

After all 4 pillar groups, add:
```html
<div style="margin-top:3rem;text-align:center;">
  <p id="quiz-error" style="color:#c0392b;font-size:0.9rem;margin-bottom:1rem;display:none;">Please answer all 12 questions before continuing.</p>
  <button class="btn-primary" onclick="calculateScore()" style="font-size:0.9rem;letter-spacing:0.1em;">See My Score</button>
</div>
```

**Step 4: Add `selectAnswer()` JS function**

```javascript
function selectAnswer(btn) {
  const group = btn.closest('.answer-group');
  group.querySelectorAll('.answer-btn').forEach(b => {
    b.classList.remove('selected-yes', 'selected-no');
  });
  const value = parseInt(btn.dataset.value);
  btn.classList.add(value === 1 ? 'selected-yes' : 'selected-no');
  btn.dataset.selected = 'true';
}
```

**Step 5: Verify in browser**

Click each Yes/No button. Confirm Yes = dark/ink selected state, No = gold selected state. Confirm buttons deselect each other within a group.

**Step 6: Commit**

```bash
git add assessment.html
git commit -m "feat: add 12-question quiz with yes/no toggles"
```

---

## Task 3: Score calculation and pillar breakdown reveal

**Files:**
- Modify: `C:\Users\chuck\startuptosold-site\assessment.html`

**Step 1: Add score results section HTML (hidden initially)**

After the quiz section, add a `<section id="results" style="display:none;">` with:
- Score display (large Cormorant Garamond number)
- Classification label (High Dependency / Operational Hybrid / Turnkey Asset)
- 4 pillar score bars
- Brief interpretation copy

```html
<section id="results" class="section-cream" style="display:none;">
  <div class="section-inner">
    <div class="section-label">— Your Results</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:start;margin-top:2rem;">
      <div>
        <div id="score-display" style="font-family:'Cormorant Garamond',serif;font-size:6rem;font-weight:300;line-height:1;color:var(--ink);"></div>
        <div id="score-label" style="font-size:0.82rem;font-weight:500;letter-spacing:0.16em;text-transform:uppercase;color:var(--gold);margin-bottom:1rem;"></div>
        <p id="score-copy" style="font-size:1rem;color:#4a4540;line-height:1.75;max-width:400px;"></p>
      </div>
      <div id="pillar-breakdown"></div>
    </div>
  </div>
</section>
```

**Step 2: Add `calculateScore()` JS function**

```javascript
const PILLARS = [
  { name: 'Administrative Logic', questions: [1, 2, 3] },
  { name: 'Personnel & Operations', questions: [4, 5, 6] },
  { name: 'The Vacation Test', questions: [7, 8, 9] },
  { name: 'Financial Transparency', questions: [10, 11, 12] },
];

function calculateScore() {
  const questions = document.querySelectorAll('.question');
  let answered = 0;
  let scores = {};

  questions.forEach(q => {
    const qNum = parseInt(q.dataset.question);
    const selected = q.querySelector('.answer-btn[data-selected="true"]');
    if (selected) {
      answered++;
      scores[qNum] = parseInt(selected.dataset.value);
    }
  });

  if (answered < 12) {
    document.getElementById('quiz-error').style.display = 'block';
    return;
  }

  document.getElementById('quiz-error').style.display = 'none';

  const total = Object.values(scores).reduce((a, b) => a + b, 0);

  let label, multiple, copy;
  if (total >= 8) {
    label = 'High Dependency';
    multiple = 1.85;
    copy = 'Your business is heavily owner-dependent. Buyers see this as risk and price accordingly — typically 1.5x to 2.2x SDE. The gap between where you are and where you could be is significant.';
  } else if (total >= 4) {
    label = 'Operational Hybrid';
    multiple = 2.85;
    copy = 'Your business has some systems in place but still relies on you in key areas. Strategic buyers will offer 2.5x to 3.2x SDE — better, but still well below institutional multiples.';
  } else {
    label = 'Turnkey Asset';
    multiple = 4.0;
    copy = 'Your business operates with minimal owner dependency. You are in the top tier for exit multiples — 3.5x to 4.5x SDE. If you\'re not already talking to buyers, you should be.';
  }

  document.getElementById('score-display').textContent = total;
  document.getElementById('score-label').textContent = label;
  document.getElementById('score-copy').textContent = copy;

  // Pillar breakdown
  const breakdownEl = document.getElementById('pillar-breakdown');
  breakdownEl.innerHTML = '';
  PILLARS.forEach(pillar => {
    const pillarScore = pillar.questions.reduce((acc, q) => acc + (scores[q] || 0), 0);
    const pct = (pillarScore / 3) * 100;
    breakdownEl.innerHTML += `
      <div style="margin-bottom:1.75rem;">
        <div style="display:flex;justify-content:space-between;margin-bottom:0.4rem;">
          <span style="font-size:0.9rem;font-weight:500;color:var(--ink);">${pillar.name}</span>
          <span style="font-size:0.9rem;color:var(--muted);">${pillarScore}/3</span>
        </div>
        <div style="height:4px;background:var(--rule);width:100%;">
          <div style="height:4px;background:${pct >= 67 ? 'var(--ink)' : pct >= 34 ? 'var(--gold)' : 'var(--gold-light)'};width:${pct}%;transition:width 0.6s ease;"></div>
        </div>
      </div>
    `;
  });

  // Store for valuation section
  window._assessmentScore = { total, multiple };

  // Show results and scroll
  const resultsEl = document.getElementById('results');
  resultsEl.style.display = 'block';
  setTimeout(() => resultsEl.scrollIntoView({ behavior: 'smooth', block: 'start' }), 100);
}
```

**Step 3: Verify in browser**

Answer all 12 questions, click "See My Score". Confirm score (0-12) displays, label matches score range, pillar bars render correctly. Test with 0, 5, and 10 answers to verify all three classifications.

**Step 4: Commit**

```bash
git add assessment.html
git commit -m "feat: add score calculation and pillar breakdown reveal"
```

---

## Task 4: Valuation gate section (lead capture)

**Files:**
- Modify: `C:\Users\chuck\startuptosold-site\assessment.html`

**Step 1: Add valuation gate HTML**

After the results section, add a dark section (matching `section-dark` from `index.html`) with the SDE input + lead form. This section is always visible once results are shown.

```html
<section id="valuation-gate" class="section-dark" style="display:none;">
  <div class="section-inner">
    <div class="section-label" style="color:var(--gold);">— What This Means in Dollars</div>
    <h2 style="color:var(--dark-text);max-width:600px;margin-bottom:1rem;">
      Enter your SDE to see <em>your valuation gap</em>
    </h2>
    <p style="font-size:1rem;font-weight:300;color:var(--dark-muted);max-width:480px;margin-bottom:3rem;line-height:1.8;">
      SDE (Seller's Discretionary Earnings) is your business profit plus your owner salary and any personal expenses run through the business. Enter your best estimate.
    </p>

    <form id="lead-form" onsubmit="submitLead(event)" style="max-width:480px;">
      <input type="hidden" id="hidden-score" name="Dependency Score" value="" />
      <input type="hidden" id="hidden-label" name="Score Label" value="" />

      <div style="margin-bottom:1.5rem;">
        <label style="display:block;font-size:0.82rem;font-weight:500;letter-spacing:0.1em;text-transform:uppercase;color:var(--dark-muted);margin-bottom:0.6rem;">Annual SDE</label>
        <div style="position:relative;">
          <span style="position:absolute;left:1rem;top:50%;transform:translateY(-50%);color:var(--dark-muted);font-size:1rem;">$</span>
          <input type="number" id="sde-input" name="Annual SDE" min="0" step="1000" placeholder="250000"
            style="width:100%;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.12);color:var(--dark-text);font-family:'DM Sans',sans-serif;font-size:1rem;padding:0.9rem 1rem 0.9rem 2.25rem;" required />
        </div>
      </div>

      <div style="display:grid;grid-template-columns:1fr 1fr;gap:1rem;margin-bottom:1.5rem;">
        <div>
          <label style="display:block;font-size:0.82rem;font-weight:500;letter-spacing:0.1em;text-transform:uppercase;color:var(--dark-muted);margin-bottom:0.6rem;">First Name</label>
          <input type="text" name="First Name" placeholder="Sarah"
            style="width:100%;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.12);color:var(--dark-text);font-family:'DM Sans',sans-serif;font-size:1rem;padding:0.9rem 1rem;" required />
        </div>
        <div>
          <label style="display:block;font-size:0.82rem;font-weight:500;letter-spacing:0.1em;text-transform:uppercase;color:var(--dark-muted);margin-bottom:0.6rem;">Email</label>
          <input type="email" name="email" placeholder="you@company.com"
            style="width:100%;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.12);color:var(--dark-text);font-family:'DM Sans',sans-serif;font-size:1rem;padding:0.9rem 1rem;" required />
        </div>
      </div>

      <div style="margin-bottom:2rem;">
        <label style="display:block;font-size:0.82rem;font-weight:500;letter-spacing:0.1em;text-transform:uppercase;color:var(--dark-muted);margin-bottom:0.6rem;">Biggest Operational Bottleneck <span style="font-weight:300;text-transform:none;letter-spacing:0;">(optional)</span></label>
        <textarea name="Biggest Bottleneck" rows="3" placeholder="e.g. Everything runs through me — I haven't taken a real vacation in 3 years"
          style="width:100%;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.12);color:var(--dark-text);font-family:'DM Sans',sans-serif;font-size:1rem;padding:0.9rem 1rem;resize:vertical;"></textarea>
      </div>

      <button type="submit" style="background:var(--gold);color:var(--ink);font-family:'DM Sans',sans-serif;font-size:0.9rem;font-weight:500;letter-spacing:0.1em;text-transform:uppercase;padding:1.1rem 2.5rem;border:none;cursor:pointer;transition:background 0.2s,transform 0.15s;width:100%;">
        Show My Valuation
      </button>
    </form>
  </div>
</section>
```

**Step 2: Show valuation gate after results**

In `calculateScore()`, after showing results, also show the valuation gate:
```javascript
document.getElementById('valuation-gate').style.display = 'block';
// Pre-fill hidden fields
document.getElementById('hidden-score').value = total;
document.getElementById('hidden-label').value = label;
```

**Step 3: Verify form renders correctly**

Open browser. Complete quiz, click "See My Score". Confirm dark section appears with SDE input, name, email, optional textarea, and gold submit button.

**Step 4: Commit**

```bash
git add assessment.html
git commit -m "feat: add valuation lead capture form on dark section"
```

---

## Task 5: Valuation results reveal

**Files:**
- Modify: `C:\Users\chuck\startuptosold-site\assessment.html`

**Step 1: Add valuation results HTML (hidden initially)**

After the valuation gate section, add a light section for the dollar reveal:

```html
<section id="valuation-results" class="section-light" style="display:none;">
  <div class="section-inner">
    <div class="section-label">— Your Valuation Gap</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:center;margin-top:2rem;">

      <div>
        <div style="margin-bottom:2.5rem;padding-bottom:2.5rem;border-bottom:1px solid var(--rule);">
          <div style="font-size:0.82rem;font-weight:500;letter-spacing:0.1em;text-transform:uppercase;color:var(--muted);margin-bottom:0.5rem;">Your Business Today</div>
          <div id="val-current" style="font-family:'Cormorant Garamond',serif;font-size:3.5rem;font-weight:300;color:var(--ink);line-height:1;"></div>
          <div id="val-current-note" style="font-size:0.9rem;color:var(--muted);margin-top:0.4rem;"></div>
        </div>
        <div>
          <div style="font-size:0.82rem;font-weight:500;letter-spacing:0.1em;text-transform:uppercase;color:var(--gold);margin-bottom:0.5rem;">Optimized Exit Value</div>
          <div id="val-optimized" style="font-family:'Cormorant Garamond',serif;font-size:3.5rem;font-weight:300;color:var(--ink);line-height:1;"></div>
          <div id="val-optimized-note" style="font-size:0.9rem;color:var(--muted);margin-top:0.4rem;"></div>
        </div>
      </div>

      <div style="background:var(--cream);padding:2.5rem;border:1px solid var(--rule);">
        <div style="font-size:0.82rem;font-weight:500;letter-spacing:0.1em;text-transform:uppercase;color:var(--muted);margin-bottom:0.5rem;">Potential Value Created</div>
        <div id="val-gap" style="font-family:'Cormorant Garamond',serif;font-size:4rem;font-weight:300;color:var(--gold);line-height:1;margin-bottom:1rem;"></div>
        <p id="val-gap-copy" style="font-size:1rem;color:#4a4540;line-height:1.75;"></p>
      </div>

    </div>

    <!-- CTA -->
    <div style="margin-top:5rem;padding-top:3rem;border-top:1px solid var(--rule);text-align:center;">
      <div class="section-label" style="justify-content:center;">— Ready to Close the Gap?</div>
      <h2 style="font-family:'Cormorant Garamond',serif;font-size:clamp(2rem,4vw,3rem);font-weight:300;line-height:1.2;margin:1rem auto 1.5rem;max-width:600px;">
        Let's build the operations that make your business <em>worth more</em>.
      </h2>
      <a href="https://calendly.com/chuck-startuptosold" target="_blank" rel="noopener" class="btn-primary" style="display:inline-flex;align-items:center;margin-top:0.5rem;">
        Book a Free 30-Minute Call
      </a>
    </div>
  </div>
</section>
```

**Step 2: Add `submitLead()` JS function**

```javascript
function submitLead(event) {
  event.preventDefault();

  const sde = parseFloat(document.getElementById('sde-input').value);
  if (!sde || sde <= 0) return;

  const { multiple } = window._assessmentScore;
  const currentVal = sde * multiple;
  const optimizedVal = sde * 4.0;
  const gap = optimizedVal - currentVal;

  const fmt = (n) => '$' + Math.round(n).toLocaleString('en-US');

  document.getElementById('val-current').textContent = fmt(currentVal);
  document.getElementById('val-current-note').textContent = `${multiple}x SDE — current market rate for your dependency score`;
  document.getElementById('val-optimized').textContent = fmt(optimizedVal);
  document.getElementById('val-optimized-note').textContent = `4.0x SDE — institutional-grade, managed asset`;
  document.getElementById('val-gap').textContent = fmt(gap);
  document.getElementById('val-gap-copy').textContent = gap > 0
    ? `That's the equity being left on the table. We build the systems that close this gap — and make your business 100% bankable for SBA financing.`
    : `Your business is already at the top multiple. Let's make sure your exit is structured to capture it.`;

  // Show valuation results
  const valEl = document.getElementById('valuation-results');
  valEl.style.display = 'block';
  setTimeout(() => valEl.scrollIntoView({ behavior: 'smooth', block: 'start' }), 100);

  // Submit to Formspree (same endpoint as index.html contact form)
  const form = document.getElementById('lead-form');
  const formData = new FormData(form);
  formData.append('_subject', 'New Exit Readiness Assessment Lead');
  fetch('https://formspree.io/f/xaqplpgv', {
    method: 'POST',
    body: formData,
    headers: { 'Accept': 'application/json' }
  }).catch(() => {}); // silent fail — results already shown to user
}
```

**Step 3: Verify full flow in browser**

Complete quiz → See score → Fill form → Submit → Confirm valuation numbers are mathematically correct for several test cases:
- SDE $200,000, score 10 (High Dep, 1.85x): current=$370,000, optimized=$800,000, gap=$430,000
- SDE $200,000, score 5 (Hybrid, 2.85x): current=$570,000, optimized=$800,000, gap=$230,000
- SDE $200,000, score 2 (Turnkey, 4.0x): current=$800,000, optimized=$800,000, gap=$0

**Step 4: Commit**

```bash
git add assessment.html
git commit -m "feat: add valuation reveal and CTA section"
```

---

## Task 6: Mobile responsiveness and polish

**Files:**
- Modify: `C:\Users\chuck\startuptosold-site\assessment.html`

**Step 1: Add mobile media query**

```css
@media (max-width: 768px) {
  nav { padding: 1.25rem 1.5rem; }
  .assessment-hero .section-inner { padding-left: 1.5rem; padding-right: 1.5rem; }
  .section-light, .section-cream, .section-dark { padding: 4rem 1.5rem; }
  .question { grid-template-columns: 1fr; gap: 1rem; }
  .answer-group { justify-content: flex-start; }
  #results .section-inner > div,
  #valuation-results .section-inner > div { grid-template-columns: 1fr; gap: 2rem; }
  #lead-form > div[style*="grid-template-columns:1fr 1fr"] { grid-template-columns: 1fr; }
  #val-gap { font-size: 3rem; }
}
```

**Step 2: Add index.html link to assessment**

In `index.html`, find the hero actions section and add a secondary link to the assessment page. Look for `.hero-actions` — add after the existing CTA:

```html
<a href="/assessment" class="btn-secondary">Take the Free Assessment</a>
```

**Step 3: Test mobile at 375px and 768px**

Open browser dev tools, resize to 375px. Confirm:
- Questions stack vertically (text above Yes/No buttons)
- Form fields stack to single column
- Valuation numbers don't overflow
- Nav stays readable

**Step 4: Final commit**

```bash
git add assessment.html index.html
git commit -m "feat: add mobile styles and link assessment from homepage"
```

---

## Task 7: Deploy and verify live

**Step 1: Push to GitHub**

```bash
cd C:\Users\chuck\startuptosold-site
git push
```

**Step 2: Wait ~30 seconds for Cloudflare Pages auto-deploy**

**Step 3: Verify live at `startuptosold.com/assessment`**

- Complete the full flow end-to-end on the live site
- Check that the FormSubmit.co email arrives at chuck@startuptosold.com
  - Note: FormSubmit.co requires a one-time email confirmation on first submission. Click the confirm link when it arrives.
- Confirm Calendly link opens correctly

**Step 4: Done**

---

## Formspree Notes

- Same account/endpoint already used on index.html contact form — no new setup needed
- Endpoint: `https://formspree.io/f/xaqplpgv`
- Each lead email will include: First Name, Email, Annual SDE, Dependency Score, Score Label, Biggest Bottleneck
- The `_subject` field sets the email subject line in Formspree

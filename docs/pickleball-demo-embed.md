# Pickleball Court Availability Demo — Embed Instructions

## What It Is

A live AI automation demo hosted at `https://web-production-1d80d.up.railway.app`.
Visitors pick a date and see real-time availability for Bushrod Tennis Court in Oakland.
Built to embed on the AI Automations page (`automations.html`) as a proof of concept.

## How to Embed (iframe)

Add this HTML block wherever you want it to appear in `automations.html`:

```html
<iframe
  src="https://web-production-1d80d.up.railway.app"
  width="100%"
  height="620"
  style="border: none; display: block;"
  title="Live Pickleball Court Availability Demo"
  loading="lazy"
></iframe>
```

Wrap it in a section with a label if you want context around it:

```html
<section style="margin: 3rem 0;">
  <div style="font-size: 0.72rem; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; color: var(--orange); margin-bottom: 0.75rem;">
    Live Demo
  </div>
  <h3 style="font-size: 1.35rem; font-weight: 800; margin-bottom: 0.5rem;">
    Oakland Pickleball Court Availability
  </h3>
  <p style="font-size: 0.92rem; color: var(--dark-muted); margin-bottom: 1.25rem;">
    Pick a date and see real-time court availability scraped live from the city portal.
    This is the kind of tool we build for clients.
  </p>
  <iframe
    src="https://web-production-1d80d.up.railway.app"
    width="100%"
    height="620"
    style="border: none; display: block;"
    title="Live Pickleball Court Availability Demo"
    loading="lazy"
  ></iframe>
</section>
```

## Railway Hosting

- **URL:** `https://web-production-1d80d.up.railway.app`
- **Repo:** `github.com/chuckyte-prog/pickleball-booking-demo`
- **Cost:** ~$5/month on Railway free tier (30-day credit, then pay-as-you-go)
- **Credentials:** Oakland PerfectMind login stored in Railway environment variables (never in code)

## Updating the Demo

Any push to the `master` branch of `pickleball-booking-demo` triggers an auto-deploy on Railway.

To make changes:
1. Edit files in `C:\Users\chuck\pickleball-demo\`
2. `git add . && git commit -m "your message" && git push`
3. Railway deploys automatically

## Key Files

| File | Purpose |
|------|---------|
| `api.py` | FastAPI backend, handles requests, queues scrapes |
| `court_agent.py` | Playwright scraper for Oakland PerfectMind portal |
| `static/index.html` | The UI visitors see |
| `Dockerfile` | Uses `mcr.microsoft.com/playwright/python:v1.58.0-jammy` |

## Notes

- Scrape takes ~30 seconds — progress bar is shown during wait
- One scrape at a time (asyncio lock) — concurrent visitors queue
- 90-second timeout — users always get a result or error
- `HEADLESS=true` is set in Railway env vars so Chrome runs invisibly on the server

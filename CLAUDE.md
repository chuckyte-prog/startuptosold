# Startup to Sold — Site Notes

## Google Analytics

Measurement ID: **G-1XV0PEXSQJ**

Every HTML page must include the GA4 snippet in the `<head>`, before the font preconnect links:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-1XV0PEXSQJ"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-1XV0PEXSQJ');
</script>
```

When creating any new page, add this snippet. Current pages that have it:
- `index.html`
- `assessment.html`

## Deployment

Cloudflare Pages — auto-deploys on push to `main` branch of GitHub repo.

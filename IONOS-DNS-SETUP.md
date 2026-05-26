# IONOS DNS — One step to go live

Add a single CNAME record at IONOS to make `assets.romain-leroux.racing` resolve to your GitHub Pages site.

## The record

| Field | Value |
|---|---|
| **Type** | CNAME |
| **Host name** | `assets` |
| **Points to** | `romainlrx171-ui.github.io` |
| **TTL** | default (3600s) |

## Where to add it in IONOS

1. Log in → **Domains & SSL** → click `romain-leroux.racing`
2. **DNS** tab → **Add record**
3. Select **CNAME**
4. Host name = `assets`  (just the word `assets`, not the full domain)
5. Points to = `romainlrx171-ui.github.io` (no trailing dot, no https)
6. Save

## After saving

- DNS propagation: 5-30 min (occasionally up to a few hours)
- GitHub will auto-issue an HTTPS certificate once DNS resolves (15 min - 24h after propagation)
- Until HTTPS is live, the URL works over HTTP only — fine for testing, do NOT send cold emails until HTTPS is live

## Verify it's working

After ~15 min, run:

```bash
curl -I https://assets.romain-leroux.racing/bd-platform.pdf
```

Expected: `HTTP/2 200`. If you get a 404 from GitHub Pages, DNS propagated but Pages cert isn't ready — wait. If you get DNS resolution failure, propagation isn't done yet.

## Fallback URL while waiting

Both PDFs are already live at:
- `https://romainlrx171-ui.github.io/sponsor-assets/bd-platform.pdf`
- `https://romainlrx171-ui.github.io/sponsor-assets/spa-24h.pdf`

You can use these temporarily if you need to send the link before DNS+HTTPS is ready, but they reveal the GitHub origin — better to wait for the custom domain.

## Once live, the two canonical URLs are

- `https://assets.romain-leroux.racing/bd-platform.pdf`
- `https://assets.romain-leroux.racing/spa-24h.pdf`

These are already wired into:
- `outreach-engine/scripts/lib/assets.py` (single source of truth)
- `outreach-engine/scripts/05_morning_briefing.py` (printed at top of every morning briefing)
- `outreach-engine/README.md` (handoff doc)

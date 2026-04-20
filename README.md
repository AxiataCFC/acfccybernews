# ACFC Cyber Intelligence Feed
**Axiata Cyber Fusion Center — SOC Wall Display**

A live cybersecurity news feed designed for SOC wall screens. Pulls from 5 open-source intelligence feeds and auto-classifies articles by severity. No backend required — runs entirely in the browser.

---

## Live Sources

| Source | Type | Feed |
|--------|------|------|
| The Hacker News | General cyber news | RSS via rss2json |
| Bleeping Computer | Incidents & malware | RSS via rss2json |
| CISA Advisories | Official US govt alerts | RSS via rss2json |
| Krebs on Security | Investigations & breaches | RSS via rss2json |
| SANS ISC | Daily handlers diary | RSS via rss2json |

---

## Hosting on GitHub Pages

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Under **Source**, select `Deploy from a branch`
4. Select branch: `main`, folder: `/ (root)`
5. Click **Save**
6. Your URL will be: `https://<your-username>.github.io/acfc-soc-display/`

Point the SOC screen browser to that URL and press **F11** for full-screen kiosk mode.

---

## Adding the ACFC Logo

**Option A — Click to upload (live, no code edit needed):**
Open the page in a browser. Click the dashed logo box in the top-left. Select your logo image file. It will display immediately. Note: this resets on page refresh.

**Option B — Permanent embed (recommended):**
1. Drop your logo file into this repo folder (e.g. `acfc_logo.png`)
2. Open `index.html` and find this comment:
   ```
   <!-- LOGO PLACEHOLDER — replace with your logo image or swap this block -->
   ```
3. Replace the entire `<div class="logo-placeholder">...</div>` block with:
   ```html
   <img src="acfc_logo.png" alt="ACFC Logo" style="height:38px;object-fit:contain;">
   ```
4. Push to GitHub — done.

---

## Configuration

All configurable values are at the top of the `<script>` block in `index.html`:

```javascript
const REFRESH_MS = 15 * 60 * 1000;  // Refresh interval (default: 15 minutes)
```

To add or remove sources, edit the `SOURCES` array:
```javascript
const SOURCES = [
  { id:'THN', name:'The Hacker News', color:'#ff3c3c', url:'https://feeds.feedburner.com/TheHackersNews' },
  // add more here
];
```

---

## How Severity Classification Works

Articles are automatically tagged Critical / High / Medium / Low based on keyword matching in the title and description:

- **Critical**: zero-day, actively exploited, ransomware attack, nation-state, APT, data breach
- **High**: vulnerability, exploit, malware, phishing, backdoor, supply chain
- **Medium**: advisory, patch, security update, threat actor
- **Low**: everything else

---

## Known Dependency

This page uses [rss2json.com](https://rss2json.com) as a CORS proxy to fetch RSS feeds from the browser. It is a free third-party service.

**If feeds stop loading:** check rss2json.com availability. As a fallback, the page will show a retry button. A future upgrade path is to replace rss2json with an Azure Function that fetches RSS server-side.

---

## Maintained By

- Primary: Rafaya (ACFC)
- Technical Support: Rafa Islam Diba, Ahmad Ahnaf Bin Masdi

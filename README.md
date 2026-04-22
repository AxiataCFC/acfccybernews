# ACFC SOC Wall — Sentinel Prototype
**Axiata Cyber Fusion Center · 5-Screen SOC Display Prototype**

A fully simulated Microsoft Sentinel-style SOC wall prototype. Fake data throughout — designed to demonstrate what the real implementation would look like before committing to KQL + Sentinel workbooks.

---

## Pages

| File | Screen | Description |
|------|--------|-------------|
| `index.html` | Left (big screen) | 6-panel overview: threat map, alert timeline, KPIs, attack countries, attack types, SOC health |
| `incidents.html` | Screen 1 | Active incidents, triage queue, incident detail, MITRE ATT&CK |
| `executive.html` | Screen 2 | Executive dashboard: security score, monthly trends, top users at risk |
| `vulnerability.html` | Screen 3 | CVE list, risky assets, patch coverage (Tenable-style) |
| `intel.html` | Screen 4 | Live threat intel feed (RSS), IOCs, breaking news ticker |

---

## Hosting on GitHub Pages

1. Push repo to GitHub
2. **Settings → Pages → Deploy from branch → main → / (root)**
3. Your URL: `https://<username>.github.io/acfc-soc-wall/`

### Custom Domain (soc.axiatacfc.com)
1. Add `CNAME` file to repo with content: `soc.axiatacfc.com`
2. GitHub Pages Settings → Custom domain → enter `soc.axiatacfc.com`
3. Ask DNS admin to add: `CNAME  soc  →  <username>.github.io`
4. Enable "Enforce HTTPS" in GitHub Pages settings

---

## Adding the ACFC Logo

Each page has a dashed `[ LOGO ]` placeholder in the top-left.

**Temporary (demo use):** Click the placeholder — it accepts any image file upload.

**Permanent:** 
1. Add your logo file to the repo (e.g. `acfc_logo.png`)
2. In each HTML file, find `<div class="topbar-logo-placeholder"...>` and replace the whole block with:
```html
<img src="acfc_logo.png" alt="ACFC" style="height:28px;object-fit:contain;">
```

---

## Displaying on SOC Screens

Open each page in Chrome and press **F11** for fullscreen kiosk mode.

Recommended: use Chrome's `--kiosk` flag for auto-start:
```
chrome.exe --kiosk "https://soc.axiatacfc.com/index.html"
```

For 5 screens, open one tab per screen and drag each to its physical monitor.

---

## Real Implementation Path

When ready to replace fake data with live Sentinel:

| Prototype element | Real Sentinel replacement |
|---|---|
| Hardcoded alert counts | KQL: `SecurityAlert \| summarize count() by AlertSeverity` |
| Fake incident list | Sentinel Incidents blade or custom KQL workbook |
| Static CVE table | Tenable.io connector + KQL query on `TenanbleIO_Assets` |
| RSS news feed | Keep as-is — this is already real live data |
| World map | Sentinel built-in Workbook: "Microsoft Sentinel — Maps" |
| Security score | Direct embed from Microsoft Secure Score API |

---

## Maintained By
- **Lead:** Rafaya (ACFC)  
- **Technical Support:** Rafa Islam Diba · Ahmad Ahnaf Bin Masdi

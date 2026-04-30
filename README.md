# ACFC SOC Wall — Sentinel Prototype v2
**Axiata Cyber Fusion Center · Analyst-first SOC Display**

Rebuilt based on L1/L2 analyst feedback. Defensive monitoring tool, not a reporting tool.

---

## Pages

| File | Screen | Purpose |
|------|--------|---------|
| `index.html` | Left (big screen) | 6-panel security overview — for anyone walking in |
| `incidents.html` | Screen 1 | **Exploit Movement Tracker** — MITRE kill chain live progression, alert correlation |
| `edr.html` | Screen 2 | **EDR/XDR Volume Monitor** — Defender + CrowdStrike baselines, drop-off detection |
| `acta.html` | Screen 3 | **ACTA Weekly Feed** — Cyber Threat Activity bulletins, OpCo associations |
| `intel.html` | Screen 4 | **Threat Intel Feed** — Live RSS from SANS, CISA, THN, Krebs, Bleeping Computer |

---

## Design Philosophy
- Screens 1–4: analyst-facing, reactive, monitoring-first
- Left screen: balanced — readable by visitors, useful to analysts passively
- No duplicating what's on analyst laptops — wall = awareness + anomaly detection

---

## Real Implementation Path

| Prototype element | Real Sentinel / automation replacement |
|---|---|
| MITRE kill chain stages | Sentinel KQL: `SecurityIncident \| extend tactics = TacticName` |
| EDR volume baseline | KQL: `SecurityAlert \| where ProviderName == "MDATP" \| summarize count() by bin(TimeGenerated, 1h)` |
| CrowdStrike drop detection | Logic App: alert if hourly count < 30% of 7-day avg |
| ACTA bulletin feed | Power Automate: read Outlook/SharePoint → push to JSON → GitHub |
| Alert correlation | Sentinel Fusion rules + KQL correlation workbook |
| Silent endpoint detection | KQL: `Heartbeat \| summarize lastHB=max(TimeGenerated) by Computer \| where lastHB < ago(2h)` |

---

## Hosting
1. Push to GitHub repo
2. Settings → Pages → Deploy from main / (root)
3. Custom domain: add `CNAME` → `axiatacfc.com`
4. DNS: `CNAME soc → <username>.github.io`

## Maintained By
- Lead: Rafa Islam Diba
- Technical Support: Rafa Islam Diba · Ahmad Ahnaf Bin Masdi · Afeefah

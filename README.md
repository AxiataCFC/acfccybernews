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

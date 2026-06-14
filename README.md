# Email & URL Threat Analyzer

An AI-powered security tool that scans emails and URLs for phishing, lookalike domains, alarming language, and harmful URL patterns. No installation needed — runs entirely in the browser from a single HTML file.

---

## Two versions

| Version | File | AI Model | Cost |
|---|---|---|---|
| **Anthropic (Claude)** | `threat-analyzer.html` | Claude Sonnet 4 | ~$0.002–$0.005 per scan (BYOK) |
| **Google Gemini (Free)** | `threat-analyzer-gemini.html` | Gemini 2.5 flash | Free (up to 15 req/min) |

> **BYOK** = Bring Your Own Key. Each user provides their own API key. It never touches any server other than the respective AI provider.

---

## What it detects

### Email scanning — 8 categories
| Category | What it checks |
|---|---|
| Sender spoofing | Display name vs actual email address mismatch |
| Lookalike domains | Typosquatting (paypa1.com), homoglyph attacks (g00gle.com), brand+keyword combos |
| Alarming language | Urgency phrases, threats, fear tactics ("act now", "24 hours", "suspended") |
| Harmful URLs | Links where text and destination don't match, login paths on non-brand domains |
| Header anomalies | SPF/DKIM/DMARC failures, forged Received headers, reply-to mismatches |
| Brand impersonation | Fake PayPal, Microsoft, Apple, Amazon, bank, and government emails |
| Attachment references | .exe, .zip, .iso, macro-enabled .doc, password-protected archives |
| Credential harvesting | Requests for passwords, card numbers, OTPs, SSNs |

### URL scanning — 8 categories
| Category | What it checks |
|---|---|
| Lookalike domains | Typosquatting, homoglyphs, brand+keyword combos (apple-id-verify.com) |
| Subdomain abuse | Brand used as subdomain of attacker domain (paypal.attacker.com) |
| Harmful paths | /login /verify /confirm /update /suspend on non-brand domains |
| Protocol issues | Plain HTTP for sensitive pages, non-standard ports |
| Redirectors | URL shorteners, open redirect parameters (?url=, ?goto=) |
| Obfuscation | %XX encoding of brand names, excessive URL length, unicode tricks |
| Suspicious params | ?token= ?session= ?email= pre-filled targeting |
| IP-based URLs | Raw IP addresses instead of domain names |

---

## How to use

### Free version (Gemini)
1. Open `https://abhijithkris0101.github.io/Threat-Analyzer/` in any browser
2. Get a free API key from [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey) — no credit card needed
3. Paste the key into the tool and click Save
4. Paste an email or URL and hit Scan

### Anthropic version (Claude)
1. Open `https://abhijithkris0101.github.io/Threat-Analyzer/` in any browser
2. Get an API key from [console.anthropic.com](https://console.anthropic.com)
3. Paste the key into the tool and click Save
4. Paste an email or URL and hit Scan

---

## How it works

```
User pastes email/URL
        │
        ▼
Tool builds a detailed prompt
(lists all 8 detection categories
 and tells AI to return JSON)
        │
        ▼
Prompt sent to AI API
(Gemini or Claude)
        │
        ▼
AI returns structured JSON
{ risk_level, threat_score,
  categories, findings,
  iocs, recommendations }
        │
        ▼
Tool animates the checklist
and renders results on screen
```

**Why JSON?** Forcing the AI to reply in JSON (instead of plain sentences) means the tool can reliably read and display each field — risk level, score, per-category results — without any parsing guesswork.

**Why two separate prompts for email vs URL?** Each type of threat works differently. Emails have headers, sender fields, and embedded links. URLs have domains, paths, and query parameters. Separate rule sets mean more accurate, relevant results for each.

---

## Tech stack

- Pure HTML, CSS, JavaScript — zero dependencies, zero build step
- [Tabler Icons](https://tabler.io/icons) for UI icons (loaded via CDN)
- Google Gemini-2.5-flash API or Anthropic Claude Sonnet 4 API
- localStorage for API key persistence (browser-only, never transmitted elsewhere)
- XSS protection on all rendered content via HTML escaping

---

## Repository structure

```
threat-analyzer/
│
├── threat-analyzer.html          # Claude (Anthropic) version — BYOK
├── threat-analyzer-gemini.html   # Gemini-2.5-flash version — free tier
└── README.md                     # This file
```

---

## Security & privacy

- API keys are stored only in your browser's localStorage
- No backend server — the tool communicates directly with the AI provider
- All rendered content is HTML-escaped to prevent XSS attacks
- Email/URL content is sent only to the chosen AI provider for analysis

---

## Free tier limits (Gemini version)

| Limit | Amount |
|---|---|
| Requests per minute | 15 |
| Tokens per day | 1,000,000 |
| Cost | Free |

For most personal or portfolio use, these limits are more than sufficient.

---

## Local development

No setup required. Just open either HTML file directly in a browser:

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/threat-analyzer.git

# Open in browser
open threat-analyzer-gemini.html
```

---

Peace out!! :)

------------------------- THE END ---------------------------

# Support Ticket Triage & Reply Assistant

A small, single-page web tool that takes a raw customer support message and instantly:

- **Categorizes** it (Billing, Integration/SSO, Bug, How-to, Account/Access)
- **Assigns a priority** (P1 / P2 / P3) with a short reason
- **Reads the tone** (Neutral / Frustrated)
- **Drafts a suggested reply** that a support engineer reviews and edits before sending
- **Outputs the parsed ticket as structured JSON**

It runs fully in the browser — no backend, no login, no data leaves the page.

**Live demo:** _(add your GitHub Pages link here after publishing)_

---

## Why I built this

I work in SaaS customer support, so I built the kind of tool I would actually want on my own desk. When many tickets come in at once, the slow part is often the first 30 seconds: *what is this about, how urgent is it, and where do I start the reply?* This tool does that first pass automatically, so the human can spend their time solving the problem instead of sorting it.

I designed it as a **human-in-the-loop** assistant on purpose: the tool suggests, the person decides. Every draft reply is editable, and nothing is ever sent automatically. That mirrors how AI should work in support — accelerating the human, not replacing them.

## How it works

The logic is intentionally simple and readable:

1. The message text is lower-cased and scanned against keyword rule-sets for each category; the best-matching category wins.
2. Priority is decided by urgency signals (e.g. "urgent", "whole team", "payroll", "down") for P1, and technical/billing-impact words for P2, otherwise P3.
3. A light sentiment check flags frustrated customers so the reply opens with more empathy.
4. A reply is drafted from a template chosen by category, then combined with the tone-aware opening.
5. The parsed result is shown as JSON, the same shape a real integration would pass to another system.

## How I "vibe-coded" it

I built this with AI assistance (my normal workflow): I described the problem and the behavior I wanted in plain English, iterated on the design and the rules with the AI, then read through, tested, and adjusted the code myself until it did exactly what I intended. I understand every part of it and can extend it.

## Tech

Plain **HTML, CSS, and JavaScript** — no frameworks, no dependencies. One file, loads instantly, works offline.

## How I'd extend it

- Swap the keyword classifier for a real **AI model / MCP tool** call, keeping the human-in-the-loop review step.
- Pull tickets in from a helpdesk (Zendesk / Intercom) via **API** instead of paste.
- Learn from the edits agents make to the drafts, so suggestions improve over time.

---

_Built by Md. Jahidul Islam Hemel — Technical Support Engineer (SaaS & Shopify)._

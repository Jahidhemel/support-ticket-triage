# Efoli Support Assistant — Triage, Docs & Human Handoff

A small, single-page web tool that reads a customer support message and decides the right next step:

- **Detects the app** the customer is asking about (PushBundle, MultiVariants, DiscountRay, OrderRules, Embed App)
- **Categorizes** the message and assigns a **priority** (P1 / P2 / P3) with a reason
- **Reads the tone** (Neutral / Frustrated)
- **Answers from the knowledge base** when it finds a confident match — with a source and confidence level
- **Routes to the right human** when it shouldn't auto-answer — billing to the Billing team, bugs to Engineering, upset customers to Senior support, and anything unclear to General support — with an internal handoff note and a holding reply for the customer
- **Outputs the whole decision as JSON**

It runs fully in the browser — no backend, no login, no data leaves the page.

**Live demo:** https://jahidhemel.github.io/support-ticket-triage/

---

## Why I built this

I work in SaaS customer support, so I built the kind of tool I'd actually want on my desk. Good support isn't just fast replies — it's getting each message to the *right* place: deflect the common questions with clear documentation, and make sure the sensitive or technical ones reach a human quickly. This tool does exactly that first pass.

It's **human-in-the-loop by design**: the assistant only *suggests*. A support engineer reviews every reply, and anything sensitive, technical, or unclear is routed to a person instead of auto-answered.

## How the routing works

For each message the tool runs a simple decision flow:

1. If the customer asks for a person → **human handoff** (General support).
2. If they ask "are you human or AI?" → an **honest auto-answer** (no ticket needed).
3. Greetings / thank-yous → a friendly **auto-reply**.
4. If the customer sounds frustrated → **Senior support** (people, not bots, for upset customers).
5. If it's a bug / technical issue → **Engineering / Tier-2**, with a request for repro steps.
6. If it's a billing dispute or refund → **Billing team**.
7. If there's a confident match in the knowledge base → **auto-answer from docs**, with the source.
8. Otherwise → **General support**, asking for a bit more detail.

## How I "vibe-coded" it

I built this with AI assistance (my normal workflow): I described the behavior I wanted in plain English, iterated on the knowledge base and the routing rules with the AI, then read through, tested with real-style messages, and fixed the logic myself. For example, an early version drafted a "duplicate charge" reply for a cancellation refund — I caught it during testing and rewrote the logic so it doesn't assume. That review step is the whole point.

## A note on the knowledge base

The knowledge-base entries are **representative sample content** for Efoli's Shopify apps — enough to demonstrate the doc-deflection flow. In a real deployment these would be replaced with the actual help-center articles (or fetched from the help center via API).

## Tech

Plain **HTML, CSS, and JavaScript** — no frameworks, no dependencies. One file, loads instantly, works offline.

## How I'd extend it

- Swap the keyword classifier and KB match for a real **AI model / MCP tool**, keeping the human review step.
- Pull articles live from the **help center** and tickets from the helpdesk (Zendesk / Intercom) via **API**.
- Learn from the edits agents make to drafts, so both the answers and the routing improve over time.

---

_Built by Md. Jahidul Islam Hemel — Technical Support Engineer (SaaS & Shopify)._

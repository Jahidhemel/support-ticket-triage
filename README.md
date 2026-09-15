# eFoli Support Assistant — AI chat with human handoff

An interactive support chat (single web page) that answers customer questions from **eFoli's real help docs**, asks follow-up questions, and hands off to a human when it should. Built around eFoli's Shopify apps: **PushBundle, MultiVariants, DiscountRay, QuotWay, OrderRules**.

**Live demo:** https://jahidhemel.github.io/support-ticket-triage/

It runs fully in the browser — no backend, no login, no data leaves the page.

---

## What it does

The customer chats; the assistant responds turn by turn. For every message it:

- **Detects the app** the customer is asking about (and remembers it across the conversation).
- **Classifies** the message (category, priority, tone).
- **Answers from the knowledge base** when it finds a confident match — the KB content is taken from eFoli's public docs and FAQs (e.g. *"a customer-specific DiscountRay discount needs the shopper to be signed in — it won't resolve at guest checkout"*), and it shows the **source doc** and **confidence**.
- **Asks a follow-up** ("Did that solve it?"). If the customer says it didn't, it **escalates to a human**.
- **Routes to the right team** when it shouldn't auto-answer: **Billing** for refunds, **Engineering** for bugs, **Senior support** for upset customers, **General support** when someone asks for a person or it's unclear.
- Shows all of this in a **"behind the scenes" reasoning panel** (detected app, routing decision, matched article, confidence, and the full JSON).

## Why I built it

I work in eFoli support, so I built the kind of assistant I'd actually want on the front line: deflect the common, well-documented questions instantly, and get everything sensitive or unclear to the right human fast — without ever guessing.

It's **human-in-the-loop by design**: the assistant only *suggests*. A support engineer reviews replies, and it never auto-answers billing, bugs, upset customers, or anything it isn't confident about.

## Example flows to try

- *"How do I install DiscountRay?"* → answers from docs, detects DiscountRay.
- *"My discount is not applying at checkout"* → gives the real guest-checkout / sign-in answer, then asks if it's solved.
- Reply *"still not working"* → escalates to a support engineer.
- *"How do I change the widget colour?"* → design guidance (Custom CSS / Display Style), offers a human for custom work.
- *"I want a refund, charged twice"* → routes to the Billing team.
- *"Can I talk to a human?"* → routes to a support engineer.

## How I "vibe-coded" it

I researched eFoli's real product docs and FAQs, described the conversation and routing behaviour I wanted in plain English, built the knowledge base and rules with AI, then tested it turn by turn and fixed the logic myself. For example, an early version assumed a "duplicate charge" for a *cancellation* refund — I caught it in testing and rewrote the logic so it doesn't assume. That review step is the whole point.

## A note on the knowledge base

The KB is built from eFoli's **public** docs and FAQs — enough to demonstrate accurate, doc-grounded answers. In a real deployment it would read the live help center (or an internal doc store) via API, and the keyword matching would be replaced with a real AI model / MCP tool, keeping the human review step.

## Tech

Plain **HTML, CSS, and JavaScript** — no frameworks, no dependencies. One file, loads instantly, works offline.

---

_Built by Md. Jahidul Islam Hemel — Technical Support Engineer, eFoli (SaaS & Shopify)._

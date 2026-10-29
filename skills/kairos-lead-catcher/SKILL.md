---
name: kairos-lead-catcher
description: Catch after-hours leads for a trade or service business. Use when the user runs a contracting, trade, or local service business and wants inquiries that arrive after hours — or while the crew is mid-job — captured, answered fast with an approved draft, and flagged to the owner instead of going cold.
---

# After-Hours Lead Catcher

Trades and services lose jobs when calls and texts go unanswered after
hours or mid-job. This catcher captures each inquiry, triages its
urgency, drafts the first response, and prepares an owner
notification — so the lead gets a fast, human-approved reply instead
of silence.

The work that matters — activation and licence checks, intake
validation, urgency triage, draft assembly, notification prep — runs
on the hosted service this plugin connects to. This package is the
thin client: keep the `state` value from every tool result and pass
it back unchanged on the next call.

## How a session runs

1. **Activate once.** Call `lead_catcher_activate` with the business
   profile: business name, trade, owner first name (optional),
   after-hours window (optional, default 17:00–08:00), and average
   job value (optional — used only for the labelled estimate in the
   summary). If the user has a licence key, pass it as `licenceKey`;
   without one the session runs in trial mode with a small lead
   limit. Keep the returned `state`.
2. **Capture each inquiry.** When the user tells you about an
   after-hours or missed inquiry — a call, text, web form, email, or
   voicemail — call `lead_catcher_capture` with the caller's name,
   callback contact, channel, and their message in their own words.
   Add `serviceNeeded` and `receivedAt` when known.
3. **Show the draft, always.** The tool returns a first-response
   draft and an owner notification payload. Present the draft to the
   user for approval. **A person sends every message** — never send,
   submit, or deliver anything on the user's behalf.
4. **Move the lead.** Use `lead_catcher_update` as things progress:
   `mark_contacted` once the reply goes out, `draft_followup` for a
   follow-up draft, `escalate` when the owner needs to step in (it
   returns an escalation payload), `mark_booked`, `mark_closed`.
5. **Summarise.** `lead_catcher_summary` returns counts by status
   and priority, the lead list, and — when an average job value was
   supplied — a recovery figure. That figure is an **ESTIMATE, not a
   guarantee**: say so every time you present it.

## Urgency

Leads whose wording signals an emergency (burst pipe, no heat, gas,
flooding, sparking) come back flagged `urgent`, and their draft tells
the caller to reach emergency services first if anyone is at risk.
Surface urgent leads to the user immediately — don't let them sit in
a summary.

## Hard rules

- **Drafts only.** You never send messages, place calls, or submit
  forms as part of this flow. The user approves and sends.
- **Never promise a remedy.** No draft, summary, or reply may offer
  or imply a refund, discount, credit, free work, or compensation —
  and never edit a draft to add one. Pricing and remedies are the
  owner's call, made in person.
- **Never guarantee outcomes.** The recovery figure is a labelled
  estimate based on the business's own inputs and a benchmark
  assumption. Present it as an estimate, every time.
- **Never invent lead details.** Capture only what the user or the
  inquiry actually says. If a field is unknown, leave it out — never
  guess a name, number, or message.
- If a tool call errors (expired or invalid session state, trial
  limit reached), say so plainly and offer to re-activate — don't
  paper over it.

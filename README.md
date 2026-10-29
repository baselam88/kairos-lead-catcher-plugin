# After-Hours Lead Catcher — plugin for Grok Bot, Cursor, and MCP hosts

**What it does.** Catches the leads a trade or service business loses
when calls and texts go unanswered after hours or mid-job. For each
inquiry, the catcher captures the details, triages the urgency,
drafts a first response for a person to approve and send, and
prepares an owner notification. Urgent wording (burst pipe, no heat,
gas, flooding) is flagged immediately, and the draft tells the caller
to reach emergency services first if anyone is at risk.

**Why it matters.** A 5-person trade shop missing ~3 inbound
inquiries a week at an average job value of ~$800 (trade benchmark)
could recover an estimated **~$4,800/mo** by responding to 50% of
them. **ESTIMATE — not a guarantee.** Your session summary computes
the same estimate from your own average job value and the leads you
actually captured.

**Drafts only, by design.** Nothing is ever sent automatically. A
person reviews and sends every message, and no draft ever offers a
refund, discount, credit, or other remedy — pricing and remedies stay
the owner's call, made in person.

**Tools**

| Tool | Label | What it does |
|---|---|---|
| `lead_catcher_activate` | Write | Validates the business profile and licence key, opens a session (trial mode without a key) |
| `lead_catcher_capture` | Write | Captures one after-hours lead; returns a first-response draft + owner notification payload |
| `lead_catcher_update` | Write | Moves a lead: contacted, follow-up draft, escalate, booked, closed |
| `lead_catcher_summary` | Read | Session counts, lead list, and the labelled recovery ESTIMATE |

**Configure variables.** None to install. Activation takes your
business profile in chat; a licence key is optional (without one,
sessions run in trial mode with a small lead limit).

**Privacy.** The service stores nothing. Your session — business
profile and captured leads — travels between calls inside a signed
token your own agent carries. Lead details are used only to draft
the responses and notifications you asked for, and nothing is sent
anywhere on your behalf.

## Test locally

The package points at the hosted endpoint in `mcp.json`. To exercise
the tools from any MCP client, add the server from `mcp.json` and ask
your agent to "set up the After-Hours Lead Catcher for my business".

Cursor IDE local load:

```bash
ln -s /path/to/kairos-lead-catcher ~/.cursor/plugins/local/kairos-lead-catcher
```

Then reload the window and confirm the `kairos-lead-catcher` skill
and MCP server load.

## Submit

- Grok Bot / Cursor marketplace: https://x.ai/bot/marketplace/submit-a-plugin
- License: MIT (see LICENSE) — the plugin package is open; the
  lead-catcher service itself is hosted by KAIROS AI Systems.

Built by KAIROS AI Systems — https://kairosasi.com

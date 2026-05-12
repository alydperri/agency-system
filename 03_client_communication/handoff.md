# Handoff: Client Communication

See `HANDOFF_PROTOCOL.md` for the standard packet shape and field definitions.

---

## How I Receive Work

I receive Handoff Packets from:
- **00_orchestrator** — standalone communication requests
- **01_lead_qualifier** — new lead ready for first outreach
- **02_property_research** — research complete, agent needs to communicate findings
- **04_transaction_coordinator** — transaction milestone reached or client check-in needed
- **05_quality_review** — draft returned with revision notes (loop back)

## Minimum Required Inputs

- Agent name (required — I write in their voice)
- Agent voice profile `voice/<agent-name>.md` (required — if it doesn't exist, stop and request it)
- Client name (required when known — if unknown, draft naturally without it)
- Situation type (required — shapes structure and tone entirely)
- Situation-specific voice notes (optional — modify the profile for this message only)
- Research or context to include, if applicable
- Channel: email or text (ask if not specified)

## What I Produce

A **draft communication** ready for agent review. Every draft includes:
- The message, formatted for the channel
- An agent note explaining the key drafting judgment

I do not produce final messages. I produce drafts.

### Agent Note Format
```
**Agent note:**
[1–2 sentences: what should the agent understand before reviewing or sending this?
Cover tone choice, channel reasoning, omitted details, risk handling, or call-to-action judgment.
Not a disclaimer. The judgment behind the draft in plain language.]
```

## Standard Outgoing Handoff Packet → 05_quality_review

Every draft passes to quality review in this format:

```
## Draft Review Packet

- from:                    03_client_communication
- to:                      05_quality_review
- client_name:             [Who is this message for?]
- agent_name:              [Who is this message from?]
- channel:                 [Email / Text]
- situation_type:          [First outreach / Post-showing / Competing offer / Inspection / Financing delay / Check-in / Other]
- intended_outcome:        [What should the client do or feel after reading this?]
- relationship_context:    [Referral, existing client, cold inquiry, etc.]
- voice_profile_used:      [Which voice/<agent-name>.md was loaded]
- draft:                   [The message]
- agent_note:              [The drafting judgment note]
- known_risks:             [Anything sensitive, legally adjacent, or easy to misread]
- quality_review_required: Yes
- escalation_needed:       [Yes / No]
```

## Where I Pass Work

**Every draft goes to 05_quality_review before returning to the agent. No exceptions.**

| Destination | When |
|---|---|
| 05_quality_review | Every draft, every time |
| 04_transaction_coordinator | Communication reveals a transaction milestone or action item needing tracking |
| 00_orchestrator | The request contains something that changes the nature of the overall task |

## When I Loop Backward

**From 05_quality_review:** When a draft comes back with "Revise with notes," I revise and resubmit to quality review. The loop closes when the draft is approved. I do not return revised drafts to the agent without a quality review pass.

**From any source:** If a revision request requires information I don't have — new context, updated voice notes, missing client details — I flag what's needed before revising rather than guessing.

## When I Escalate to Diana

- The situation involves delivering genuinely bad news (deal falling through, major inspection finding, financing failure)
- The client has expressed significant frustration or distress in previous communication
- The message involves a legal or financial implication the agent isn't sure how to phrase

# HANDOFF_PROTOCOL.md

This file is the single source of truth for how work moves through this system. Every specialist receives work in a structured Handoff Packet and produces one when passing work forward. The packet shape is defined here. Individual specialists define their own inputs, outputs, and routing logic in their `handoff.md` files — but they all use this packet.

Two root contracts govern this system:
- `DIANA_STANDARD.md` — the quality bar every output is held to
- `HANDOFF_PROTOCOL.md` (this file) — how work moves between specialists

---

## The Standard Handoff Packet

```
## Handoff Packet

- from:                    [Sending specialist, e.g. 01_lead_qualifier]
- to:                      [Receiving specialist, e.g. 03_client_communication]
- request_type:            [What kind of request is this?]
- client_name:             [Who is this for? "Unknown" is valid.]
- agent_name:              [Which team member owns this relationship? Always required.]
- current_stage:           [Where in the workflow does this sit?]
- known_facts:             [Confirmed information relevant to the receiving specialist's work]
- unknowns:                [Missing information the receiving specialist should be aware of]
- output_completed:        [What the sending specialist produced]
- output_needed_next:      [What the receiving specialist should produce]
- risk_flags:              [Anything needing attention before or during the work. "None" is valid.]
- diana_standard_notes:    [Quality expectations, relationship sensitivity, trust context. See DIANA_STANDARD.md.]
- voice_context_needed:    [Yes / No — does the receiving specialist need voice/<agent-name>.md?]
- quality_review_required: [Yes / No — does this output go to 05_quality_review before reaching the client?]
- escalation_needed:       [Yes / No — should Diana be looped in? If yes, note why.]
- recommended_next:        [Next destination after the receiving specialist completes their work]
```

---

## Field Reference

| Field | Required | Notes |
|---|---|---|
| `from` | Always | The sending specialist |
| `to` | Always | The receiving specialist |
| `request_type` | Always | Shapes how the receiving specialist approaches the work |
| `client_name` | Always | "Unknown" is a valid value — never omit the field |
| `agent_name` | Always | Blocks routing if missing. Voice and relationship context can't be reconstructed downstream. |
| `current_stage` | Always | Pre-qualification, active listing, under contract, etc. |
| `known_facts` | Always | Even a single fact is better than an empty field |
| `unknowns` | Always | "None" is valid. Missing context that isn't named is missing context that gets assumed. |
| `output_completed` | Always | What was actually produced by the sending specialist |
| `output_needed_next` | Always | What the receiving specialist should produce |
| `risk_flags` | Always | "None" is valid |
| `diana_standard_notes` | Always | "None" is valid — but think before writing "None" |
| `voice_context_needed` | Always | Must be Yes for any specialist that drafts client-facing communication |
| `quality_review_required` | Always | Must be Yes for any output that reaches a client |
| `escalation_needed` | Always | "No" is valid — but flag early rather than late |
| `recommended_next` | Always | Where the work goes after the receiving specialist is done |

---

## The Handoff Guarantee

When a specialist receives a packet, they should be able to start work immediately. If they have to ask what they're doing or why, the handoff failed.

When a specialist produces a packet, the receiving specialist should have everything they need — not everything that exists, but everything that matters for the next step.

---

## Loop-Back Handoffs

Not all work moves forward in a straight line. Three loop patterns are part of this system:

**Quality Review → Client Communication**
When `05_quality_review` returns a "Revise with notes" verdict, the packet goes back to `03_client_communication`. The revision notes travel with it. The loop closes when the draft is approved.

**Transaction Coordinator → Client Communication**
When `04_transaction_coordinator` identifies a client update that needs to go out — a deadline approaching, a milestone reached, a risk surfacing — it routes to `03_client_communication` to draft the message. That draft then goes to `05_quality_review` before reaching the agent.

**Any Specialist → Orchestrator**
If a specialist discovers mid-task that the request is different from what was routed — the scope changed, new information arrived, the situation escalated — it can return to `00_orchestrator` for re-routing. This is rare but should be used rather than improvising outside scope.

---

## Escalation

Escalation to Diana is not a failure state. It is a design feature.

Any specialist can escalate. The trigger is: *this situation requires judgment that isn't encoded in this system.* Common triggers are defined in each specialist's `rules.md`. The common thread: high stakes, outside standard experience, or a decision that Diana would want to have made herself.

When escalating, the Handoff Packet travels with the escalation. Diana should never receive an escalation without context.

---

## What the Packet Is Not

- It is not a summary of everything that happened. It carries what the next specialist needs, not a full case history.
- It is not a decision. The packet surfaces context and flags risk. Decisions belong to agents and Diana.
- It is not optional. A request that moves without a packet is a request that loses context.

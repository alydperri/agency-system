# Handoff: Quality Review

See `HANDOFF_PROTOCOL.md` for the standard packet shape and field definitions.

---

## How I Receive Work

I receive Draft Review Packets from `03_client_communication` — every client-facing draft, every time, before it returns to the agent.

I do not receive work from other specialists. My input is always a draft from Client Communication.

## Minimum Required Inputs

A complete Draft Review Packet containing:

```
- from:                    03_client_communication
- to:                      05_quality_review
- client_name:
- agent_name:              [Required — blocks review if missing]
- channel:
- situation_type:
- intended_outcome:
- relationship_context:
- voice_profile_used:      [Required — blocks review if missing]
- draft:
- agent_note:
- known_risks:
- quality_review_required: Yes
- escalation_needed:
```

If `agent_name` or `voice_profile_used` is missing, I ask before reviewing. Missing `intended_outcome`, `relationship_context`, or `agent_note` are noted in the review but do not block it.

## What I Produce

A **review verdict** in the standard format:

```
### Quality Review — [Draft Description]

**Verdict:** Approved / Approved — pending Diana review / Revise with notes
**Send status:** Ready to send / Hold for Diana review
(include Send status only when verdict is "Approved — pending Diana review")

**What's working:**
[Specific note on what the draft does well]

**Notes for revision:** (if applicable)
- [Specific, actionable note]
- [Specific, actionable note]

**Flag for Diana:** Yes / No
[If yes: brief explanation]
```

## Standard Outgoing Handoff Packet

```
## Handoff Packet

- from:                    05_quality_review
- to:                      [03_client_communication / agent via 03 / Diana]
- request_type:            Quality review verdict
- client_name:             [From incoming packet]
- agent_name:              [From incoming packet]
- current_stage:           [From incoming packet]
- known_facts:             [What worked in the draft]
- unknowns:                N/A
- output_completed:        Review verdict — [Approved / Approved pending Diana / Revise with notes]
- output_needed_next:      [Revision / Diana confirmation / Agent sends]
- risk_flags:              [Any risks identified in the review]
- diana_standard_notes:    [Criteria that failed or nearly failed, for Diana's awareness]
- voice_context_needed:    No
- quality_review_required: No — review is complete
- escalation_needed:       [Yes if flagged for Diana]
- recommended_next:        [03_client_communication for revision / Diana for confirmation / Agent to send]
```

## Where I Pass Work

| Destination | When |
|---|---|
| 03_client_communication | Verdict is "Revise with notes" — draft returns with specific revision notes |
| Agent (via 03_client_communication) | Verdict is "Approved" — draft returns to agent ready to send |
| Diana first, then agent | Verdict is "Approved — pending Diana review" — Diana confirms, then agent sends |

## When I Loop Backward

Quality review loops back to `03_client_communication` until the draft is approved. Each revision pass returns to me. I do not approve a draft that hasn't addressed the previous revision notes.

The loop closes when the draft is approved. The goal is not speed — it is a message that's right.

## When I Escalate to Diana

- The draft involves delivering news that could significantly affect the deal
- The situation is high-stakes and the draft is borderline — not clearly wrong, but Diana's judgment would add value
- The client relationship is particularly important (referral source, long-term client, high-value transaction)
- The draft required multiple revision rounds and still feels off

## What I Don't Pass Forward

- Rewritten drafts — notes only; the drafter revises
- Vague feedback — every note must be specific and actionable
- Approvals for drafts that fail any Diana Standard criteria

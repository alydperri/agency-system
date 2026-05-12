# Handoff: Property Research

See `HANDOFF_PROTOCOL.md` for the standard packet shape and field definitions.

---

## How I Receive Work

I receive Handoff Packets from:
- **00_orchestrator** — standalone research requests
- **01_lead_qualifier** — new lead mentions a specific property needing research

## Minimum Required Inputs

- Property address (required)
- Brief purpose: buyer brief, listing brief, or neighborhood brief (required — these are structured differently)
- Agent name (required — shapes how the brief is framed)
- Buyer priorities, if stated (schools, budget ceiling, specific concerns)
- Risk flags from the orchestrator (e.g. seller has price expectations)

If the brief purpose isn't specified, I ask before starting.

## What I Produce

A **Research Brief** in one of three formats:

| Brief Type | Used When |
|---|---|
| **Listing Brief** | Preparing for a seller listing consultation or pricing conversation |
| **Buyer Brief** | Buyer is evaluating a specific property for an offer |
| **Neighborhood Brief** | Buyer or seller needs context on an area, not a specific property |

Every brief includes:
- "What the agent should know before the meeting" — summary at the top
- Data with pull date and confidence level noted
- Property flags worth follow-up
- Recommended next step

## Standard Outgoing Handoff Packet

```
## Handoff Packet

- from:                    02_property_research
- to:                      03_client_communication
- request_type:            Research brief — [Listing / Buyer / Neighborhood]
- client_name:             [Client name]
- agent_name:              [Agent name]
- current_stage:           [Pre-listing / Pre-offer / Market exploration]
- known_facts:             [Key findings from the brief — comp range, flags, market context]
- unknowns:                [What the brief couldn't resolve — thin comps, unverified details]
- output_completed:        Research brief ([type]) for [property/area]
- output_needed_next:      Client-facing communication incorporating research findings
- risk_flags:              [Price expectation gap, property flags, thin data, etc.]
- diana_standard_notes:    [How the agent will use this in a client conversation]
- voice_context_needed:    Yes
- quality_review_required: Yes
- escalation_needed:       [Yes if comp data is too thin to support a defensible recommendation, or property has unusual history]
- recommended_next:        05_quality_review (via 03_client_communication)
```

## Where I Pass Work

| Destination | When |
|---|---|
| 03_client_communication | Research complete — agent needs to communicate findings to client |
| 00_orchestrator | Research reveals something that fundamentally changes the nature of the request |

## When I Loop Backward

- If research reveals the property or situation is materially different from what was described in the incoming packet, I return to `00_orchestrator` with a note explaining what changed before passing to `03_client_communication`.

## When I Escalate to Diana

- Comparable data is too thin to support a defensible pricing recommendation
- Something in the property record looks unusual enough to warrant legal or inspection attention
- The property is in a market segment outside the team's typical range

## What I Don't Pass Forward

- Research without a pull date
- Pricing recommendations stated as facts
- Briefs with ambiguous confidence levels — label uncertainty explicitly
- Any brief before noting property flags, even minor ones

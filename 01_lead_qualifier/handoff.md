# Handoff: Lead Qualifier

See `HANDOFF_PROTOCOL.md` for the standard packet shape and field definitions.

---

## How I Receive Work

I receive a Handoff Packet from `00_orchestrator`. I do not accept raw requests directly from team members.

## Minimum Required Inputs

- Agent name (required — shapes how I frame the profile)
- Whatever is known about the prospect (even very little is enough to start)
- Referral source, if applicable

I can work with incomplete information. My job is to identify what's missing and organize it.

## What I Produce

A **Lead Profile** for every routed prospect — including early, incomplete, or exploratory leads.

```
### Lead Profile — [Client Name or Description]

| Field | Status | Notes |
|---|---|---|
| Intent | [Buyer / Seller / Both / Unknown] | |
| Budget | [Range or "Unknown"] | |
| Timeline | [Hard / Soft / Unknown] + description | |
| Location | [Address or area / Unknown] | |
| Constraints | [List or "Unknown"] | |
| Source | [Referral from X / Website / Social / etc.] | |

**Readiness:** [Active / Near-term / Exploratory / Unknown]
[One sentence on what this readiness read is based on.]

**Agent note for first contact:**
[One to two sentences the agent should know before picking up the phone or sending a message.]

**Top unknown / next question:**
[The single most important missing piece, framed as the question that should surface it.]

**Diana Standard notes:**
[Relationship sensitivity, referral context, trust considerations, or "None"]

**Risk flags:**
[Anything worth flagging before the relationship develops further. "None" is valid.]

**Recommended next:**
[Which specialist should receive this, and why.]
```

## Standard Outgoing Handoff Packet

```
## Handoff Packet

- from:                    01_lead_qualifier
- to:                      [03_client_communication / 02_property_research / both]
- request_type:            Lead profile — [Buyer / Seller / Exploratory]
- client_name:             [Client name or description]
- agent_name:              [Agent name]
- current_stage:           Pre-qualification
- known_facts:             [Six-field profile summary]
- unknowns:                [Top unknown / next question]
- output_completed:        Lead profile with readiness read
- output_needed_next:      [First outreach draft / Research brief / both]
- risk_flags:              [From profile. "None" is valid.]
- diana_standard_notes:    [From profile.]
- voice_context_needed:    Yes — if routing to 03_client_communication
- quality_review_required: Yes — any output that reaches the client
- escalation_needed:       [Yes / No]
- recommended_next:        [After outreach or research, where does this go?]
```

## Where I Pass Work

| Destination | When |
|---|---|
| 03_client_communication | Agent needs a first outreach drafted |
| 02_property_research | Prospect mentioned a specific property or address |
| Both 02 and 03 | Seller lead with a known address — comp pull and outreach run in parallel |
| 00_orchestrator | Something in qualification reveals this request isn't what it appeared to be |

**When routing to both 02 and 03:** produce two short handoff notes — one research-oriented, one outreach-oriented. The research note leads with property and market details; the outreach note leads with relationship context and readiness read.

## When I Loop Backward

- If qualification reveals the request is something other than a lead (e.g. an existing client mid-transaction), I return to `00_orchestrator` for re-routing.

## When I Escalate to Diana

- Lead is a referral from a high-value past client or professional relationship
- Prospect has a complex situation that doesn't fit a standard buyer or seller profile
- Something in the conversation makes the team's fit for this client unclear

## What I Don't Pass Forward

- A profile with fewer than six fields addressed (even if some are "unknown")
- Interpretation disguised as fact — label observations clearly
- A lead disposition decision — I profile and flag. Diana or the agent decides.

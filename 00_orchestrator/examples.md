# Examples: Orchestrator

---

## Example 1: New Lead Comes In

**Team member input:**
> "Got a referral from the Hendersons. Couple looking to buy, said they're 'ready to move soon.' That's all I have."

**Orchestrator output:**

Two things before I route this: do you have a name or contact for this couple, or just the referral heads-up? And which agent owns this relationship?

*(Once confirmed: just a heads-up so far, and the message came from Marcus)*

Got it. Here's the handoff to Lead Qualifier.

---

**Handoff Packet → 01_lead_qualifier**

- **request_type:** New buyer lead
- **client_name:** Unknown — Henderson referral
- **agent_name:** Marcus
- **current_stage:** Pre-qualification
- **known_facts:** Couple, buyer, referred by Henderson clients, stated readiness "soon"
- **unknowns:** Names, contact info, budget, location preference, timeline specifics, pre-approval status
- **risk_flags:** None yet — very early stage
- **diana_standard_notes:** Referral from existing clients. Handle with care — experience reflects on the Hendersons' trust in us.
- **recommended_next:** 01_lead_qualifier
- **output_needed:** Qualified lead profile

---

## Example 2: Mid-Deal Research Request

**Team member input:**
> "Can you pull comps for 4712 Brentwood Ave? We're listing it next week and the sellers want to know what's realistic."

**Orchestrator output:**

One thing before I route: which agent is on this listing?

*(Once confirmed: Diana)*

Routing to Property Research. Since this is a listing conversation with a hard timeline, I'm flagging it as time-sensitive.

---

**Handoff Packet → 02_property_research**

- **request_type:** Comp pull for listing
- **client_name:** [sellers at 4712 Brentwood Ave]
- **agent_name:** Diana
- **current_stage:** Pre-listing
- **known_facts:** Property address is 4712 Brentwood Ave; listing target is next week; sellers have pricing expectations
- **unknowns:** Seller's current price expectation, property condition, any improvements made
- **risk_flags:** Sellers have a stated price expectation — research output may need to manage that conversation. Flag if comps come in significantly under expectations.
- **diana_standard_notes:** Agent will take this into a client conversation. Output should be usable in a real meeting, not just internally.
- **recommended_next:** 02_property_research
- **output_needed:** Comp analysis and pricing context brief

---

## Example 3: The 11pm Slack

**Team member input:**
> "Hey sorry it's late — we just got an executed contract on the Morrison deal and I don't know what documents need to go where or by when. Help?"

**Orchestrator output:**

No worries — let's get you sorted. I need two things to route this correctly:

1. What's the contract date on the Morrison deal?
2. Are you the buyer's agent or listing agent on this one?

*(Once answered)*

Routing to Transaction Coordinator now with everything I have.

---

**Handoff Packet → 04_transaction_coordinator**

- **request_type:** New contract — onboarding to transaction tracking
- **client_name:** Morrison
- **agent_name:** [team member name]
- **current_stage:** Contract executed
- **known_facts:** Contract just executed; agent is [buyer's/listing] agent
- **unknowns:** Contract date, option period length, closing date, lender contact, title company
- **risk_flags:** Agent is newer — provide full checklist with explanations, not just task list. Time is already running.
- **diana_standard_notes:** Don't assume familiarity with the process. Give the agent what they need to feel confident at 11pm, not just technically covered.
- **recommended_next:** 04_transaction_coordinator
- **output_needed:** Transaction checklist with deadlines and document owners

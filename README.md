# The Agency System
### An AI Operating System for Diana's Team

---

Diana, this was built for you.

Not for a generic real estate team. For a four-person boutique operation that turns down volume to do better work, runs on referrals and reputation, and has too much institutional knowledge living in one person's head.

The system has one job: make your standards portable. When Marcus handles a lead, he should handle it the way you would. When Carmen is staring at a new contract at 11pm, she should know exactly what to do without texting you. When a client-facing email goes out under Priya's name, it should sound like Priya — and it should be good.

That's what this is. Two root contracts hold it together:

- **`DIANA_STANDARD.md`** — the quality bar every output is held to
- **`HANDOFF_PROTOCOL.md`** — how work moves between specialists

Everything else inherits from those two files.

---

## What You're Working With

Six specialists, each owning one part of your workflow. Every request starts at the Orchestrator and moves through the system with an explicit handoff at each stage — so context doesn't disappear between steps and nobody has to rebuild it from scratch.

```
agency-system/
├── README.md
├── DIANA_STANDARD.md           ← Quality bar every specialist applies
├── HANDOFF_PROTOCOL.md         ← Standard packet for moving work between specialists
├── voice/                      ← Agent voice profiles (one file per team member)
├── 00_orchestrator/            ← Every request starts here
├── 01_lead_qualifier/          ← Turns inquiries into actionable lead profiles
├── 02_property_research/       ← Research briefs for client conversations
├── 03_client_communication/    ← Drafts all client-facing messages in the agent's voice
├── 04_transaction_coordinator/ ← Tracks deals from contract to close
└── 05_quality_review/          ← Reviews drafts before anything reaches a client
```

Each folder contains four files:
- `identity.md` — who this specialist is, what they own, what they don't
- `rules.md` — how they operate, always and never
- `examples.md` — two to three examples showing the specialist in action
- `handoff.md` — what they receive, what they produce, and where work goes next. Each `handoff.md` uses the root `HANDOFF_PROTOCOL.md` packet shape, then defines that specialist's specific inputs, outputs, and routing logic.

---

## How a Request Moves Through the System

**Every request starts at the Orchestrator.** No exceptions.

The Orchestrator reads the incoming request, assesses what's known and what's missing, surfaces any risk flags, and produces a Handoff Packet for the right specialist. If a request is ambiguous, it asks one clarifying question before routing.

**A new lead looks like this:**

```
Team member → 00_orchestrator
  → Handoff Packet → 01_lead_qualifier
    → Lead Profile → 03_client_communication
      → Draft → 05_quality_review
        → Approved → agent sends
```

**A deal going under contract looks like this:**

```
Team member → 00_orchestrator
  → 04_transaction_coordinator
    → Transaction checklist with deadlines and owners
    → On status check: surfaces upcoming deadlines and flags risks before they become problems
    → When client update needed → 03_client_communication
      → Draft → 05_quality_review → agent sends
```

**The Handoff Packet is what keeps this system coherent.** Every specialist receives one and produces one. Context travels forward explicitly at every step — nobody has to ask "wait, what am I doing and why?"

---

## The Two Root Contracts

**`DIANA_STANDARD.md`** defines the quality bar: four criteria — specificity, clarity, brevity, and voice — that every output is held to. Each specialist folder applies those criteria to its own domain. The quality review specialist (05) exists to enforce this before anything reaches a client. If Diana's standards evolve, update `DIANA_STANDARD.md` and it propagates through the whole system.

**`HANDOFF_PROTOCOL.md`** defines how work moves. Every specialist receives and produces a standard Handoff Packet — a structured context carrier with named fields for known facts, unknowns, risk flags, Diana Standard notes, voice context, escalation status, and next output needed. Work doesn't move between specialists without one.

The two contracts are designed to work together: the handoff packet carries the Diana Standard forward at every stage, so quality expectations travel with the work rather than getting re-stated at each step.

---

## How to Use This System

The folders are the system. You load a specialist's context when you need that specialist.

**Working in Claude Code (VS Code):**

When you start a task, load the two root contracts plus the relevant specialist's files:

```
@DIANA_STANDARD.md
@HANDOFF_PROTOCOL.md
@00_orchestrator/identity.md
@00_orchestrator/rules.md
@00_orchestrator/handoff.md
```

Load both root contracts every time — it's simpler than deciding when they're relevant, and they're small enough that the overhead is negligible. When the specialist produces a Handoff Packet, open a new session, load the root contracts again plus the destination specialist's files, and continue. Use `examples.md` when a task is unusual or you want to show Claude what good output looks like.

**Working in claude.ai (browser):**

Same approach without the `@` syntax. Copy the contents of `DIANA_STANDARD.md`, `HANDOFF_PROTOCOL.md`, `identity.md`, `rules.md`, and `handoff.md` into the conversation before your request. For frequent use, create a saved Project per specialist and paste all five files into the project instructions.

**The flow in either setup:**
1. Start with `00_orchestrator` — load its three core files, drop your request
2. Take the Handoff Packet to the destination specialist
3. Follow the chain until the work is done

**Before your first session, do two things:**

1. **Create voice profiles for each agent.** Copy `voice/TEMPLATE_voice.md`, rename it to the agent's first name (e.g. `voice/marcus.md`), and fill it out. It takes about 15 minutes per person. The `voice/diana.md` file ships as a completed example — read it first to understand what a good profile looks like. The `03_client_communication` specialist will not draft without a profile for the named agent.
2. **Replace the placeholder agent names** throughout the examples: the system uses Diana, Marcus, Priya, and Carmen — find and replace those with your real team names, and rename the voice profile files to match.

---

## Onboarding a New Team Member

Hand them this README. Then have them do one thing: run a practice request through the Orchestrator.

Pick a scenario they'll actually face in the first week — a new lead, a research request, a contract just executed. Walk through the Handoff Packet that comes out, open the destination folder, and read the examples.

The system doesn't require training on real estate. It requires understanding the flow. The flow is in this README. The depth is in the folders. A new agent should be functional within a day.

---

## What This System Doesn't Do

- It doesn't make decisions. It surfaces context, flags risk, and produces drafts. You and your agents decide.
- It doesn't send anything. Every client-facing output is a draft for agent review.
- It doesn't replace your judgment. It makes your judgment portable across the team.
- It doesn't manage multiple transactions in a single session. One request, one client, one thread.

---

## Adapting This System for a Different Team

This system was built for Diana's team, but the underlying architecture is not Diana-specific. The folder structure, handoff protocol, and specialist logic apply to any small, high-trust service team with consistent quality standards and clear workflow stages.

To stand it up for a different team, change four things:

1. **The two root contracts** — update `DIANA_STANDARD.md` with the new team lead's quality bar. `HANDOFF_PROTOCOL.md` carries over unchanged; the packet shape is domain-agnostic. The specialist folders each have a short domain-specific application of the Diana Standard — review those too, but the root file is the only place the full definition lives.

2. **Agent names and voice profiles** — find and replace agent names throughout `03_client_communication` and any examples. Replace the voice profile files in `voice/` with profiles for the new team's agents using `TEMPLATE_voice.md`.

3. **The transaction checklist** — `04_transaction_coordinator/rules.md` contains a checklist built for Texas residential real estate. A different jurisdiction, deal type, or industry will have different milestones and documents. Rewrite the checklist; the tracking and flagging logic carries over.

4. **The examples** — scenarios in each `examples.md` are drawn from real estate situations. Replace them with two to three representative scenarios from the new domain.

The Orchestrator logic, Handoff Packet structure, and Quality Review criteria transfer without changes. Those are the architecture. Everything else is content.

---

## Folder Reference

**Specialist folders** — each owns a stage in the workflow and participates in the handoff chain:

| Folder | One-line description |
|---|---|
| `00_orchestrator` | Receives all requests; routes with context and risk assessment |
| `01_lead_qualifier` | Builds a six-field lead profile from any prospect inquiry |
| `02_property_research` | Produces buyer briefs, listing briefs, and neighborhood profiles |
| `03_client_communication` | Drafts all client-facing messages in the agent's voice |
| `04_transaction_coordinator` | Tracks deadlines and documents from contract to close |
| `05_quality_review` | Reviews drafts against the Diana Standard before anything goes out |

**Reference folder** — not a specialist; loaded as context by the specialist that needs it:

| Folder | One-line description |
|---|---|
| `voice/` | Agent voice profiles used by `03_client_communication` to match tone and style. Contains `TEMPLATE_voice.md` to create new profiles and `diana.md` as a completed example. Create one file per agent before using the communication specialist. |

**Root reference files** — single source of truth for system-wide definitions:

| File | One-line description |
|---|---|
| `DIANA_STANDARD.md` | The canonical definition of Diana's quality bar. Every specialist references it. Update here only — not in individual folders. |
| `HANDOFF_PROTOCOL.md` | The standard Handoff Packet shape every specialist uses. Defines all fields, loop patterns, and escalation logic. Update here if the packet shape changes. |

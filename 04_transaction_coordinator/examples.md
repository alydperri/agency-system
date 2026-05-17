# Examples: Transaction Coordinator

*Packets in these examples are condensed for readability. Full field definitions are in `HANDOFF_PROTOCOL.md` and this specialist's `handoff.md`.*

---

## Example 1: New Contract — Building the Checklist

**Incoming handoff from Orchestrator:**
- client_name: Morrison (buyers)
- agent_name: Priya
- situation: Contract just executed on 2841 Kerbey Lane. Priya is the buyer's agent. Contract date: May 10. Option period: 10 days. Closing date: June 14.
- risk_flags: Priya is newer — provide full checklist with context, not just tasks.

---

**Transaction Coordinator Output:**

### Transaction Checklist — Morrison / 2841 Kerbey Lane
*Buyer-side | Agent: Priya | Contract executed: May 10*

---

**⚠️ Immediate actions (first 3 business days):**
- [ ] **Option fee** — must be delivered to seller by May 13. Confirm delivery method with title company today.
- [ ] **Schedule inspection** — option period runs through May 20. Inspection should be scheduled for May 15–17 at the latest to leave response time.

---

**Option Period** *(expires May 20)*

| Item | Status | Owner | Notes |
|---|---|---|---|
| Option fee delivered | ⬜ Unconfirmed | Priya | Due May 13 — urgent |
| Inspection scheduled | ⬜ Pending | Priya | Target May 15–17 |
| Inspection report received | ⬜ Pending | Inspector | |
| Inspection response sent | ⬜ Pending | Priya + Diana | If needed — discuss findings first |
| Option exercised/released | ⬜ Pending | Priya | Due by May 20 EOD |

---

**Financing** *(contingency deadline: TBD — confirm with lender)*

| Item | Status | Owner | Notes |
|---|---|---|---|
| Lender contact | ⬜ Confirm | Priya | Who is the Morrisons' lender? |
| Loan application submitted | ⬜ Unconfirmed | Buyers | Priya to confirm |
| Appraisal ordered | ⬜ Pending | Lender | |
| Appraisal received | ⬜ Pending | Lender | |
| Financing approval | ⬜ Pending | Lender | |

---

**Title & Closing** *(closing date: June 14)*

| Item | Status | Owner | Notes |
|---|---|---|---|
| Title company confirmed | ⬜ Confirm | Priya | Who is handling title? |
| Title commitment received | ⬜ Pending | Title company | |
| Homeowner's insurance | ⬜ Pending | Buyers | Must be bound before closing |
| Final walkthrough | ⬜ Schedule | Priya | Target June 12–13 |
| Closing disclosure | ⬜ Pending | Lender | Due June 11 (3 days before closing) |
| Closing | ⬜ Pending | All parties | June 14 |

---

**Note for Priya:** The most urgent item is the option fee — that has a hard 3-day deadline. Everything else has some runway. If you're not sure who to deliver the option fee to or how, call the title company first thing tomorrow.

**Risk flags:** None currently. Flag will trigger if inspection response isn't resolved by May 18.

---

## Example 2: Mid-Transaction Status Check

**Incoming from agent:**
> "Can you give me a status update on the Morrison deal? We're about two weeks in."

---

**Transaction Coordinator Output:**

### Status Update — Morrison / 2841 Kerbey Lane
*As of May 24 | Buyer-side | Agent: Priya*

---

**Option Period:** ✅ Closed. Option exercised May 20. Inspection credit of $1,800 agreed.

**Financing:**

| Item | Status | Notes |
|---|---|---|
| Lender | ✅ Confirmed | First National, contact: [lender name] |
| Appraisal | ⬜ In progress | Ordered May 19; expected back by May 30 |
| Financing contingency deadline | ⚠️ June 2 | 9 days out — follow up with lender by May 29 |

**⚠️ Action needed:** No update from lender since May 19. Priya should check in with [lender] by May 29 to confirm appraisal is on track. If appraisal isn't back by May 31, escalate to Diana.

**Title & Closing:**

| Item | Status | Notes |
|---|---|---|
| Title commitment | ✅ Received | No issues flagged |
| Insurance | ⬜ Pending | Morrison to confirm by June 7 |
| Final walkthrough | ⬜ Not scheduled | Schedule for June 12–13 |
| Closing | ⬜ On track | June 14 |

**Overall:** Deal is on track. One flag: lender check-in is overdue. Everything else is running to schedule.

---

## Example 3: Risk Flag — Deadline at Risk

**Generated on status check — May 30:**

---

**⚠️ Risk Flag — Morrison / 2841 Kerbey Lane**
*May 30 — Flagged for Priya and Diana*

The financing contingency deadline is June 2 — **3 days from now.**

Appraisal was expected back by May 30. As of today, no update has been logged.

**Status:** Unresolved
**Owner:** Priya (to follow up with lender immediately)
**Escalation threshold:** If no lender update by June 1 EOD, escalate to Diana.

Recommended action: Priya calls lender today. If appraisal is delayed, Diana needs to know before the deadline to assess options.

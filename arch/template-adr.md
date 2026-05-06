# Architecture Decision Record
## ADR-[NUMBER]: [Short Title]

**Status:** `Draft` | `Proposed` | `Accepted` | `Deprecated` | `Superseded by ADR-[NUMBER]`
**Date:** YYYY-MM-DD
**Author(s):** [Name(s)]
**Stakeholders:** [Names and roles of people who reviewed or approved]
**Related ADRs:** [Links to related or superseded records]
**Related Principles:** [e.g., AD-2 Preserve Optionality, RS-2 Document Known Risks]

---

## Context

*Describe the situation that requires a decision. Include the business or technical forces at play — what problem are we solving, what constraints exist, and why does a decision need to be made now. Be specific about what is known and what is uncertain.*

---

## Decision Drivers

*List the specific factors that most influence this decision. These may include:*

- *Workload requirements (performance, scale, availability)*
- *Organizational constraints (budget, timeline, team expertise)*
- *Risk posture (regulatory, security, operational)*
- *Strategic direction (platform alignment, vendor relationships, exit optionality)*
- *Existing dependencies and integration requirements*

---

## Options Considered

*Document each option that was seriously evaluated. Use a consistent structure for each.*

### Option 1: [Name]

**Description:** [What this option is and how it works]

**Pros:**
- 

**Cons:**
- 

**Cost/Complexity estimate:** [High / Medium / Low or specific figures if known]

**Exit optionality:** [How easily can this decision be reversed or changed?]

---

### Option 2: [Name]

**Description:**

**Pros:**
-

**Cons:**
-

**Cost/Complexity estimate:**

**Exit optionality:**

---

### Option 3: [Name] *(if applicable)*

**Description:**

**Pros:**
-

**Cons:**
-

**Cost/Complexity estimate:**

**Exit optionality:**

---

## Decision

*State the decision clearly and unambiguously. One option, chosen.*

**We will:** [Chosen option and brief restatement of what will be done]

**Because:** [The primary reasons this option was selected over the alternatives — reference the decision drivers above]

---

## Validation Approach

*Describe how this decision will be validated before full commitment, scaled to the risk of being wrong. (Principle DD-2)*

- [ ] Proof of concept required? **Yes / No**
- [ ] If yes: scope of PoC, success criteria, and timeline
- [ ] If no: rationale for proceeding without PoC

---

## Known Risks and Mitigations

*Document every known risk associated with this decision. Each risk must have a status. (Principle RS-2)*

| Risk | Likelihood | Impact | Mitigation | Status |
|---|---|---|---|---|
| [Risk description] | High/Med/Low | High/Med/Low | [Mitigation approach] | Open / Mitigated / Accepted |

**Accepted risks** (risks with no mitigation, accepted by the organization):

| Risk | Rationale for Acceptance | Accepted By | Date |
|---|---|---|---|
| | | | |

---

## Consequences

*What becomes easier or harder as a result of this decision? What does it constrain or enable? What follow-on decisions will be required?*

**Enables:**
-

**Constrains:**
-

**Follow-on decisions required:**
-

---

## Review and Supersession

*Describe the conditions under which this decision should be revisited.*

- This ADR should be reviewed if: [e.g., vendor pricing changes materially, workload scale exceeds X, regulatory requirements change]
- Supersession requires: a new ADR with status "Superseded by ADR-[NUMBER]" and a link back to this record

---

## Approval

| Role | Name | Decision | Date |
|---|---|---|---|
| Architecture | | Approved / Rejected / Abstained | |
| Engineering Lead | | Approved / Rejected / Abstained | |
| Operations | | Approved / Rejected / Abstained | |
| Business Owner | | Approved / Rejected / Abstained | |

---

*Template version: 1.0*
*Governed by: [Architecture Principles](architecture-principles.md)*

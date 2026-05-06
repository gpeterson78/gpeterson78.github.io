# Project Intake Document
*Complete this document at project initiation. Update it at each major milestone.*
*This is the authoritative record of requirements, decisions, risks, and acceptance criteria for the project.*

---

## Project Identity

**Project name:**
**Project ID:** [If applicable]
**Date initiated:** YYYY-MM-DD
**Target delivery date:** YYYY-MM-DD
**Project owner (business):**
**Technical lead:**
**Status:** `Intake` | `Discovery` | `Design` | `Validation` | `Delivery` | `Closed`

---

## 1. Executive Summary

*Two to four sentences. What is being built, why, and what the expected outcome is. Written for a non-technical audience.*

---

## 2. Business Context

**Problem or opportunity being addressed:**

**Business driver:** `Risk mitigation` | `Capacity` | `Compliance` | `Cost reduction` | `New capability` | `Other`

**Urgency and deadline:** [Is there a hard deadline? What drives it?]

**Organizational stakeholders:**

| Name | Role | Interest in this project |
|---|---|---|
| | | |

---

## 3. Discovery Findings

*Document what was found during the initial investigation. This section is completed during discovery, before design begins. (Principle DD-4)*

**Current state summary:**

**Key findings:**

| Finding | Severity | Impact on scope | Notes |
|---|---|---|---|
| | High/Med/Low | Expands / Constrains / Neutral | |

**Scope confirmed:** `Yes` | `No — pending: [what is outstanding]`

**Chesterton's Fence check:** *(For projects modifying or replacing existing systems)*
- What does the existing system do?
- Why was it built the way it was?
- What depends on it?
- Is there a reason to preserve any part of it?

---

## 4. Requirements

### Functional Requirements

| ID | Requirement | Priority | Source | Acceptance Criteria |
|---|---|---|---|---|
| F1 | | Must/Should/Nice | | |

### Non-Functional Requirements

| ID | Requirement | Target | Priority | Acceptance Criteria |
|---|---|---|---|---|
| NF1 | Availability | | Must/Should | |
| NF2 | RTO | | Must/Should | |
| NF3 | RPO | | Must/Should | |
| NF4 | Performance | | Must/Should | |
| NF5 | Security / Compliance | | Must | |
| NF6 | Scalability | | Must/Should | |

### Constraints

| Type | Constraint | Flexibility | Source |
|---|---|---|---|
| Budget | | Hard/Soft | |
| Timeline | | Hard/Soft | |
| Team expertise | | Hard/Soft | |
| Regulatory | | Hard | |
| Platform/vendor | | Hard/Soft | |

---

## 5. Architecture Decisions

*Link to or summarize each significant architectural decision made for this project. Each significant decision should have a corresponding ADR.*

| Decision | ADR | Status | Date |
|---|---|---|---|
| [e.g., Platform selection] | [ADR-001](./adr-001.md) | Accepted | |
| [e.g., Deployment model] | [ADR-002](./adr-002.md) | Proposed | |

---

## 6. Risk Register

*Every known risk must be documented with a status. (Principle RS-2)*
*Risks that are deferred or accepted must be recorded with the approver and date.*

| ID | Risk Description | Likelihood | Impact | Mitigation | Owner | Status | Date |
|---|---|---|---|---|---|---|---|
| R1 | | H/M/L | H/M/L | | | Open/Mitigated/Accepted | |

**Formally accepted risks** *(risks with no available mitigation, accepted by the organization):*

| Risk ID | Rationale | Accepted By | Date |
|---|---|---|---|
| | | | |

---

## 7. Dependencies

| Dependency | Type | Owner | Status | Risk if unavailable |
|---|---|---|---|---|
| | Platform/Team/Vendor/Data | | Confirmed/Pending | |

---

## 8. Delivery Plan

**Migration approach:** `Big bang` | `Strangler fig / incremental` | `Parallel run` | `N/A`

**Rationale for approach:**

### Milestones

| Milestone | Description | Target Date | Owner | Status |
|---|---|---|---|---|
| Discovery complete | | | | |
| Design approved | | | | |
| Validation complete | | | | |
| Stakeholder alignment | | | | |
| Production ready | | | | |
| Post-implementation review | | | | |

### Rollback Plan

*How will the change be reversed if delivery fails? (Principle RS-1)*

---

## 9. Stakeholder Alignment Log

*Record alignment checkpoints throughout the project. (Principle DD-3)*

| Date | Milestone | Stakeholders Present | Outcome | Outstanding Items |
|---|---|---|---|---|
| | Intake review | | Aligned / Gaps noted | |
| | Design review | | Aligned / Gaps noted | |
| | Pre-production review | | Aligned / Gaps noted | |

---

## 10. Acceptance Criteria and Sign-Off

*A solution is not production until requirements have been met, mitigated, or explicitly accepted as missed — and all parties have confirmed. (Principle DD-3)*

### Requirements Sign-Off

| Requirement ID | Status | Notes |
|---|---|---|
| F1 | Met / Mitigated / Accepted as missed | |
| NF1 | Met / Mitigated / Accepted as missed | |

### Production Sign-Off

| Role | Name | Signature | Date |
|---|---|---|---|
| Technical Lead | | | |
| Operations | | | |
| Business Owner | | | |
| Security (if applicable) | | | |
| Architecture (if applicable) | | | |

**Production approved:** `Yes` | `No — pending: [items]`

---

## 11. Post-Implementation Notes

*Complete after delivery. What was learned? What would be done differently?*

**What worked:**

**What didn't:**

**Follow-on work identified:**

| Item | Priority | Owner | ADR or ticket |
|---|---|---|---|
| | | | |

---

*Template version: 1.0*
*Governed by: [Architecture Principles](architecture-principles.md)*
*Significant decisions should be recorded in: [ADR Template](./template-adr.md)*
*Pre-decision analysis should use: [Decision Template](./template-decision.md)*

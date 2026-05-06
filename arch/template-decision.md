# Architecture Decision Template
*Use this template before committing to a design on any significant technical decision.*
*When a decision is finalized, promote it to a formal ADR.*

---

## Decision Summary

**Decision title:** [One line description]
**Date initiated:** YYYY-MM-DD
**Decision owner:** [Name and role]
**Target decision date:** YYYY-MM-DD
**Urgency:** `Routine` | `Elevated` | `Crisis-driven`

---

## 1. Problem Statement

*What problem are we solving? State it in one or two sentences. If you cannot state it simply, requirements gathering is not complete.*

---

## 2. Scope Check

*Before designing, confirm the full scope has been investigated. (Principle DD-4)*

- [ ] Have I talked to the people who will **build** this?
- [ ] Have I talked to the people who will **operate** this?
- [ ] Have I talked to the people who **requested** this?
- [ ] Have I reviewed existing systems this will depend on or affect?
- [ ] Have I identified what I don't yet know?

**Scope gaps identified:**

---

## 3. Requirements

*Document requirements across all relevant dimensions. Separate hard requirements (must-have) from preferences (nice-to-have).*

### Functional Requirements
| # | Requirement | Must / Should / Nice-to-have | Source |
|---|---|---|---|
| F1 | | | |

### Non-Functional Requirements
| # | Requirement | Must / Should / Nice-to-have | Source |
|---|---|---|---|
| NF1 | Availability target | | |
| NF2 | Recovery time objective (RTO) | | |
| NF3 | Recovery point objective (RPO) | | |
| NF4 | Performance requirements | | |
| NF5 | Security / compliance requirements | | |

### Constraints
| Type | Constraint | Source |
|---|---|---|
| Budget | | |
| Timeline | | |
| Team expertise | | |
| Regulatory | | |
| Existing platform dependencies | | |

---

## 4. Workload Profile

*Characterize the workload to inform platform selection. (Principle AD-1)*

| Dimension | Assessment |
|---|---|
| Scale (current) | |
| Scale (projected 3yr) | |
| Traffic pattern | Steady / Bursty / Seasonal / Unknown |
| Data gravity / residency requirements | |
| Maturity | Greenfield / Existing / Legacy migration |
| Team operational expertise | |

**Deployment default:** `On-premises` | `Cloud` | `Hybrid` | `SaaS`
**Rationale for default:** [Why this deployment model fits this workload]

---

## 5. Options

*Document at least two options. A single option is not a decision — it is an assumption. (Principle DD-1)*

| | Option A | Option B | Option C |
|---|---|---|---|
| **Description** | | | |
| **Deployment model** | | | |
| **Cost estimate** | | | |
| **Complexity** | Low/Med/High | Low/Med/High | Low/Med/High |
| **Team expertise fit** | | | |
| **Exit optionality** | | | |
| **Vendor dependencies** | | | |
| **Time to deliver** | | | |

---

## 6. Recommendation

**Recommended option:** [Option A / B / C]

**Primary rationale:** [The one or two reasons this option is correct for this workload and organization]

**Tradeoffs accepted:** [What you're giving up by choosing this option]

**Principles applied:**
- [ ] AD-1: Deployment location matches workload requirements
- [ ] AD-2: Exit optionality preserved or explicitly waived
- [ ] AD-3: Simplest solution that meets requirements
- [ ] AD-4: Strangler fig / incremental migration planned (if applicable)
- [ ] AD-5: Existing systems understood before modification (if applicable)
- [ ] RS-1: Recovery requirements defined
- [ ] RS-2: Known risks documented
- [ ] RS-3: Attack surface and access controls considered
- [ ] DD-1: Requirements gathered from all parties
- [ ] DD-2: Validation approach scaled to risk

---

## 7. Validation Plan

*How will this recommendation be validated before full commitment? (Principle DD-2)*

**Validation required:** `PoC` | `Pilot` | `Spike` | `None — low risk, proceed`

If validation required:
- **Scope:** [What will be tested]
- **Success criteria:** [What must be true for this to proceed]
- **Timeline:** [Duration and target date]
- **Owner:** [Who is responsible]

---

## 8. Known Risks

*Every known risk must be documented. (Principle RS-2)*

| Risk | Likelihood | Impact | Mitigation | Status |
|---|---|---|---|---|
| | High/Med/Low | High/Med/Low | | Open / Mitigated / Accepted |

---

## 9. Stakeholder Alignment

*Record who has been consulted and where alignment stands. (Principle DD-3)*

| Stakeholder | Role | Consulted | Aligned | Notes |
|---|---|---|---|---|
| | | Yes/No | Yes/Partial/No | |

**Outstanding alignment gaps:**

---

## 10. Next Step

- [ ] Escalate for budget approval
- [ ] Proceed to proof of concept
- [ ] Proceed directly to ADR
- [ ] Return to requirements — scope incomplete
- [ ] Defer — awaiting: [reason]

---

*Template version: 1.0*
*Governed by: [Architecture Principles](architecture-principles.md)*
*When finalized, promote to: [ADR Template](./template-adr.md)*

# Architecture Principles
*Grady Peterson — Infrastructure Engineering Leadership*
*Version 1.0 — May 2026*

---

## Purpose

This document defines the architecture principles that guide my approach to infrastructure design, technology decision-making, risk management, and team leadership. These principles are derived from practice across twenty years of infrastructure engineering in healthcare, education, media, and enterprise environments.

Each principle follows a standard structure: a name, a statement, the rationale behind it, and the practical implications for design and delivery.

This is a living document. Principles are updated as practice evolves.

---

## Categories

1. [Architecture & Design](#architecture--design)
2. [Risk & Security](#risk--security)
3. [Decision Making & Delivery](#decision-making--delivery)
4. [People & Teams](#people--teams)

---

## Architecture & Design

---

### AD-1 — Infrastructure Is the Foundation; Deployment Location Is an Architectural Decision

**Statement:** Infrastructure encompasses all platforms upon which IT solutions are built — on-premises, cloud, and SaaS — and where a workload is deployed is as much an architectural decision as how it is designed.

**Rationale:** Deployment location is not a default or a convention — it is a decision with real consequences for cost, complexity, operational burden, and velocity. The most sophisticated platform is not always the right one. Cloud-native reference architectures and well-architected frameworks are valuable guidance, not universal prescriptions. A workload deployed onto a platform it doesn't need pays a complexity tax and an operational cost with no return. The correct deployment decision follows from honest workload analysis: what does this workload actually require, and what platform serves those requirements most efficiently?

A small set of lightweight Python integration services has different requirements than a high-traffic, globally distributed application. Deploying the former into a full Kubernetes orchestration platform because "containers are containers" is not modernization — it is re-platforming, with all the rebuild cost and operational overhead that entails, for capabilities the workload does not need. The velocity and simplicity gains of the cloud can be captured without adopting its most complex patterns by default.

**Implications:**
- Workload requirements must drive platform selection. The analysis starts with the workload, not the platform.
- Cloud, on-premises, and SaaS are all valid deployment targets; the selection criterion is fit, not fashion.
- Reference architectures and vendor frameworks describe what is possible, not what is required. Deviation from a reference architecture that is justified by workload requirements is correct engineering.
- Complexity introduced by platform choice has a real cost: rebuild effort, operational expertise, and ongoing overhead. That cost must be justified by capability the workload actually needs.
- My default posture is hybrid: on-premises as the anchor for mature, stable workloads with predictable resource profiles; cloud where elasticity, developer velocity, or capability fit warrants it. Neither is the answer in the abstract.

---

### AD-2 — Preserve Optionality

**Statement:** Architecture decisions should preserve the freedom to change course; lock-in to any platform, vendor, or pattern is a liability that must be justified.

**Rationale:** Platforms change. Vendors are acquired, pricing models shift, support quality degrades, and technologies are superseded. An architecture that can only be operated by a single vendor or can only evolve in one direction is a risk, not a foundation. Optionality — the ability to replace, remove, or redirect any component — has real value even when it is never exercised.

**Implications:**
- Every significant platform dependency should have a documented exit path.
- Components should be designed for independent replaceability: interfaces minimized, dependencies explicit, state externalized where possible.
- Vendor selection processes should include at least one genuine alternative; competition is a lever, not a formality.
- Proprietary integrations that eliminate exit options require explicit justification and documented acceptance.

*Demonstrated in practice: During a multi-year HCI platform replacement, a hypervisor exit path was modeled and validated before a major vendor acquisition closed — optionality that proved immediately relevant. In personal infrastructure, each layer of a self-hosted stack is independently removable without disrupting the security model below it.*

---

### AD-3 — Simplicity Is Discipline

**Statement:** The simplest architecture that honestly meets the requirements is the correct architecture; complexity must be justified, not assumed.

**Rationale:** Complexity is easy to add and nearly impossible to remove. Every layer of unnecessary complexity becomes operational debt — more failure modes, more expertise required, more surface area for errors. Simplicity is not a lack of sophistication; it is the result of rigorous requirements analysis and the discipline to resist over-engineering.

**Implications:**
- Requirements must be understood before design begins. A solution cannot be evaluated for simplicity until the actual problem is defined.
- Complexity added for future flexibility that has not been requested is speculation, not engineering.
- When evaluating options, the simpler solution carries the burden of proof in reverse: it should be adopted unless there is a specific, documented reason it cannot meet requirements.

---

### AD-4 — Apply the Strangler Fig Pattern for Migration

**Statement:** Replace existing systems incrementally alongside the old, migrating workloads progressively until the legacy system can be decommissioned cleanly.

**Rationale:** Big-bang migrations concentrate all risk into a single event. Incremental replacement through the strangler fig pattern distributes risk across time, allows course correction, keeps the business operational throughout, and produces a validated replacement before the legacy system is removed.

**Implications:**
- New platforms should be stood up alongside existing ones, not as replacements that require immediate cutover.
- Workloads should migrate through natural refresh cycles, redeployment events, or deliberate sequencing — not forced cutovers driven by arbitrary deadlines.
- Decommission the legacy system in stages as dependencies are resolved, not all at once.
- A strangler fig migration has a defined target state and a clear path to it. Incremental pace is not the same as indefinite deferral.

*Demonstrated in practice: During a full datacenter platform replacement across four sites, the legacy hypervisor was decommissioned progressively by site and workload while the replacement platform ran in parallel — no forced cutover, no single point of failure during transition.*

---

### AD-5 — Understand the Fence Before You Remove It

**Statement:** Do not remove, replace, or significantly alter any system, process, or configuration until its purpose is understood.

**Rationale:** Systems exist for reasons that are not always documented, obvious, or still valid. Removing something without understanding what it does — or what depends on it — is how migrations create new failures. Chesterton's Fence is a discipline against careless change, not a prohibition on change.

**Implications:**
- Inherited infrastructure, undocumented configurations, and legacy processes must be investigated before modification.
- "It looks unused" is not sufficient justification for removal. Absence of visible traffic, monitoring alerts, or documentation does not mean absence of function.
- When the investigation reveals there is no good reason for something to exist — or that the reason no longer applies — act decisively. The principle has done its job.
- Document the findings of the investigation regardless of outcome.

*Demonstrated in practice: A publicly exposed remote access tool discovered on domain controllers during initial environment mapping. The investigation was immediate, the purpose was non-existent, and the remediation was same-day. Chesterton's Fence applied; the fence came down.*

---

### AD-6 — Documentation Is a Living System

**Statement:** Documentation that is not accessible, maintained, and actively used is not documentation — it is an artifact.

**Rationale:** Stale documentation is worse than no documentation. It gives false confidence, misleads the people who act on it, and creates liability when decisions are made on outdated information. Documentation earns its value by being current, findable, and owned.

**Implications:**
- Documentation belongs in a system where it can be discovered without asking someone: a repo, a wiki, a published internal site. An SMB share with ungoverned versions is a documentation graveyard.
- Every document needs an owner and a review cadence. Ownerless documentation drifts toward inaccuracy.
- Outdated documents must be removed or explicitly superseded, not left to accumulate alongside current material.
- Where SMB-based storage is unavoidable, strong governance and active cleanup processes are non-negotiable.

---

## Risk & Security

---

### RS-1 — Plan for Failure; Recovery Is a Design Requirement

**Statement:** Failure is inevitable; the architecture must account for failure modes and recovery paths from the earliest stages of design.

**Rationale:** Backup platforms, failover architectures, and disaster recovery procedures that are designed after the primary system is built are afterthoughts. They reflect the wrong failure in the wrong order. Recovery capability is a design input, not a retrofit.

**Implications:**
- Recovery time and recovery point objectives must be defined before architecture is finalized, not after.
- Every system with a recovery requirement must be tested against that requirement. Untested recovery is assumed recovery, which is not recovery.
- Disaster recovery plans must be exercised, not just documented. A plan that has never been run is a hypothesis.

*Demonstrated in practice: A catastrophic datacenter water event resulted in nearly 1PB of customer backup data at risk. Zero customer data was lost — the result of a recovery architecture that had been designed and validated in advance, not improvised during the crisis.*

---

### RS-2 — Document Known Risks Explicitly

**Statement:** Every known risk must be documented with an owner, a mitigation status, and — where accepted — a recorded rationale for acceptance.

**Rationale:** A risk that lives only in someone's head is a liability. When that person leaves, the risk becomes unknown again. When the risk materializes, the organization has no record of prior awareness, no documented decision, and no clear accountability. Documented risk is manageable. Undocumented risk is not.

**Implications:**
- Risks identified during design, discovery, or operation must be entered into a risk register or equivalent tracking system.
- Every budget proposal that is declined despite containing a risk mitigation must be recorded as a risk acceptance decision, with the date and the approver.
- Near-misses are risks that almost triggered. They must be treated with the same documentation rigor as active risks.
- "We know about it" is not a risk management posture.

*Demonstrated in practice: A platform replacement proposal had been submitted and declined across multiple budget cycles, with each denial recorded. When the platform failed catastrophically, the post-incident approval conversation was unnecessary. The documented history spoke for itself.*

---

### RS-3 — Assume Compromise; Design for Compartmentalization

**Statement:** Security architecture must assume that any component can be compromised and limit the blast radius accordingly.

**Rationale:** Security through obscurity, perimeter-only defenses, and flat network architectures all share the same failure mode: once the perimeter is breached, everything is reachable. The correct model is to assume breach and design so that no single compromise yields access to everything. This is the operational definition of zero trust.

**Implications:**
- Administrative credentials and standard user credentials must be separated. The compromise of a standard account should not yield administrative access.
- Network segmentation must reflect actual trust boundaries, not just logical convenience.
- Every component should have the minimum access required to perform its function, and no more.
- Supply chain integrity is a security layer: verify software sources, validate hashes, restrict what enters the environment.
- The attack surface should be actively minimized: ports closed, services not running unless required, access not granted until needed.

*Demonstrated in practice: A management forest redesign eliminated pass-the-hash attack vectors through privilege separation and smart card enforcement, producing the first clean penetration test result for the organization in eleven years. Separately, a publicly exposed domain controller access tool discovered during environment mapping was remediated the day it was found.*

---

### RS-4 — Crises Create Organizational Momentum

**Statement:** A failure event creates a window for change that does not otherwise exist; the right response is to have the proposal ready before the crisis arrives.

**Rationale:** Organizations routinely defer investments in risk mitigation until the risk materializes. This is a predictable pattern, not a failure of judgment. The correct architectural response is to maintain a current, well-reasoned proposal for every documented risk so that when the window opens, it can be acted upon immediately.

**Implications:**
- Risk mitigation proposals should be maintained and updated regardless of prior budget decisions.
- When a crisis occurs, the technical response and the organizational response must happen simultaneously. Recovery and the proposal for permanent remediation are not sequential.
- The record of prior risk documentation removes the need to relitigate the problem during a crisis. It should be readily accessible.

---

## Decision Making & Delivery

---

### DD-1 — Requirements Before Design

**Statement:** Architecture cannot be finalized until the requirements — including organizational, budgetary, and operational constraints — are fully understood.

**Rationale:** A technically correct solution that cannot be implemented is not a solution. Requirements include not only what the system must do, but what the organization can build, operate, afford, and support. Constraints are inputs, not obstacles.

**Implications:**
- Design work that begins before requirements are gathered produces assumptions, not architecture.
- Requirements must be gathered from the people who will build and operate the system, not only from the people who requested it.
- When requirements are incomplete or changing, the design must be staged to defer commitment on the uncertain elements.
- The appropriate response to incomplete requirements is a bounded description of approaches, not a premature commitment to a design.

---

### DD-2 — Validate Before You Commit; Scale Validation to Risk

**Statement:** The appropriate level of proof-of-concept validation before architectural commitment scales with the risk of being wrong.

**Rationale:** Some decisions are easily reversed; others are not. High-stakes, difficult-to-reverse architectural decisions warrant formal proof-of-concept validation before commitment. Lower-risk decisions can move directly to proposal. The discipline is in correctly assessing which category a decision falls into and calibrating the validation effort accordingly.

**Implications:**
- For platform replacements, major migrations, or novel technology adoption: build and validate a proof of concept before finalizing the proposal.
- For incremental changes within known platforms: proposal first, with validation built into the delivery process.
- A proof of concept must test the specific assumptions the architecture depends on, not just demonstrate that the technology works in general.
- Proof-of-concept findings — including failures — must be documented and incorporated into the final design.

*Demonstrated in practice: During a major platform replacement program, a dev environment migration to the candidate platform preceded the full proposal — validating the architecture before organizational commitment. Separately, an automation replacement path was proven via proof of concept before the legacy platform decommission was proposed.*

---

### DD-3 — Align Continuously; Require Sign-Off at Delivery

**Statement:** Stakeholder alignment is maintained throughout design and delivery; formal acceptance is required before production sign-off.

**Rationale:** A solution delivered to a specification that no longer reflects stakeholder needs is a failed delivery regardless of technical correctness. Requirements drift, organizational priorities change, and misalignments that are caught early are cheap to correct. Misalignments caught at delivery are expensive. Formal acceptance at production is not bureaucracy — it is confirmation that the requirement was met, mitigated, or explicitly accepted as missed.

**Implications:**
- Stakeholders should be engaged at major design milestones, not only at kickoff and delivery.
- The level of engagement should be proportional to the significance of the decision — not every choice requires a meeting, but no major decision should surprise a stakeholder.
- Production sign-off requires documented confirmation that each requirement has been met, formally mitigated, or explicitly accepted as out of scope.
- Acceptance must come from the parties responsible for each dimension: technical, operational, budgetary, and business.

---

### DD-4 — Scope the Full Problem Before Designing the Solution

**Statement:** Discovery must precede design; the stated problem is often not the complete problem.

**Rationale:** The presenting problem is frequently a symptom or a partial view of a larger condition. Designing a solution to the stated problem without investigating the full scope produces solutions that are technically correct and practically insufficient. Discovery is not overhead — it is the foundation of a durable design.

**Implications:**
- Initial discovery should treat the stated scope as a hypothesis, not a constraint.
- Physical infrastructure, dependencies, organizational context, and historical decisions must all be understood before design is finalized.
- Scope changes discovered during investigation should be documented and surfaced before design is committed, not absorbed silently.
- The cost of discovery is always less than the cost of a redesign after delivery.

*Demonstrated in practice: A storage fabric replacement scoped as a switch swap revealed during discovery that structured cabling, legacy infrastructure debt, and a stakeholder conflict all had to be addressed. The delivered project bore little resemblance to the original ask — and was significantly more valuable for it.*

---

## People & Teams

---

### PT-1 — Hire for DNA; Teach Technical Skills

**Statement:** Critical thinking, intellectual honesty, and the capacity to learn are hiring prerequisites; technical skills are trainable.

**Rationale:** Technical skills in specific platforms and tools have a half-life. The engineer who can think carefully under pressure, ask the question everyone is avoiding, and tell you something isn't working before it becomes a crisis is the one who makes a team durable. That capacity is either present or it isn't. Platform knowledge can be developed.

**Implications:**
- Interview processes must assess reasoning and judgment, not just technical recall.
- Onboarding investment in platform-specific skills is expected and planned for.
- A technically expert engineer who cannot communicate risk, work collaboratively, or self-correct is a liability in proportion to their expertise.

---

### PT-2 — A Leader Serves Their Staff

**Statement:** Leadership exists to remove obstacles, provide context, advocate for the team, and create conditions for skilled people to do good work.

**Rationale:** The people closest to the work have the best information about what the work requires. A leader who hoards decisions, filters information, or optimizes for their own visibility at the expense of the team's effectiveness is actively degrading the organization's capacity. Servant leadership is not a management style — it is the correct model for technical teams where the work is complex and the expertise is distributed.

**Implications:**
- A leader's primary operational question is: what is preventing my team from doing their best work, and how do I remove it?
- Recognition belongs to the team. A leader who takes credit for team outcomes undermines the trust that makes the team function.
- Escalation, advocacy, and political navigation within the organization are leadership responsibilities, not impositions on the team.
- This principle is demonstrated through consistent behavior, not stated in meetings.

---

### PT-3 — Turning a Critic into a Collaborator Is a Leadership Skill

**Statement:** Opposition that is engaged directly and given a genuine role in the outcome becomes advocacy; opposition that is ignored or escalated becomes an organizational liability.

**Rationale:** Technical organizations contain people with strong opinions and direct experience. When those opinions manifest as resistance to a project, the instinct to ignore or route around the critic is understandable and usually wrong. Critics often have legitimate insight. Giving them a real role in the outcome — asking for their expertise rather than their approval — changes the dynamic and frequently improves the result.

**Implications:**
- Identify resistance early. Stakeholder opposition that is discovered late in a project is harder to address and more disruptive.
- Approach critics as sources of expertise, not obstacles. Ask what they know, not whether they agree.
- Give critics genuine authorship over some aspect of the outcome. People support what they help build.
- Recognize their contribution meaningfully when the project succeeds.

*Demonstrated in practice: Fibre Channel migration — a skeptical senior peer became a project advocate after being privately asked for his expertise on a plan he'd been criticizing publicly.*

---

### PT-4 — Communicate Across Fluency Levels

**Statement:** Technical findings must be translated into the language of each audience; the same information requires different framing for engineers, operators, and organizational leadership.

**Rationale:** A technically correct message delivered in the wrong register is an ineffective message. Leadership does not need to understand the implementation — they need to understand the risk, the cost, and the decision being asked of them. Engineers need to understand the constraints and the tradeoffs. Operators need to understand what changes and what doesn't. These are different conversations.

**Implications:**
- Architecture proposals should address financial, operational, and strategic dimensions explicitly, not just the technical design.
- Risk communication to leadership should be framed in terms of business impact, not technical failure modes.
- Analogy is a valid and often powerful communication tool when translating complex technical concepts for non-technical audiences.
- The ability to hold a technical and an organizational conversation simultaneously is a core competency for infrastructure leadership.

---

*Grady Peterson | [gradyp.com](https://gradyp.com)*
*Source: [github.com/gpeterson78](https://github.com/gpeterson78)*

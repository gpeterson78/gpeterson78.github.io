# Architecture Decision Governance

This repository contains my architecture principles, decision templates, and project decision records. It serves as a personal reference, a professional resource, and a working example of how I approach infrastructure architecture and technical decision-making.

It is public by design. Architecture is most useful when it is shared.

---

## Repository Contents

| Document | Purpose |
|---|---|
| [`architecture-principles.md`](./architecture-principles.md) | The foundational principles that govern all architectural decisions |
| [`template-decision.md`](./template-decision.md) | Pre-decision analysis template — use before committing to a design |
| [`template-adr.md`](./template-adr.md) | Architecture Decision Record template — the permanent record of a finalized decision |
| [`template-project-intake.md`](./template-project-intake.md) | Project intake template — the full project record from initiation through delivery |
| [`projects/`](./projects/) | One folder per project, containing that project's intake document and ADRs |

---

## How to Use This Repo

### The Core Pattern

Every significant technical decision should leave a record. This repo implements that pattern using three document types that work together:

```
Project Intake (one per project)
    └── Decision Template (working doc, one per significant decision)
            └── ADR (permanent record, promoted from Decision Template)
```

The **Project Intake** is opened at the start of a project and updated at each milestone. It is the container for everything about that project — requirements, risks, decisions, stakeholder alignment, and production sign-off.

The **Decision Template** is a working document you fill out before committing to a design. It is not a permanent record — it is a thinking tool. When a decision is finalized, promote it to a formal ADR and link it from the Project Intake.

The **ADR** is the permanent record. Once accepted, it is never edited — it is only superseded by a new ADR. Future engineers (or future you) reading this repo should be able to understand not just what was decided, but why, and what alternatives were considered.

---

## Starting a New Project

1. Create a new folder under `projects/` named for the project:
   ```
   projects/
   └── YYYY-MM-project-name/
       ├── intake.md
       └── adr/
           ├── ADR-001-platform-selection.md
           └── ADR-002-deployment-model.md
   ```

2. Copy [`template-project-intake.md`](./template-project-intake.md) into the folder as `intake.md` and begin filling it out during discovery.

3. For each significant decision during the project, copy [`template-decision.md`](./template-decision.md) as a working document. Work through it, then promote the finalized decision to an ADR using [`template-adr.md`](./template-adr.md).

4. Link each ADR from the decisions table in `intake.md`.

5. Update the intake document at each milestone. Close it with production sign-off.

---

## What Counts as a Significant Decision?

Not every choice needs an ADR. Use judgment. A decision warrants an ADR when:

- It is difficult or expensive to reverse
- It introduces a new platform, vendor, or technology
- It affects more than one team or system
- It involves an accepted risk
- Future engineers would reasonably ask "why did they do it this way?"

Routine operational choices — patching, minor configuration changes, standard deployments — do not need ADRs.

---

## Folder Structure

```
.
├── README.md                        # This file
├── architecture-principles.md       # Governing principles
├── template-decision.md             # Decision analysis template
├── template-adr.md                  # ADR template
├── template-project-intake.md       # Project intake template
└── projects/
    └── YYYY-MM-project-name/
        ├── intake.md                # Project intake document
        └── adr/
            └── ADR-NNN-title.md     # One file per decision
```

---

## Using This Approach in Other Systems

This repo structure maps directly to how this process should work in other documentation platforms. The folder = project pattern works in:

- **Confluence**: one Space or top-level page per project, child pages for intake and each ADR
- **SharePoint**: one folder per project in a Document Library, with intake and ADR documents
- **Notion**: one database entry per project, with linked pages for intake and decisions
- **Shared folder / SMB**: same folder structure as this repo — but requires strong governance, a single source of truth, and an active cleanup process to avoid version drift

Regardless of platform, the pattern is the same: one container per project, decisions recorded as they are made, the intake document as the authoritative project record. The platform is a deployment decision. The structure is architectural.

---

## Principles Reference

All templates in this repo reference the [Architecture Principles](./architecture-principles.md) by code (e.g., `AD-2`, `RS-1`). These codes are stable identifiers — a reference to `RS-2` in an ADR always means the same principle regardless of when it was written.

---

## About

These documents reflect my approach to infrastructure architecture developed over twenty years of practice across healthcare, education, media, and enterprise environments. They are a working reference, not a finished artifact — they will evolve as practice does.

More context, case studies, and the reasoning behind these principles can be found at [gradyp.com](https://gradyp.com).

---

*Grady Peterson | [gradyp.com](https://gradyp.com) | [github.com/gpeterson78](https://github.com/gpeterson78)*

# P.A.R.K.I.T — Project Roadmap

This document shows the current project phase, major steps, and dependencies.

Detailed tasks, owners, and progress are managed on the `Project Board`.

---

## Current Status

**Current focus:** LED Matrix Integration  
**Current phase:** Research & Evaluation  
**Next milestone:** Architecture Selection

No final LED architecture has been selected yet.

---

## Roadmap

```text id="ld6m8s"
LED Matrix Integration
│
├── Requirements & Criteria                 ✓ Drafted
│
├── Research & Evaluation                   ● In progress
│   └── Hardware, architecture, connections,
│       software, costs and constraints
│
├── Architecture Selection                  ○ Pending
│
├── Proof of Concept                        ○ Pending
│   └── Validate selected technical approach
│
├── Administration Approval                 ○ Pending
│   └── Prepare installation proposal
│       and obtain Facility Management approval
│
├── Implementation                          ○ Pending
│   └── Parkit integration and controller software
│
├── Procurement & Installation              ○ Pending
│   └── Hardware, cabling, power and mounting
│
├── System Testing                          ○ Pending
│
└── Deployment                              ○ Pending
```

**Legend:** `✓` Drafted · `●` In progress · `○` Pending

---

## Phases

| Phase | Expected Outcome |
|---|---|
| **Requirements & Criteria** | Requirements and evaluation criteria are documented. |
| **Research & Evaluation** | Technical options, costs, risks and constraints are understood. |
| **Architecture Selection** | Preferred architecture is selected and documented. |
| **Proof of Concept** | Main technical assumptions are validated with available hardware. |
| **Administration Approval** | Installation proposal is prepared and Facility Management approval is obtained. |
| **Implementation** | Parkit integration and required controller software are implemented. |
| **Procurement & Installation** | Required hardware is acquired and physically installed. |
| **System Testing** | Complete solution is validated against the requirements. |
| **Deployment** | Solution is operational and final documentation is completed. |

---

## Key Dependencies

| Step | Depends on |
|---|---|
| Architecture Selection | Research & Evaluation |
| Proof of Concept | Selected architecture and available hardware |
| Administration Approval | Defined architecture and installation requirements |
| Production Implementation | Selected and validated architecture |
| Procurement & Installation | Facility Management approval |
| System Testing | Implementation and installation |
| Deployment | Successful system testing |


> **Facility Management approval is a project gate:** physical installation and related infrastructure changes must not proceed before approval.

See [`workstream/project-presentation/`](workstream/project-presentation/) for the approval workstream.
# P.A.R.K.I.T — Project Roadmap

This document shows the current project phase, major steps, and dependencies.

Detailed tasks, owners, and progress are managed on the `Project Board`.

---

## Current Status

**Current focus:** LED Matrix Integration  
**Current phase:** Detailed Architecture & Hardware Validation  
**Next milestone:** Architecture Validation (PoC)

**Selected direction:** Raspberry Pi 4 with SIM-based mobile internet, reusing the existing Pico W / Interstate 75 W and RGB LED panels where possible.

The detailed connections, required components, and complete architecture still need validation.

---

## Roadmap

```
LED Matrix Integration
│
├── Requirements & Criteria                 ✓ Drafted
│
├── Initial Research & Evaluation           ✓ Completed
│
├── Detailed Architecture                   ● In progress
│   └── Raspberry Pi 4, mobile internet (SIM),
│       connections, software, power, costs and risks
│
├── LED Hardware Test                       ✕ Blocked
│   └── Missing lab power supply(5 V, 8 A), connectors/clamps
│
├── Architecture PoC                        ○ Pending
│   └── Validate data flow from Parkit Cloud
│       to LED panels and update delay
│
├── Architecture Validation                 ○ Pending
│   └── Confirm final hardware and connections
│
├── Administration Approval                 ○ Pending
│   └── Obtain Facility Management approval
│       for physical installation
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

**Legend:** `✓` Completed / Drafted · `●` In progress · `○` Pending · `✕` Blocked

---

## Phases

| Phase | Expected Outcome |
|---|---|
| Requirements & Criteria | Requirements documented. |
| Initial Research & Evaluation | Initial options researched. |
| Detailed Architecture | Hardware, connections, software and costs defined. |
| LED Hardware Test | Two LED panels tested with different images. |
| Architecture PoC | Complete data flow and update delay tested. |
| Architecture Validation | Final architecture confirmed. |
| Administration Approval | Installation approved. |
| Implementation | Parkit and LED software integrated. |
| Procurement & Installation | Hardware acquired and installed. |
| System Testing | System validated against requirements. |
| Deployment | System operational and documented. |

---

## Key Dependencies

| Step | Depends on |
|---|---|
| Detailed Architecture | Initial Research |
| LED Hardware Test | Required equipment and power supply |
| Architecture PoC | Detailed Architecture and working test setup |
| Architecture Validation | PoC results |
| Administration Approval | Installation plan |
| Implementation | Validated architecture |
| Procurement & Installation | Facility Management approval |
| System Testing | Implementation and installation |
| Deployment | Successful system testing |


> **Facility Management approval is a project gate:** physical installation and related infrastructure changes must not proceed before approval.

See [`workstream/project-presentation/`](workstream/project-presentation/) for the approval workstream.

# LED Matrix Integration

## Goal

Integrate LED displays with the existing Parkit application to help drivers identify the correct parking space and see current parking availability.

The solution should allow displays, controllers, and communication technologies to be replaced without major changes to Parkit.

---

## Problem

Drivers may park in a different space than the one assigned to their reservation, which can create conflicts with other reservations.

Drivers also need a clear way to see whether a parking space is currently available.

---

## Use Cases

### UC-01 — Check Reserved Space

A driver already has a reservation and uses the LED display to confirm which parking space is assigned before parking.

### UC-02 — Find Free Space

A driver enters the parking area, sees that a parking space is currently free, and then reserves it in Parkit.

### LED Display Use Cases

The LED system must support different display scenarios based on parking availability, reservation periods, vehicle types, and special situations.

These include:

- Available and reserved parking spaces (AM, PM, full-day, and multi-day).
- Consecutive and upcoming reservations.
- Guest reservations with or without licence plate numbers.
- Motorcycle parking spaces.
- Reservation changes and cancellations.
- Unavailable parking spaces and communication errors.
- Special display designs for holidays.

The detailed scenarios are documented in [LED Display Use Cases](././led-display-use-cases.md).

---

## Target Users

**Primary**
- Drivers entering the parking area

**Secondary**
- Parking operators
- Parkit administrators
- Technical and maintenance staff

---

## Scope

- Integrate the LED system with the existing Parkit application.
- Transfer reservation and parking-space information from Parkit to the LED system.
- Evaluate and select suitable hardware and communication methods.
- Define an architecture that requires minimal changes to Parkit.
- Implement and configure the required software and hardware.
- Install, test, and validate the solution.
- Document the final architecture and implementation.

---

## Requirements

Requirement IDs are used to link requirements to features, technical decisions, and tests.

### Functional Requirements

Requirement ID prefixes:

| Prefix | Meaning |
|---|---|
| FR | Functional Requirement |
| LP | Licence Plate Requirement |
| DISP | Display Requirement |
| INT | Integration Requirement |
| REL | Reliability Requirement |
| SEC | Security Requirement |
| HW | Hardware & Infrastructure Requirement |

---

| ID | Requirement |
|---|---|
| `FR-01` | The system must display the parking space assigned to the driver's reservation. |
| `FR-02` | The system must show whether a parking space is currently available for reservation. |
| `FR-03` | Displayed information must match the current reservation data in Parkit. |
| `FR-04` | LED displays must reflect reservation changes in Parkit within a maximum of 1 minute. |
| `FR-05` | The system must support morning, afternoon, and full-day reservations. |
| `FR-06` | The system must correctly represent when a parking space is available or reserved. |
| `FR-07` | Displayed parking availability must remain current. |

### Licence Plate Requirements

| ID | Requirement |
|---|---|
| `LP-01` | The system must support the licence plate formats required by the project. |
| `LP-02` | Different supported licence plate lengths and characters must be handled. |
| `LP-03` | A consistent format for displaying licence plates must be defined. |
| `LP-04` | Privacy must be considered when licence plate information is displayed. |

### Display Requirements

| ID | Requirement |
|---|---|
| `DISP-01` | LED information must be readable from the required distance and viewing angles under the parking area's lighting conditions. |
| `DISP-02` | The display must support the required content, characters, and lines. |
| `DISP-03` | Information must remain readable under expected lighting conditions. |
| `DISP-04` | The system must define how content is handled when it does not fit on the display. |
| `DISP-05` | Displays must be installed where drivers can clearly see the relevant parking information when entering or approaching the parking spaces. |
| `DISP-06` | The display must use accessible colour combinations and must not rely on colour alone to communicate information, ensuring readability for users with colour vision deficiencies. |

### Integration Requirements

| ID | Requirement |
|---|---|
| `INT-01` | The LED system must receive the required reservation and parking-space information from Parkit. |
| `INT-02` | A clearly defined interface must be used between Parkit and the LED system. |
| `INT-03` | LED-specific logic should be separated from Parkit's core business logic. |
| `INT-04` | Replacing a display or controller should not require major changes to Parkit. |
| `INT-05` | Failure of the LED system must not prevent Parkit from operating normally. |

### Reliability Requirements

| ID | Requirement |
|---|---|
| `REL-01` | Communication failures must be detected. |
| `REL-02` | Communication should be retried or restored automatically where appropriate. |
| `REL-03` | Communication and integration errors must be logged. |
| `REL-04` | The system must avoid displaying outdated or incorrect parking information when current data is unavailable. |
| `REL-05` | The system must automatically reconnect after a mobile network failure. |
| `REL-06` | The LED software must automatically retry failed API requests and recover after connection is restored. |
| `REL-07` | LED displays must show a safe status when current parking information is unavailable. |

### Security Requirements

The following security requirements apply to both architecture options:

- Option A — Without Orchestrator: Each LED controller communicates directly with the Parkit API.
- Option B — With Orchestrator: A central orchestrator communicates with Parkit and distributes information to the LED controllers.
`A / B` indicates that a requirement applies to both architecture options.

The requirements are further examined in [LED Integration — Security & Architecture Evaluation Spec](research/security-architecture/README.md).

#### Authentication

| ID | Requirement | Option |
|---|---|---|
| `SEC-01` | Only authorized systems or users may control the LED displays. | A / B |
| `SEC-02` | Unauthorized changes to displayed information must be prevented. | A / B |
| `SEC-03` | Communication between Parkit and the LED system must be appropriately secured. | A / B |
| `SEC-04` | Physical access to displays, controllers, and related hardware must be considered. | A / B |
| `SEC-05` | Only registered and authorized devices may access the LED integration interfaces. | A / B |
| `SEC-06` | Each device must verify the identity of the system it communicates with. | A / B |
| `SEC-07` | Authentication mechanisms must be suitable for the selected hardware. | A / B |
| `SEC-08` | Credentials must not be exposed through logs or transmitted without appropriate protection. | A / B |
| `SEC-09` | The feasibility of mutual device authentication must be evaluated. | A / B |

#### Authorization

| ID | Requirement | Option |
|---|---|---|
| `SEC-10` | The LED system must have read-only access to the reservation and parking information required for display operation. | A / B |
| `SEC-11` | Controllers must not be able to modify reservations or other Parkit business data. | A / B |
| `SEC-12` | Access should be restricted to the required parking spaces and operations. | A / B |
| `SEC-13` | Unauthorized devices must not be able to change displayed information. | A / B |
| `SEC-14` | Permission boundaries between Parkit, the orchestrator (if used) and controllers must be documented. | A / B |

#### Communication Security

| ID | Requirement | Option |
|---|---|---|
| `SEC-15` | Communication with the Parkit API must use an appropriately secured connection. | A / B |
| `SEC-16` | Server identity verification and certificate validation must be evaluated. | A / B |
| `SEC-17` | The local communication channel must protect against unauthorized commands and data modification. | B |
| `SEC-18` | Replay protection and message freshness must be considered. | A / B |
| `SEC-19` | Required network ports and exposed services must be minimized. | A / B |

#### Credential Management

| ID | Requirement | Option |
|---|---|---|
| `SEC-20` | Credentials must be protected against unauthorized access. | A / B |
| `SEC-21` | Credentials must be revocable when devices are lost, replaced or compromised. | A / B |
| `SEC-22` | Credential rotation must be possible without unnecessary system disruption. | A / B |
| `SEC-23` | The impact of storing credentials on eight controllers versus one orchestrator must be evaluated. | A / B |

#### Caching and Data Freshness

| ID | Requirement | Option |
|---|---|---|
| `SEC-24` | Cached reservation data must have a defined validity period. | A / B |
| `SEC-25` | Displays must not present expired information as current. | A / B |
| `SEC-26` | The system must support reservation updates within one minute, as required by `FR-04`. | A / B |
| `SEC-27` | When current information is unavailable, displays must enter a defined safe state. | A / B |
| `SEC-28` | Cache invalidation, recovery after reconnection and time synchronization must be evaluated. | A / B |

#### Physical and Operational Security

| ID | Requirement | Option |
|---|---|---|
| `SEC-29` | Physical access to controllers, network equipment and the orchestrator (if used) must be considered. | A / B |
| `SEC-30` | Devices must not expose unnecessary debugging or administrative interfaces. | A / B |
| `SEC-31` | Security-relevant failures must be logged without exposing sensitive data. | A / B |
| `SEC-32` | The LED system must not compromise normal Parkit operation. | A / B |



### Hardware & Infrastructure Requirements

| ID | Requirement |
|---|---|
| `HW-01` | Selected hardware must be compatible with the existing project infrastructure. |
| `HW-02` | Hardware must be suitable for the intended installation environment. |
| `HW-03` | Individual components should be replaceable without major changes to Parkit or the overall architecture. |
| `HW-04` | Additional displays or controllers should be addable without major redesign. |
| `HW-05` | Reliable communication must be possible between cloud-hosted Parkit and the LED equipment in the parking area. |
| `HW-06` | The orchestrator must use reliable storage (microSD or SSD) for the operating system and software. |
| `HW-07` | The LED system must use mobile internet via SIM card to connect to Parkit. |
| `HW-08` | The mobile connection must support regular polling and LED updates within 1 minute. |
| `HW-09` | The SIM data plan must provide enough monthly data for continuous operation. |
---

## Evaluation Criteria

Possible architecture and hardware options should be evaluated using the same criteria.

| Criterion | What is evaluated |
|---|---|
| **Visibility** | Readability at the required distance and lighting conditions |
| **Display capacity** | Supported content, characters, lines, and brightness |
| **Connectivity** | Communication interfaces, coverage, protocols, and reliability |
| **Software support** | APIs, libraries, documentation, and maintainability |
| **Integration effort** | Changes required in the existing Parkit application |
| **Replaceability** | Ability to replace components without major Parkit changes |
| **Compatibility** | Compatibility with Parkit and existing infrastructure |
| **Reliability** | Communication stability, failure handling, and recovery |
| **Scalability** | Ability to add or replace components |
| **Security & privacy** | Protection of systems, communication, and displayed information |
| **Lifecycle** | Hardware availability, vendor support, and replacement options |
| **Cost** | Hardware, installation, maintenance, replacement, electricity, and estimated 10-year cost |

---

## Expected Outcome

- A selected and documented LED integration architecture.
- Required hardware, communication methods, software, and libraries identified.
- Integration implemented without unnecessary coupling to specific LED hardware.
- Solution validated against the defined requirements.
- Final technical documentation transferred to the main `parkit-service` repository.

---

## Research

Research, architecture comparisons, hardware tests, and other working materials are maintained in [`research/`](research/).

Open project questions are tracked in [`project-notes/open-questions.md`](../../project-notes/open-questions.md).
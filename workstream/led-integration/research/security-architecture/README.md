# LED Integration — Security & Architecture Evaluation Spec

**Status:** Research — Architecture not yet decided.

**Summary:** Evaluate the security requirements and communication approaches for two possible LED integration architectures: direct communication between LED controllers and Parkit, and communication through a central orchestrator.

**Related:** `SEC-01` to `SEC-32`, `INT-01` to `INT-05`, `REL-01` to `REL-07`, `FR-04` in the [LED Integration README](../../README.md).

---

## Contents

1. [Problem](#1-problem)
2. [Evaluation Criteria](#2-evaluation-criteria)
3. [Out of Scope](#3-out-of-scope)
4. [Architecture Options](#4-architecture-options)
5. [Security Requirements](#5-security-requirements)
6. [Open Questions and Required Research](#6-open-questions-and-required-research)
7. [Validation and Tests](#7-validation-and-tests)
8. [Decisions this spec asks for](#8-decisions-this-spec-asks-for)

---

## 1. Problem

The LED displays must receive current parking and reservation information from Parkit.

Two possible architectures are currently under consideration:

- **Option A — Without Orchestrator:** Each LED controller communicates directly with the Parkit API.
- **Option B — With Orchestrator:** A central orchestrator communicates with Parkit and distributes information to the LED controllers.

The final architecture has not yet been selected.

The main challenge is determining how authentication, authorization, secure communication and credential management can be implemented reliably on the available hardware.

Both options must be evaluated against the same security requirements before an architecture decision is made.

## 2. Evaluation Criteria

| ID | Criterion | What is evaluated |
|---|---|---|
| C1 | Authentication | Devices must be able to verify the identity of the system they communicate with. |
| C2 | Authorization | Each component must have only the permissions required for its operation. |
| C3 | Secure communication | Communication must protect data integrity and confidentiality where required. |
| C4 | Credential management | Credentials must be securely stored, managed, rotated and revoked. |
| C5 | Device security | Unauthorized devices must not be able to control LED displays or access reservation information. |
| C6 | Data freshness | Outdated reservation information must not be displayed as current. |
| C7 | Reliability | Communication failures must be detected and handled safely. |
| C8 | Maintainability | Replacing or adding a controller must not require major changes to Parkit. |
| C9 | Monitoring | Relevant authentication, authorization and communication failures must be observable. |
| C10 | Attack surface | The number of exposed services, privileged components and trust boundaries must be evaluated. |

## 3. Out of Scope

This research does not include:

- **Implementation of security mechanisms.** Authentication, authorization, credential storage and rotation are evaluated here but will not be implemented as part of this research.
- **Parkit API implementation.** Endpoint design, request payloads and API changes are covered by the integration workstream (`INT-01`, `INT-02`).
- **Hardware and network selection.** The choice of controllers, 5G router, SIM plan and communication hardware is handled separately (`HW-01`, `HW-05`, `HW-07` to `HW-09`). This research only evaluates their security implications.
- **Caching implementation.** Cache location, validity and security risks are evaluated here, but the caching mechanism will not be implemented.

## 4. Architecture Options

### 4.1 Option A — Without Orchestrator

Each LED controller communicates directly with the Parkit API through the shared network connection.

**Proposed communication flow:**

`LED Controller → 5G/Wi-Fi Router → Parkit API`

The controller requests the information required for its assigned parking space.

**Security aspects to evaluate:**

- How each controller authenticates with the Parkit API.
- How controllers verify that they are communicating with the legitimate Parkit server.
- Whether each controller requires a separate credential.
- How access can be restricted to the assigned parking space.
- Where credentials are stored on microcontrollers.
- How credentials can be rotated or revoked.
- Whether the controllers can reliably establish HTTPS connections.
- How unauthorized or modified responses are prevented or detected.
- How failures and outdated data are handled.
- Whether caching on individual controllers is appropriate.
- What happens if a controller is stolen, replaced or compromised.

**Potential advantages:**

- No additional orchestrator is required.
- Fewer central components.
- Each controller operates independently.

**Potential risks:**

- Credentials must be managed across multiple controllers.
- Each controller requires secure communication capabilities.
- Security updates and credential rotation may require changes on several devices.
- A compromised controller could expose its credentials.

These risks must be assessed through research and testing.

### 4.2 Option B — With Orchestrator

A central orchestrator communicates with the Parkit API and distributes the required information to the LED controllers.

**Proposed communication flow:**

`Orchestrator → 5G Connection → Parkit API`

`LED Controller ↔ Orchestrator`

The exact direction and protocol of local communication remain open.

**Security aspects to evaluate:**

- How the orchestrator authenticates with Parkit.
- How the orchestrator verifies the identity of the Parkit server.
- How LED controllers authenticate with the orchestrator.
- How controllers verify that they are communicating with the legitimate orchestrator.
- Whether the orchestrator pushes updates or controllers request them.
- How authorization is enforced for individual parking spaces.
- Whether the orchestrator should cache reservation information.
- How cached information is protected and invalidated.
- How local communication is secured.
- How unauthorized devices are prevented from joining the local network.
- How credentials are stored and protected on the orchestrator.
- How orchestrator failure affects all displays.
- How compromised controllers or an orchestrator could affect the system.

**Potential advantages:**

- Parkit API credentials may be stored on one central device.
- Controllers may require less complex communication logic.
- Centralized caching and monitoring may be possible.
- Security policies may be easier to manage centrally.

**Potential risks:**

- The orchestrator becomes an additional security-sensitive component.
- Compromise of the orchestrator may affect all connected displays.
- Local communication requires its own authentication and protection.
- Orchestrator failure may affect the entire LED system.

These risks must be assessed through research and testing.

## 5. Security Requirements

The applicable security requirements are defined in the [LED Integration README](../../README.md) under Security Requirements (SEC-01 to SEC-32).

The requirements cover:
- Authentication and authorization
- Secure communication.
- Credential management.
- Caching and data freshness.
- Physical and operational security.

Both architecture options must be evaluated against these requirements.


## 6. Open Questions and Required Research

The unresolved security and communication questions are tracked in [Open Questions](../../../../project-notes/open-questions.md) under LED Matrix Integration.

These questions must be investigated before selecting the final architecture.

## 7. Validation and Tests

The following tests should be considered before selecting the final architecture.

| ID | Test | Options | Expected Result |
|---|---|---|---|
| T1 | Test HTTPS communication from an existing LED controller. | A | Stable, authenticated communication with correct server verification. |
| T2 | Attempt access using invalid or revoked credentials in a controlled test environment. | A/B | Access is rejected. |
| T3 | Verify access restrictions for different parking spaces. | A/B | Devices cannot access data outside their assigned scope. |
| T4 | Test secure communication between orchestrator and controller. | B | Only authorized devices can exchange accepted messages. |
| T5 | Simulate loss of connectivity. | A/B | The display enters the defined safe state when data is no longer valid. |
| T6 | Test reservation changes and caching. | A/B | Changes are reflected within the required one-minute interval. |
| T7 | Evaluate credential rotation and device replacement. | A/B | Access can be updated or revoked without compromising other devices. |
| T8 | Compare authentication and security maintenance effort. | A/B | Differences between both architectures are documented. |
| T9 | Review logging and error handling. | A/B | Security-relevant failures are recorded without exposing credentials. |

Tests must be performed in an authorized development or test environment.

## 8. Decisions this spec asks for

This research does not select a final architecture.

Before implementation, the following decisions are required:

1. Determine whether direct communication from LED controllers to Parkit is technically and securely feasible.
2. Determine whether a central orchestrator provides sufficient security and operational benefits to justify the additional component.
3. Select suitable authentication and authorization mechanisms.
4. Define how device identities and credentials will be managed.
5. Define the communication direction and protocol for each required connection.
6. Decide whether caching is required and where it should be implemented.
7. Define failure handling and the safe display state.
8. Compare both architectures against the evaluation criteria and select the most suitable approach.
9. Record the selected architecture and its security rationale in [decisions.md](../../../../project-notes/decisions.md) and close the related entries in [open-questions.md](../../../../project-notes/open-questions.md).


**Expected outcome:** A documented comparison of both architecture options, including their security requirements, unresolved risks and required validation tests. The final architecture will be selected only after the relevant research and testing have been completed.
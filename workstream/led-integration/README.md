## LED Matrix Integration

### Goal

Investigate, design, and implement a suitable LED matrix integration for the existing Parkit application.

The main purpose of the integration is to help drivers park in the correct reserved parking space by clearly showing their assigned space when they enter the parking area.

The solution should also be flexible enough to allow LED displays, controllers, or communication technologies to be replaced in the future without major changes to the Parkit application.

---

### Problem

Drivers do not always park in the parking space assigned to their reservation. As a result, they may occupy spaces reserved for other users and cause conflicts between reservations.

To reduce this problem, drivers need a clear and visible indication of their assigned parking space when entering the parking area.

An LED display can be used to show this information at the entrance or another suitable location.

Before implementation, the available LED hardware, communication options, software interfaces, installation requirements, reliability, security, and integration with Parkit need to be evaluated.

---

### Target Users

**Primary user**
- Drivers entering the parking area

**Secondary users**
- Parking operators
- Parkit administrators
- Technical and maintenance staff

---

### Scope

- Integrate an LED matrix system with the existing Parkit application.
- Determine how reservation and parking space information is transferred from Parkit to the LED system.
- Evaluate and select suitable LED displays, controllers, and communication interfaces.
- Define an integration architecture that requires minimal changes to the existing Parkit application.
- Implement and configure the required software and hardware components.
- Install, test, and validate the solution.
- Document the final architecture, configuration, and implementation.

---

### Requirements

1. **Parking information**
   - The system must display the parking space assigned to the driver's reservation.
   - The displayed information must match the current reservation data in Parkit.
   - The displayed information must be updated when the reservation or assigned parking space changes.
   - The parking space must be clearly identifiable by the driver.

2. **Reservation periods**
   - The system must support the reservation periods used by Parkit, including morning, afternoon, and full-day reservations.
   - The system must correctly show when a parking space becomes available again.
   - Availability information such as `FREE UNTIL 12:00` should be supported where needed.

3. **Licence plates**
   - The system must support the licence plate formats required by the project.
   - Different licence plate lengths and supported characters must be handled.
   - A consistent format for displaying licence plates must be defined.
   - Privacy must be considered when licence plate information is displayed.

4. **Display**
   - Information must be clearly readable by drivers when entering the parking area.
   - The display must support the required number of characters and lines.
   - Information must remain readable under expected daylight and nighttime conditions.
   - The system must define how information is handled when it does not fit on the display.
   - The installation location and required viewing distance must be considered when selecting the display.

5. **Parkit integration**
   - The LED system must receive the required reservation and parking space information from Parkit.
   - A clearly defined interface must be used between Parkit and the LED system.
   - LED-specific logic should be separated from Parkit's core business logic.
   - Replacing the LED display or controller should not require major changes to Parkit.
   - A failure of the LED system must not prevent Parkit from operating normally.

6. **Reliability and failure handling**
   - Communication failures between Parkit and the LED system must be detected.
   - Communication should be retried or restored automatically where appropriate.
   - Communication and integration errors must be logged.
   - The system must avoid displaying outdated or incorrect parking information when current data is unavailable.

7. **Security**
   - Only authorized systems or users may control the LED display.
   - Unauthorized changes to the displayed information must be prevented.
   - Communication between Parkit and the LED system must be appropriately secured.
   - Physical access to the display, controller, and related hardware must be considered.

8. **Hardware**
   - The selected hardware must be compatible with the existing infrastructure.
   - The hardware must be suitable for the intended installation environment.
   - Individual components should be replaceable without major changes to the overall solution or Parkit.
   - The solution should allow additional displays or controllers to be added later if needed.

---

### Evaluation Criteria

Possible solutions should be evaluated using the following criteria:

- **Visibility** — readability from the required distance and under expected lighting conditions.
- **Display capacity** — supported text length, number of lines, characters, and brightness.
- **Connectivity** — available communication interfaces, protocols, and reliability.
- **Software support** — available APIs or libraries, documentation, compatibility, and maintainability.
- **Integration effort** — amount of modification required in the existing Parkit application.
- **Replaceability** — ability to replace displays, controllers, or other components without major changes to Parkit.
- **Compatibility** — compatibility with the existing Parkit system and infrastructure.
- **Reliability** — communication stability, failure handling, and recovery.
- **Scalability** — ability to add or replace displays and other components in the future.
- **Security and privacy** — protection against unauthorized access and inappropriate exposure of information.
- **Lifecycle** — hardware availability, vendor support, and long-term replacement options.
- **Cost** — initial cost, installation, maintenance, replacement, and estimated cost over 10 years.

---

### Expected Outcome

- **Defined architecture** — a clear design for how Parkit communicates with the LED system while keeping hardware-specific logic separate from the core application.
- **Selected components** — suitable LED displays, controllers, communication methods, and required software components are identified.
- **Implemented integration** — the selected components are connected and integrated with Parkit.
- **Validated solution** — the solution is tested to confirm that drivers receive clear and correct parking space information without affecting Parkit's normal operation.
- **Documentation** — the architecture, configuration, installation, and relevant technical decisions are documented.

---

### Current Work

The current work is focused on research and evaluation.

| Area | Purpose |
|---|---|
| `led-basics/` | Understand LED matrix technology and identify suitable solutions |
| `existing-hardware/` | Identify available hardware and determine whether and how it can be reused |

These areas correspond to the research activities currently tracked in the project task tracker.

---

### Working Materials

The folders above contain research notes, diagrams, comparisons, test results, and other working materials produced during the project.

These materials will evolve as the research progresses and may later be included in the final technical documentation.
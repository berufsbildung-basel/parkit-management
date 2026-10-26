Short notes from project meetings: topics discussed, agreed directions, clarifications, and adjustments.

**Keep it brief — only key points, not full meeting notes.**

29-09-26

 ### Discussed

- Subtickets and what information should be included in their documentation.    
- What should be included in the overview presentation.
- We visited the parking area and had a look around.
- Git basics and the most important Git commands.
- Which software/OS we should install on the Intel NUC. Ubuntu is currently one of the options, but we’d like to get an expert opinion before making a decision.

Current tasks(apprentices)
- Install Rails (you can use `rbenv` or `mise`).
- Create a very simple Ruby program. If you feel comfortable, you can also try building a simple Rails app.
- Push your project to GitHub and add me as a collaborator.

softare decisions needed:
- operating system (most likely Debian Linux)
- controller driver / daemon


---

05-10-26

 ### Discussed

 - **Project management & documentation**
  - Add technical and non-technical **requirements**
  - Define **features**
  - Define generic **criteria** for comparing and replacing different options/components
- **Research**
  - Presentation of research on existing hardware and possible options, including **LoRa**, in the related sub-ticket.
  - We now have a better overview of the hardware and options currently available.

 ### Open Questions

- Do we need an **Intel NUC**, or could another **Raspberry Pi** be used as the orchestrator?
- Why do we need **Raspberry Pi Pico W** specifically?
- Which hardware, software, libraries, and communication options are suitable?
- What are the costs of the different options, including potential replacement costs?

 ### Next Steps

 Before making any technical decisions or scheduling a meeting with the hardware expert, we will:

- Investigate and compare the available options.
- Define their main advantages, limitations, connections, and costs.
- Research the required software/libraries.
- Run a small test using the components we already have, including displaying a message on the LED panel.

 **No final technical decisions have been made yet.**

---

 ## 12-10-2026

### Discussed

- Reviewed last week's work on the three LED architecture options and the existing hardware test.
- Identified communication between the three parking levels as an important technical constraint that should be included in the requirements.
- Raspberry Pi is currently the main option to investigate as both orchestrator and controller.
- Identified two main LED use cases:
  - Let users check which parking space is assigned to their reservation.
  - Show which parking spaces are currently free.
- Identified the need to define how often the LED displays should be updated.
- Requirements should have IDs so future features, research, and tests can be linked to them.
- The existing LED hardware test could not be completed because the required connection/cable was missing. Daniel confirmed that he does not have it.

### To Investigate

- Communication options between the three parking levels.
- LoRa and mobile/cellular connection as possible options.
- Required LED display update frequency.

### Next Steps

- Complete and compare the three architecture options, with Raspberry Pi as the main focus.
- Add costs and explain why each option is or is not suitable.
- Confirm the required LED test setup with the hardware specialist and obtain the missing component if needed.
- Test the existing LED hardware once the required setup is available.
- Update the LED requirements with IDs and use cases.
- Arrange a meeting with the hardware specialist for Monday, if available.

---

## 19-10-2026 — Hardware Expert Meeting

### Discussed

- Parkit is hosted in the cloud. A direct Ethernet connection from the office to the parking area is not required.
- Mobile internet via SIM card is the selected communication direction. LoRaWAN is no longer being considered.
- Intel NUC and Raspberry Pi remain the two orchestrator options.
- Reusing the existing Intel NUC could avoid purchasing another computer.
- The existing Pico W / Interstate 75 W and RGB LED panels should be reused where possible.
- The architecture needs to be investigated in more detail, including data flow, cables, interfaces, and power connections.
- The system should use mains power, not batteries.

### Open Questions

- Should we use the existing Intel NUC or a Raspberry Pi?
- Which cellular router/modem and SIM plan should we use? Wingo was discussed as a possible provider.
- How will the orchestrator communicate with the LED controllers?
- What additional cables, adapters, and power supplies are required?
- What are the costs and technical risks of the proposed architecture?

### Next Steps

- Prepare a detailed end-to-end diagram on the whiteboard: Parkit Cloud → Mobile Internet → Orchestrator → Pico W / Interstate 75 W → LED panels.
- Identify the required connections and components at each step.
- Compare Intel NUC and Raspberry Pi using the project evaluation criteria.
- Document the technical risks.
- Complete the existing LED hardware test once the missing cable and power components are available.
- Test sending two different images to two LED panels and verify how the controller routes the display data.
- Test the complete data flow from Parkit Cloud to the LED panels using mobile internet (Architecture PoC).

**No final orchestrator or hardware configuration has been selected yet.**

---

## 26-10-2026 — Hardware Expert Meeting

### 1. Discussed

The meeting focused on the next steps for the LED Integration architecture.

We have three main technical topics:

1. **Power Distribution** — How to power 8 Interstate 75 W controllers and 16 LED matrices.
2. **Data Communication** — How to transfer data from Raspberry Pi to the LED controllers.
3. **Parkit API & Data Format** — What data Raspberry Pi needs to receive from the cloud-hosted Parkit application.

We need to move from a high-level architecture to more detailed technical solutions, including hardware, protocols, data formats, measurements, and testing.

### 2. Power Distribution

We need to define how to power all 8 LED units.

Each unit consists of:
- 1 × Interstate 75 W
- 2 × LED Matrix

**Total:** 8 controllers and 16 LED matrices.

**Next steps:**
- Research possible power distribution solutions.
- Identify the required voltage and current.
- Identify the required cables, power supplies, and additional components.
- Check which existing hardware can be reused.
- Prepare a comparison table of power options.
- Evaluate the options against the project requirements.

No final power distribution solution has been selected yet.

### 3. Data Communication

We need to define how data will travel through the system:

```text
Parkit (Heroku Cloud)
        ↓
Raspberry Pi — Orchestrator
        ↓
8 LED Controllers
        ↓
16 LED Matrices
```

The following options and components were discussed:

- WLAN / Wi-Fi.
- USB.
- RS-485 and other wired communication options.
- Raspberry Pi 4G HAT — an expansion board for mobile internet via SIM card.
- Reusing existing hardware and software where possible.

**Next steps:**
- Compare possible communication methods.
- Identify suitable communication protocols.
- Check what additional hardware is required.
- Define how one orchestrator can send different data to multiple controllers.
- Prepare a comparison table of communication options.
- Check which options meet the project requirements.

The selected communication method will affect the required hardware, cables, and software.

### 4. Parkit API v1

First, we need to review the existing Parkit API.

**Questions to investigate:**
- Is API v1 still up to date?
- Is it suitable for LED Integration?
- What data does it currently return?
- Can it provide reservation and availability information for all 8 parking spaces?
- What changes are needed if the existing API is not sufficient?

We should check the existing API before developing a new one.

Testing the API through a browser was also discussed.

### 5. Data Format — Orchestrator Input

We need to define and document exactly what data the Raspberry Pi should receive from Parkit.

**Questions to answer:**
- How should each parking space be identified?
- How should `FREE` and `RESERVED` be represented?
- Do we need to send the vehicle's licence plate?
- What reservation date and time information is required?
- What should the JSON response look like?

We need to prepare specific JSON payload examples.

**Example (not final):**

```json
{
  "parking_spot_id": 3,
  "status": "reserved",
  "licence_plate": "ZH 123456"
}
```

The final data format has not been defined yet.

We also need to decide what data the orchestrator should send to the LED controllers.

### 6. Testing & Measurements

We should start testing the software communication without waiting for the complete hardware setup.

Communication can be simulated locally without physical LED matrices.

**Two communication paths need to be tested:**

```text
Parkit Web Application
        ↓
Communication Test 1
        ↓
LED Orchestrator
        ↓
Communication Test 2
        ↓
LED Controllers
```

**What we need to measure:**
- Size of the transferred data.
- Data transfer time.
- Delay between request and response.
- Time required to update the displayed information.
- How the selected protocol affects communication.

Voltage and frequency were also mentioned during the meeting, but the exact details still need clarification.

The goal is to check whether the system can meet the requirement of updating LED information within **1 minute** after a reservation change.

### 7. Architecture Documentation

After the research, we need to update the existing architecture diagrams.

**Next steps:**
- Confirm the selected hardware.
- Show how data is transferred.
- Show how power is distributed.
- Specify the communication protocols.
- Show how the orchestrator communicates with Parkit and the LED controllers.
- Prepare a detailed Data Flow Diagram showing the full path from a reservation to the LED display.

The diagrams should reflect the technical solutions, not only the high-level concept.

### 8. Next Steps

| # | Task | Expected Outcome |
|---|---|---|
| 1 | Research Power Distribution | Comparison table of power options |
| 2 | Research Data Communication | Comparison table of communication options |
| 3 | Review Parkit API v1 | Check if the existing API is suitable |
| 4 | Define JSON Payload | Documented data format with examples |
| 5 | Define Communication Protocols | Suitable protocols and required hardware |
| 6 | Simulate Data Communication | Local tests without LED hardware |
| 7 | Measure Performance | Data size, transfer time, and delays |
| 8 | Update Architecture Diagrams | Updated C4 and Data Flow diagrams |
| 9 | Send PSU Examples to Dominik | Power supply examples for discussion |

### 9. Open Questions

- What is the final power distribution architecture?
- Should we use Wi-Fi or RS-485 for local data communication?
- Should we use a 4G HAT or a separate 4G router?
- Which parts of the existing prototype can be reused?
- Can API v1 be used without changes?
- What is the final JSON data format?
- Which protocol should be used between the orchestrator and controllers?
- What exact hardware and connection specifications are required?

### Meeting Outcome

Before selecting the final architecture and hardware, we need to define the required data, compare power and communication options, and validate the solutions through tests and measurements.

**No final decision has been made on Wi-Fi, RS-485, 4G HAT, or power distribution.**
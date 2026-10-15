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
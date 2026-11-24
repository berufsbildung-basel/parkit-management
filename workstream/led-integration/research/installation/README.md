README · MD
# Installation of LED matrices
 
Status: Proposal, not yet decided. Nothing in here is tested
 
## Contents
 
1. [Context](#1-context)
2. [Risks](#2-risks)
3. [Mounting Options](#3-mounting-options)
4. [Backplate](#4-backplate)
5. [Attaching the LED Panels to the Backplate](#5-attaching-the-led-panels-to-the-backplate)
6. [Dimensions, Weight, Ventilation, Cable Access](#6-dimensions-weight-ventilation-cable-access)
7. [Comparison Table](#7-comparison-table)
8. [Recommended Solution](#8-recommended-solution)
9. [3D-Model](#9-3d-model)
## 1. Context
 
We have 8 parking spaces; this document will outline the available options for mounting the unit separately, including the cover and fasteners.
 
Above each parking space, there is a metal rail; power cables will be routed through it, and LED panels indicating the status will be mounted on it.
 
## 2. Risks
 
1. **Lid material fatigue / cracking**
Material under sustained load + vibration may creep or crack at mount points over time.
 
2. **Wall thickness at mount points**
If the wall of the lid is too thin near the attachment point, it may crack or the threads may strip, regardless of the strength of the attachment itself.
 
3. **Vibration and impact**
Over time, the fastening loosens further due to vibration and accidental impacts.
 
4. **Exhaust, humidity, temperature swings**
In a parking garage, there is higher humidity, residual exhaust gases, and greater temperature fluctuations; this accelerates the corrosion of metal parts and places stress on the cover material due to thermal cycling.
 
## 3. Mounting Options
 
### Option 1 — Direct Mounting into the Backplate
 
The mounting hardware (clamp/bracket) bolts straight into the backplate itself, with no separate mounting plate in between.
 
**Pros:**
- Simplest, fewest parts
- No extra mounting plate to source or install
**Cons:**
- Backplate must be rigid enough at the mounting points to carry the full load directly
- Works best with a solid material (e.g. aluminium), not thin plastic
### Option 2 — Sliding Metal Backplate
 
The backplate is a separate metal piece, not part of the rest of the enclosure, and slides into the box like a removable sliding lid. The enclosure itself is anchored to the rail; the backplate carries the LED panels' and electronics' load inside it.
 
**Pros:**
- Lightweight enclosure shell (e.g. 3D-printed) combined with a metal part only where load-bearing strength is needed
- Backplate can be removed/slid out for maintenance without disassembling the whole unit
**Cons:**
- Needs a rigid slide-in channel so the backplate can't work its way loose over time
- One more moving part/interface than a one-piece design
**Electrical insulation:** a silicone insert (or another non-conductive layer) must be placed between the metal backplate and the electronics — controller board, panel driver PCBs, and connectors — so that no electronic component touches the metal directly.
 
### Option 3 — Support Shelf / Holders
 
A bracket or shelf is fixed to the rail, and the whole unit simply rests on it — no bolts through the enclosure itself.
 
**Pros:**
- No drilling or fastening into the enclosure at all
- Easiest to install and to swap the unit out
**Cons:**
- Relies entirely on gravity/friction — no positive retention against lateral movement or vibration
- A secondary retention strap or lip is strongly recommended given the vibration risk already noted in [Risks](#2-risks)
## 4. Backplate
 
| | Electrical safety (conductive?) | Fire resistance | Moisture | Corrosion | Weight | Availability |
|---|---|---|---|---|---|---|
| **3D-printed PETG/ASA** | Non-conductive — safe insulator | Burns | Doesn't absorb | Not applicable | ~0.4–0.6 kg | Print it yourself, sized exactly as needed |
| **3D-printed Fire-retardant ABS/PC FR (V0)** | Non-conductive — safe insulator | Self-extinguishing, but still combustible | Barely absorbs | Not applicable | ~0.4–0.6 kg | Print it yourself, sized exactly as needed |
| **Aluminium sheet** | Conductive — needs grounding/insulation around live parts | Non-combustible (A1) | Doesn't absorb | Not an issue (only the fasteners are) | ~1.9 kg | Cutting/bending order, takes a bit longer |
 
**Note:** for the plastic options, the whole enclosure can be 3D-printed as one piece, with a sliding/removable back cover made of metal instead — that way the mounting points, which carry the actual load, stay on the metal part, while the rest of the box can stay in plastic.
 
### Additional design requirements for the enclosure
 
Regardless of which material is chosen, the enclosure design must account for:
 
1. **Moisture protection**
Keep water, condensation, and dust out, even with vents open
 
2. **Cable openings**
Sized for the power and HUB75 data cables, without becoming a weak point for moisture
 
3. **Ventilation**
Enough airflow for the heat from 4 LED panels to escape
 
4. **Mounting to the metal rail**
A solid attachment point to the ceiling structure
 
5. **Mounting the LED panels**
A reliable way to fix the panels inside the enclosure
 
## 5. Attaching the LED Panels to the Backplate
 
| Method | Description | Pros | Cons |
|---|---|---|---|
| **Magnets** | Panel held in place by magnets mounted on the backplate, matching magnetic/metal points on the panel's back | Quick to attach/detach, no tools needed, no visible fasteners | Weaker hold under vibration; needs a flat metal contact surface; less resistant to lateral movement |
| **Bolts/screws** | Panel fixed with screws through its corner mounting holes into the backplate | Strong, reliable hold, resists vibration | Needs tools to attach/detach; more preparation on the backplate |
 
Both options require the enclosure to have reliable, pre-planned mounting points prepared in advance.
 
## 6. Dimensions, Weight, Ventilation, Cable Access
 
### Dimensions
 
```
           ◄──────────────── 675 mm ────────────────►
         ┌──────────────────────────────────────────┐  ▲
         │                                          │  │
         │              enclosure footprint         │ 355 mm
         │                                          │  │
         └──────────────────────────────────────────┘  ▼
                         depth: 44 mm
```
 
Outer enclosure footprint: ~675 × 355 mm, ~44 mm deep (from the current 3D model).
 
### Estimated weight
 
| Component | Weight |
|---|---|
| 4× LED panels (Waveshare RGB-Matrix-P5-64x32, confirmed) | ~1.9 kg (~474 g each) |
| Enclosure lid + tray (3D-printed) | ~0.4–0.6 kg |
| Aluminium backplate (3mm) | ~1.9 kg |
| **Total** | **~3.5–4.5 kg** |
 
The panel weight above is confirmed for the specific product ordered (AliExpress item 1005011661208809). The total is higher than the 2.5 kg figure used in earlier risk notes, so mounting hardware should be sized against this updated number rather than the original estimate.
 
### Ventilation
 
Vents should be side-mounted rather than top-mounted, since the unit sits flush against the ceiling and hot air has nowhere to rise into above it. Louvered vents (angled slats with a drip edge) are preferred over plain holes, so rain or condensation cannot enter directly. A small drip hole at the lowest point of the enclosure is recommended as a backup in case condensation forms inside. If passive airflow proves insufficient once built, a small filtered fan can be added as a fallback.
 
### Cable access
 
| Cable | Opening |
|---|---|
| Power (5V) | 9 mm, grommeted |
| HUB75 ribbon (data) | ~22×5 mm slot |
 
Both openings are already defined in the enclosure model, routed through the same rail that carries the existing cable ladder.
 
## 7. Comparison Table
 
| Criterion | Option 1 — Direct mounting | Option 2 — Sliding metal backplate | Option 3 — Support shelf |
|---|---|---|---|
| **Load capacity** | Depends on backplate material — good with aluminium, weak with plastic | High — load carried by the metal part | Good vertically, none laterally |
| **Vibration resistance** | Good if bolted into solid material | Good, provided the slide-in channel is rigid | Low without an extra retention strap |
| **Electrical safety** | Depends on material — metal needs insulation | Requires a silicone insert between metal and electronics | Not affected by the mounting itself |
| **Installation effort** | Low | Medium — backplate and shell are separate parts | Lowest |
| **Maintenance access** | Unit must be unbolted | Backplate slides out without removing the whole unit | Unit can be lifted off directly |
| **Parts count** | Lowest | Medium | Low, plus a retention strap |
 
## 8. Recommended Solution
 
**Option 2 — Sliding Metal Backplate**, with the LED panels attached using **bolts/screws** and a **silicone insert** between the metal backplate and the electronics.
 
This option keeps the load-bearing mounting points on metal, which addresses the material fatigue and wall-thickness risks listed in [Risks](#2-risks), while the rest of the enclosure can still be 3D-printed to the exact required size. It also allows the backplate to be removed for maintenance without taking the whole unit off the rail. Bolted panels are preferred over magnets because of the vibration expected in the parking garage.
 
## 10. 3D-Model

A 3D model will be created later.

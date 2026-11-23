 # Installation of LED matrices

Status: Proposal, not yet decided. Nothing in here is tested

## Contents

1. [Context](#1-context)
2. [Risks](#2-risks)
3. [Fastening Options](#3-fastening-options)
4. [Backplate](#4-backplate)
5. Attaching the LED Panels to the Backplate
6. Dimensions, Weight, Ventilation, Cable Access

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

## 3. Fastening Options

### Option A — Beam / Channel Clamp

The lid is suspended from the rail using two beam/channel clamps, gripping the flange of the rail without drilling into it. Each clamp carries a threaded stud (M8/M10) connecting to a mounting plate fixed to the lid.

- Minimum 2 clamps, symmetrically spaced, to prevent tilting and rotation.
- Clamp load rating should exceed the unit's weight with a safety margin.
- A reinforced metal mounting plate should transfer the load into the lid via multiple fasteners, rather than a single point on the plastic shell.
- A third anti-sway point is recommended to prevent swinging along the rail.

### Option B — Angle Brackets (L/Z-bracket)

L-shaped or Z-shaped brackets bolt into the rail using strut nuts on one flange, while the perpendicular flange bolts into the lid's corner posts.

- Minimum 4 brackets, one per corner, for a stable 4-point mount.
- Bracket material: steel or aluminum, minimum 2 mm thickness.
- Corner posts on the lid need through-holes with heat-set inserts.
- Strut nuts must match the rail's slot profile.

### Option C — DIN Rail + DIN Clips on the Lid

A short length of DIN rail (TS35) is fixed to the top of the lid. Standard DIN clips then attach the rail to a support structure on the metal rail, or via a rail-to-DIN adapter bracket.

- DIN rail segment should span at least 60–70% of the lid's width.
- Rail fixed to the lid with multiple screws into heat-set inserts.
- Requires a rail-to-DIN interface bracket, since DIN clips don't attach directly to the rail.
- Tool-free detachment for maintenance; generally lower load rating than a dedicated channel clamp — verify before relying on this as sole support.

## 4. Backplate 

| | Reliability | Fire resistance | Moisture | Corrosion | Weight | Availability |
|---|---|---|---|---|---|---|
| **3D-printed PETG/ASA** | Low — creeps over time | Burns | Doesn't absorb | Not applicable | ~0.4–0.6 kg | Print it yourself, sized exactly as needed |
| **3D-printed Fire-retardant ABS/PC FR (V0)** | Medium — holds shape better | Self-extinguishing, but still combustible | Barely absorbs | Not applicable | ~0.4–0.6 kg | Print it yourself, sized exactly as needed |
| **Aluminium sheet** | High — doesn't creep or fatigue | Non-combustible (A1) | Doesn't absorb | Not an issue (only the fasteners are) | ~1.9 kg | Cutting/bending order, takes a bit longer |

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

A reliable way to fix the panels inside the enclosur

## 5. Attaching the LED Panels to the Backplate


-----AA----
## 6. Dimensions, Weight, Ventilation, Cable Access
Outer enclosure footprint: ~675 × 355 mm, ~44 mm deep (from the current 3D model).
Estimated weight:
4× LED panels: ~1.4–1.8 kg
Enclosure lid + tray (3D-printed): ~0.4–0.6 kg
Aluminium backplate (3mm): ~1.9 kg
Total: roughly 3.5–4.5 kg — higher than the 2.5 kg figure used in earlier risk notes, so mounting hardware should be sized against this updated number, not the original estimate.
Ventilation: two perforated patches (≈3mm holes) on opposite side walls for passive cross-flow; keep clear of the backplate's structural mounting points. Vents should be side-mounted, not top-mounted — the unit sits flush against the ceiling, so hot air has nowhere to rise into above it. Louvered vents (angled slats with a drip edge) are preferred over plain holes so rain/condensation can't enter directly; a small drip hole at the lowest point of the enclosure is recommended as a backup in case condensation forms inside. If passive airflow proves insufficient once built, a small filtered fan can be added as a fallback.
Cable access: one Ø9mm grommeted hole for the power cable, one slot (~22×5mm) for the HUB75 ribbon — both already defined in the enclosure model, routed through the same rail that carries the existing cable ladder. 

## 8. Comparison Table

## 9. Recommended Solution

## 10. 3D-Model

A 3D model will be created later.

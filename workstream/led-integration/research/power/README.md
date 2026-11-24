# Production Power Spec for the Bay Displays

**Status:** Proposal, not yet decided. Nothing in here is tested on hardware. All numbers are calculated from datasheets and one assumption (5 A per tile), see [Open tests](#7-open-tests).

**Summary:** Each bay display gets its own 5 V supply (Mean Well RSP-200-5, 5 V / 40 A) inside the display, fed through a fused IEC inlet and a normal plug-in cord. All displays plug into one 16 A distribution box on the rail, fed from one Swiss 16 A socket. The team can install and move displays without changing the building installation. Worst case, the whole system draws about 975 W, or 4.6 A at 230 V, which is 26 % of one 16 A socket. Running the displays at lower brightness cuts this roughly in proportion, see [5.4](#54-brightness-as-a-lever).

**Related:** `HW-01` to `HW-04`, `DEC-001`, `DEC-007` in the [LED Integration README](../../README.md) and [decisions.md](../../../../project-notes/decisions.md). Builds on the [Display Size and Hardware Spec](../display-size/README.md) (4 P5 tiles + 1 Interstate 75 W per display, 8 displays).

## Contents

1. [Problem](#1-problem)
2. [Criteria](#2-criteria)
3. [Out of scope](#3-out-of-scope)
4. [Deliberation](#4-deliberation)
5. [Power budget](#5-power-budget)
6. [Proposed hardware](#6-proposed-hardware)
7. [Open tests](#7-open-tests)
8. [Decisions this spec asks for](#8-decisions-this-spec-asks-for)

---

## 1. Problem

The display spec puts one 5 V supply on each display backplate, but only names a size estimate (Mean Well LRS-50-5, 10 A) and leaves the model open until a bench test. That is too small for the production design:

- At full brightness, a display needs about 20 A at 5 V (see [5.1](#51-one-display)). 10 A only works with a hard brightness cap.
- Nothing covers the mains side: how 230 V gets from the wall to 8 displays, and what that line must carry.

The goal for production: the team installs the displays itself, can move a display to another position along the rail, and can swap any part by unplugging it. That means everything on the mains side is plug-in. No fixed installation, no change to the building wiring.

## 2. Criteria

| ID | Criterion | Requirement |
|---|---|---|
| PC1 | **Plug-in only.** Every device connects to mains with a plug. Nothing is wired into the building installation. | `DEC-001`, `HW-03` |
| PC2 | **Worst case covered.** Each supply carries a display at full white plus 30 % reserve, without a brightness cap. | `HW-02` |
| PC3 | **One socket.** The whole system runs from one Swiss 16 A socket with clear margin. | `DEC-007` |
| PC4 | **Survives a power cut.** After a mains outage, all displays start again by themselves, without tripping the breaker. | `REL-01`, `REL-07` |
| PC5 | **Legal and safe on Swiss mains.** Supplies meet the EU/Swiss rules for equipment on public mains (CE, EN 61000-3-2 harmonics above 75 W). Metal parts are earthed. | `HW-02` |
| PC6 | **Easy to maintain.** One display can be switched off, unplugged and swapped without touching the others. | `HW-03`, `HW-04` |
| PC7 | **Garage environment.** Parts on the rail tolerate dust and humidity, and work at garage temperatures. | `HW-02` |

## 3. Out of scope

- **The building installation.** Which socket, which circuit and which breaker are given by Facility Management. This spec only lists the questions to ask (see [8](#8-decisions-this-spec-asks-for)).
- **Enclosure and mounting.** Covered by the installation research ([PR #10](https://github.com/berufsbildung-basel/parkit-management/pull/10)). This spec only states what the enclosure must hold (supply size, inlet, earth).
- **Exact energy cost per year.** It depends on the real content, brightness and operating hours. [5.4](#54-brightness-as-a-lever) gives upper limits; the real value follows from PT2.
- **The bench setup.** The prototype runs on the Voltcraft lab supply (`DEC-008`), see the display spec.

## 4. Deliberation

### 4.1 Where the 5 V is made

The bays span about 20 m. One display needs about 20 A at 5 V. 20 A at 5 V cannot travel tens of metres without losing too much voltage, so 5 V must be made at each display. Mains (230 V) runs along the rail.

| Option | Plugs on the line | Result |
|---|---|---|
| **A. One enclosed 5 V supply per display, with IEC inlet and cord** | 8 | **Proposed.** One supply, one cord per display. Swap a display by unplugging it. |
| B. Two smaller supplies per display (5 V / 18 A each), each feeding 2 tiles | 16 | Half the display stays on if one supply fails, but twice the mains wiring and twice the switch-on current. |
| C. One central 24 V supply plus a 5 V converter at each display | 1 | About 35 A at 24 V along 20 m needs heavy cable. One failure turns off all 8 displays. Works against PC6. |
| D. Plug-in 5 V bricks (desktop adapters) | 32 | The largest 5 V Mean Well desktop adapter gives 6 A ([GST60A05](https://www.digikey.com/en/products/detail/mean-well-usa-inc/GST60A05-P1J/7703709)). 5 A per tile plus reserve does not fit. 4 bricks per display. Fails PC2 and PC6. |

### 4.2 Which supply

All three candidates are 5 V, about 40 A, closed metal case with screw terminals, convection cooled (no fan).

| | LRS-200-5 | **RSP-200-5** | HRP-200-5 |
|---|---|---|---|
| Rated current | 40 A | **40 A** | 35 A |
| Power factor correction | No | **Yes, PF > 0.95** | Yes, PF > 0.95 |
| EN 61000-3-2 (harmonics) | **No.** Datasheet note 10: not for end devices above 75 W input on 230 V mains | **Yes** | Yes |
| Input range | 115 or 230 V **by switch** | **85 to 264 V, no switch** | 85 to 264 V, no switch |
| Inrush current, cold start, 230 V | 60 A | **40 A** | 70 A |
| Leakage current | < 2 mA | **< 1 mA** | < 1.2 mA |
| Efficiency | 87 % | **85.5 %** | 84 % |
| Size | 215 x 115 x 30 mm | **215 x 115 x 30 mm** | 199 x 98 x 38 mm |
| Weight | 0.66 kg | **0.72 kg** | 0.77 kg |

Sources: Mean Well datasheets [LRS-200](https://www.meanwell.com/Upload/PDF/LRS-200/LRS-200-SPEC.PDF), [RSP-200](https://www.meanwell.com/Upload/PDF/RSP-200/RSP-200-spec.pdf), [HRP-200](https://www.meanwell.com/Upload/PDF/HRP-200/HRP-200-SPEC.PDF), read on 24 November 2026.

**Why RSP-200-5:** one display draws about 119 W from mains at full white, above the 75 W limit, so the LRS-200 fails PC5. The RSP-200-5 meets the harmonics rule, has the lowest switch-on current (helps PC4), has no voltage switch that can be set wrong, and keeps the flat 30 mm height. The HRP-200-5 is the fallback if the RSP is not available.

## 5. Power budget

Assumptions:

- **Tile:** 5 V x 5 A = 25 W at full white. This is the design assumption. The display spec quotes up to 4 A per tile from the listing, so 5 A adds margin. To be confirmed by PT1.
- **Controller:** Interstate 75 W about 0.3 A at 5 V (1.5 W) peak while Wi-Fi sends. Estimate, not measured.
- **Supply:** RSP-200-5, 85.5 % efficiency and power factor 0.95 (datasheet, typical at full load).
- **Mains:** 230 V nominal (Swiss standard, 230 V +/-10 %). Using 230 V instead of 240 V gives slightly higher currents, so the numbers err on the safe side.
- **Reserve:** 30 %, as in the display spec.

### 5.1 One display

| Part | Current at 5 V | Power |
|---|---|---|
| 4 x P5 tile at full white | 4 x 5 A = 20 A | 100 W |
| Interstate 75 W | 0.3 A | 1.5 W |
| **Total, 5 V side** | **20.3 A** | **101.5 W** |
| With 30 % reserve | 26.4 A | 132 W |
| RSP-200-5 rating | 40 A | 200 W |
| **Supply load** | **51 %** (66 % with reserve) | |
| **Mains side** (101.5 W / 0.855) | **0.54 A** at 230 V | **119 W** (125 VA) |

The 49 % headroom also covers the temperature derating of the supply in a closed enclosure (check against the derating curve in the datasheet, see PT4).

**5 V wiring inside the display.** Each of the two tile power harnesses carries 2 tiles = 10 A. Voltage loss on the wire from the supply to the tiles (out and back):

| Wire length, one way | 1.5 mm² | 2.5 mm² |
|---|---|---|
| 0.5 m | 0.12 V (2.5 %) | 0.08 V (1.5 %) |
| 1.0 m | 0.25 V (4.9 %) | 0.15 V (3.0 %) |

Rule: mount the supply in the middle of the backplate so each run stays at or below 0.5 m, or use 2.5 mm². The supply output can be adjusted from 4.5 to 5.5 V; set it so the farthest tile sees 5.0 V at full white (PT5).

### 5.2 All displays (overall budget)

| Load | 5 V side | Mains side |
|---|---|---|
| 8 displays | 162 A, 812 W | 950 W, 4.35 A |
| 4G Wi-Fi router (own adapter, estimate) | - | 10 W |
| Raspberry Pi 4 orchestrator, only if used (official 15 W adapter) | - | 15 W |
| **Total** | | **about 975 W, 4.6 A** |

The router and Pi adapters have no power factor correction, so their 25 W are counted as 0.22 A (power factor 0.5, estimate).

### 5.3 Mains line

| | Value | Note |
|---|---|---|
| Socket capacity | 16 A x 230 V = 3680 W | Swiss 16 A socket (type 23) |
| Steady load, worst case | 4.6 A, 975 W | **26 %** of the socket |
| Voltage loss on a 25 m feed, 3 x 1.5 mm² | 2.8 V (1.2 %) | No problem |
| Leakage current to earth | < 8 mA (8 x < 1 mA) | A 30 mA RCD (FI) trips between 15 and 30 mA. Below 10 mA (a third of 30 mA) is the usual safe limit |
| **Switch-on current** | **8 x 40 A = up to 320 A peak** | **The real limit, see below** |

**Switch-on current (inrush).** When a switching supply is plugged in, it charges its input capacitors and draws a short spike: 40 A for the RSP-200-5 (cold start, 230 V). The spike lasts well under 10 ms. One supply is no problem. Eight supplies that start in the same moment can trip the breaker:

- A type **B** 16 A breaker trips instantly at 3 to 5 x 16 A = 48 to 80 A.
- A type **C** 16 A breaker trips instantly at 5 to 10 x 16 A = 80 to 160 A.

Whether a short spike of up to 320 A trips it depends on the breaker and the spike length. This is a hypothesis, to be checked on site (PT3). It matters because after a power cut all 8 supplies start at the same time by themselves (PC4). Nobody is there to plug them in one by one.

If PT3 fails, in this order:

1. Ask Facility Management whether the circuit has a type C breaker or can get one.
2. Add an inrush current limiter for 16 A in front of the distribution box (product still to be found, ideally plug-in).
3. Split the displays over two sockets on different circuits (4 + 4).

### 5.4 Brightness as a lever

The tiles dim by switching the LEDs on and off very fast (PWM). The LED current, and with it the power, scales roughly with the brightness setting. A small part does not scale: the driver chips on each tile draw current even when all LEDs are off.

Model used here (estimates, to be confirmed by PT1 and PT2):

- Tile current = 0.2 A (driver chips, always on) + brightness x 4.8 A. At 100 % this gives the 5 A from [5](#5-power-budget).
- Controller stays at 0.3 A.
- Supply efficiency and power factor as at full load. At light load both get a little worse, so the real mains current is a bit higher than shown for 25 % and 50 %.
- Content is still full white. Real designs light only part of the pixels (black background), so real values are lower again. Full white is the case the hardware must survive.

**One display**

| Brightness | Current per tile | 5 V side | Supply load (RSP-200-5) | Mains side |
|---|---|---|---|---|
| 100 % | 5.0 A | 20.3 A, 101.5 W | 51 % | 119 W, 0.54 A |
| 75 % | 3.8 A | 15.5 A, 77.5 W | 39 % | 91 W, 0.41 A |
| 50 % | 2.6 A | 10.7 A, 53.5 W | 27 % | 63 W, 0.29 A |
| 25 % | 1.4 A | 5.9 A, 29.5 W | 15 % | 35 W, 0.16 A |

**All displays, with router and Pi (25 W)**

| Brightness | 5 V side, 8 displays | Mains total | Mains current | Share of a 16 A socket | Energy per year at 24/7, full white |
|---|---|---|---|---|---|
| 100 % | 812 W | 975 W | 4.6 A | 26 % | about 8,500 kWh |
| 75 % | 620 W | 750 W | 3.5 A | 20 % | about 6,600 kWh |
| 50 % | 428 W | 526 W | 2.5 A | 14 % | about 4,600 kWh |
| 25 % | 236 W | 301 W | 1.5 A | 8 % | about 2,600 kWh |

The energy column is an upper limit: all pixels white, all day, every day. Real content, and switching the displays dark at night or on weekends, both bring it down a lot. PT2 gives the real number for the designs.

What brightness changes, and what it does not:

- **It lowers consumption, heat and energy cost** about in proportion. 50 % brightness roughly halves all of them. In a dark garage, 25 to 50 % is probably bright enough and also avoids glare (display spec C6). The right level is found on site together with readability test T5.
- **It does not allow a smaller supply.** The brightness is set in the firmware. A firmware bug, a test pattern or a reset to default can drive the tiles at 100 %. The supply must survive that, so it stays sized for full white (PC2).
- **It does not change the switch-on current.** The 40 A spike comes from the supply's input capacitors, not from the LEDs. PT3 is needed at any brightness.

## 6. Proposed hardware

### 6.1 Line from the wall to the displays

The line is a star, not a chain: one distribution box, one cord per display.

```
Wall socket 16 A (type 23)
   |
   | feed cord, 16 A, 3 x 1.5 mm², type 23 plug
   |
Distribution box on the rail, IP44, 16 A, 10+ sockets
   |-- cord --> Display 1   (IEC C13 into the display's fused inlet)
   |-- cord --> Display 2
   |   ...
   |-- cord --> Display 8
   |-- 4G router adapter
   |-- Pi adapter (only if the orchestrator is used)
   '-- spare
```

- **Star, not chain.** Never plug a power strip into another power strip. A star keeps one contact point per display and makes each display independent (PC6).
- **Rated for 16 A.** The socket is fused at 16 A, so the feed cord and the distribution box must also be rated 16 A (type 23, 3 x 1.5 mm²), even though the load is only 4.6 A. A 10 A strip on a 16 A circuit is not protected against overload.
- **IP44 or better** for everything on the rail (PC7). The garage has dust, humidity and exhaust (see the installation research).
- **Cords fixed along the rail** with clips, with strain relief at both ends. No loops hanging into the vehicle clearance.

### 6.2 Inside each display

```
IEC C14 inlet with fuse and switch
   L, N  -->  RSP-200-5 input (L, N)
   PE    -->  RSP-200-5 FG  and  metal backplate (earth)
RSP-200-5 output
   +V/-V pair 1 --> fuse 15 A --> harness 1 --> tiles 1 + 2
   +V/-V pair 2 --> fuse 15 A --> harness 2 --> tiles 3 + 4
   +V/-V        --> Interstate 75 W (5 V input, check the pin-out)
```

- **Fused, switched IEC inlet.** The switch lets one display be turned off at the display. The fuse protects the mains wiring inside. Fuse T 3.15 A (slow) is our proposal: it carries 0.54 A steady and the 40 A switch-on spike. Check against the fuse's I²t data.
- **Earth.** The supply is class I. Its FG terminal and the metal backplate are connected to PE. A silicone or plastic layer alone does not replace the earth.
- **Terminal cover.** The supply has open screw terminals. The enclosure, or a separate cover, must make them impossible to touch when the display is open for service while plugged in. Better: always unplug before opening.
- **A 15 A fuse per tile harness.** The supply only limits its output above 40 A. A short circuit in one harness with 1.5 mm² wire could overheat the wire before the supply reacts. A blade fuse (car type) per harness stops that.
- **Mains wiring inside the display** (inlet to supply) is done or checked by a qualified person, as the display spec already requires. After that, the team only plugs and unplugs.

### 6.3 Shopping list, production (8 displays)

| Qty | Item | Example | Price (CHF, estimate) | Note |
|---|---|---|---|---|
| 9 | 5 V supply, 40 A, with PFC | Mean Well RSP-200-5 | about 74 each ([digitec.ch](https://www.digitec.ch/de/s1/product/meanwell-acdcnetzteilbaustein-geschlossen-spannungswandler-8490044), seen 24.11.2026, not checked in the cart) | 8 + 1 spare. Replaces the LRS-50-5 in the display spec |
| 9 | IEC C14 panel inlet with fuse holder and switch | e.g. Schurter or equal | to be checked | 8 + 1 spare |
| 20 | Fuse 5 x 20 mm, T 3.15 A | | to be checked | Spares included |
| 9 | Mains cord IEC C13 to Swiss plug type 12, 3 x 1.0 mm² | length per bay, 2 to 10 m | to be checked | Length follows the position of the distribution box |
| 1 | Distribution box, IP44, 16 A, at least 10 sockets type 13/23, with feed cord type 23 | | to be checked | Or one IP44 box plus a separate 16 A feed cord |
| 18 | Inline blade fuse holder + 15 A blade fuse | car type | to be checked | 2 per display + 2 spare |
| 10 m | Wire 2.5 mm², red and black | | to be checked | Supply to harness, only if runs are longer than 0.5 m |
| 8 | Earth wire green/yellow 1.5 mm² with ring terminal | | to be checked | Backplate to PE |
| 0-1 | Inrush current limiter, 16 A, plug-in | | to be checked | Only if PT3 fails |

Not in this list because they come with their device: router adapter, Pi adapter, tile harnesses.

## 7. Open tests

Nothing below is proven. PT1 and PT2 can start with the prototype tiles that are already in the office.

| ID | Test | Passes when | Hardware needed |
|---|---|---|---|
| PT1 | Current of 2 tiles at full white on the lab supply (10 A limit, so 2 tiles, not 4). Double the result | Measured current per tile is 5 A or less. If more, recalculate [5](#5-power-budget) | Prototype tiles, Voltcraft (`DEC-008`) |
| PT2 | One complete display on an RSP-200-5: mains power with a plug-in power meter, at full white and at 75, 50 and 25 % brightness, plus with the real designs | Full white below 125 W. The measured values replace the model in [5.4](#54-brightness-as-a-lever) | Prototype display, 1 RSP-200-5, power meter |
| PT3 | Switch-on on site: all 8 supplies (or the real installation) switched on together 10 times with the distribution box switch or the breaker | The breaker never trips. If it does, apply the steps in [5.3](#53-mains-line) | 8 supplies, site socket |
| PT4 | Heat: display closed, 2 hours at full white | Supply case temperature within the derating curve, no tile or controller resets | Prototype display in its enclosure |
| PT5 | Voltage at the farthest tile at full white | 4.9 V or more at the tile input | Prototype display, multimeter |
| PT6 | Leakage: 30 mA RCD on the line with all supplies running | RCD does not trip; measured leakage below 10 mA | 8 supplies, RCD, electrician |

## 8. Decisions this spec asks for

1. Accept the plug-in design: one RSP-200-5 per display, one 16 A distribution box, one socket (Option A in [4.1](#41-where-the-5-v-is-made)).
2. Accept 5 A per tile at full white, without a brightness cap, as the design case for the hardware. Brightness is the lever for consumption, heat and glare ([5.4](#54-brightness-as-a-lever)), not for sizing the supply.
3. Set the operating brightness on site, together with readability test T5, and decide whether the displays go dark outside office hours.
4. Ask Facility Management (`DEC-001`):
   - Which 16 A socket can be used, and where is it relative to the rail?
   - Breaker type (B or C) and whether the circuit has a 30 mA RCD.
   - What else is on that circuit?
5. Who builds or checks the mains part of each display (inlet to supply)?
6. Update the display spec: replace the LRS-50-5 with the RSP-200-5 in the parts list (done in this PR).
7. Record the result in [decisions.md](../../../../project-notes/decisions.md) and close the power entry in [open-questions.md](../../../../project-notes/open-questions.md).

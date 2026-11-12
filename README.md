[README_bop_test15.md](https://github.com/user-attachments/files/34766851/README_bop_test15.md)
# BOP Pressure Test Simulator — README

**S. Siddhu | SOGE | Central**
File: `bop_test15.html` · Version: v15 (Phase 1 — physics core) · Updated: 2026-11-12

## Purpose
Single-file HTML/Canvas training simulator for BOP pressure testing. It models the BOP stack, kill and choke lines, choke manifold, standpipe / kelly and wellbore. Each isolated section holds its own pressure, so trainees can follow the test sequences in the M-07 BOPE testing slides (Pump 1.0 – Pump 7).

## How to run
1. Open `bop_test15.html` in any current browser (Chrome or Edge recommended). No install or internet needed.
2. Set **Test Pressure (PSI)** before starting. It is locked while a test is running.
3. Use **Reset / Vent** to bleed every section to zero and open all BOPs.

## Controls
| Control | What it does |
|---|---|
| Pressure Source toggles | Test unit on the kill line (below or above the check valve), test unit on the choke manifold, rig mud pump |
| Wellbore Config | Drill pipe in hole, test plug set |
| Test buttons | Close the annular, pipe rams, blind rams (CSO) or pipe/shear rams and start the test unit |
| Click a BOP body | Open / close that element |
| Click a valve | Open / close it. Green body + raised stem = open; red = closed |
| Click the mud pump | Start / stop the pump (enable "Rig Mud Pump Active" first) |
| Click a test unit | Start / reset the test |
| Check valve | Left-click = install / remove; right-click = flip direction |

## Valves and components
- **Stack (top → bottom):** annular (bag), pipe rams, blind rams (CSO), drilling spool, pipe/shear rams, casinghead, test plug.
- **Kill side:** Kill Control (1), Kill Master (2), check valve, Kill Access (auxiliary pump connect).
- **Choke side:** Choke Mstr (10), Choke Ctrl (9), three-row choke manifold (Iso / Chk / Iso) to the buffer chamber and pits.
- **Drill string:** standpipe valve, rotary hose, swivel, UKV, LKV, kelly.
- **Pump side:** mud pump, Pump Bleeder, Pump Disch. V.

## Gauges and console
| Reading | Shows |
|---|---|
| Standpipe (DP) gauge | Pressure above the standpipe valve (drill pipe / kelly / hose side) |
| BOP Cavity | Drilling spool pressure |
| Choke Manifold | Pressure downstream of Choke Ctrl (9) |
| Mud Pump | Pump line pressure (0 once the bleeder is opened) |
| Test unit LCD | Pressure at the test unit hook-up |
| Chart recorder | Cavity, choke and standpipe trends |
| Lamps | PRESS, HOLD, LEAK, PUMP |

## How the physics works
- Every section between valves or BOP elements is a separate **zone** with its own pressure.
- **Open valve or element** → the zones on each side join and share one pressure.
- **Source pumping, no vent** → pressure builds to the test pressure, then holds (HOLDING).
- **Open path to atmosphere** (flow line, open manifold outlet, Kill Access, pump bleeder, no test plug) → that zone bleeds off. If a running source is connected to it, the test shows LEAK.
- **Source stopped or bled** → pressure stays trapped behind closed elements.
- **Drill pipe** is open at the bottom, above the plug, so it fills from the wellbore whatever the rams are doing. Valves are tested in the direction of a kick.
- **Check valve** is one-way. Installed DOWN, it holds wellbore pressure from below once the pump side is bled.
- **Pipe rams** seal only around pipe. An open casinghead outlet is not counted as a leak for now.

## Verified against the M-07 slides (Phase 1)
Pump 1.0 (shell test) through Pump 3 were run as scripted scenarios on the default manifold. Standpipe, choke, mud pump and cavity readings match the slides at every step. Pump 1.1 and 1.2 are approximated until the M-07 manifold arrives in Phase 2.

## Known limitations
- **M-07 manifold:** numbering and valve sequence are not built yet (Phase 2).
- **Drill string set-ups:** PSV / dart valve, the no-pipe configuration, the tester truck at the casinghead outlet and the plug-below-outlet option are not built yet (Phase 3).
- **Component faults:** the simulator does not yet simulate a failing component, such as a leaking LKV. A planned option for the guided mode (Phase 4).
- **Standpipe gauge:** keeps the v13 latch-and-hold behaviour.
- **Joining zones:** when a pressured zone joins an empty closed one, the higher pressure is kept.

## Roadmap
1. ~~Phase 1 — physics core~~ (built; under review against Pump 1–3)
2. Phase 2 — **M-07** toggle: slide manifold, valve numbers 1–8, M-07 names and valve sequence
3. Phase 3 — kelly / PSV + dart valve / no-pipe set-ups, Pump 6–7, tester truck, blind-ram-on-pipe warning
4. Phase 4 — guided step-through of Pump 1–7

## Version history
| Version | Change |
|---|---|
| v13 | Stable baseline: gauge latch, check valve, kill / choke flow |
| v14 | Visual overhaul: rig substructure scene, realistic stack, valves and manifold; physics unchanged |
| v15 | Phase 1 physics core: zone-pressure model, M-07 stack order, drill pipe fills from bottom, trapped pressure, separate gauges, pump bleeder, CSO = blind rams, Kill Control (1) |

Related project doc: `claude/test_crosswalk.md` (slide-by-slide crosswalk, decisions, change list).

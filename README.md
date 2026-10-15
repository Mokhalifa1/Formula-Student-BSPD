# Formula-Student-BSPD
Fail-safe analogue BSPD design for Formula Student (T 11.6 compliant)

## The Problem
In Formula Student, a driver can accidentally apply brake and throttle at the same time. A BSPD must detect this "implausibility" and cut the shutdown circuit (SDC) to prevent a DNF or crash.

## Design Highlights
* **No Code:** Pure analog logic (LM339 comparators + 74HC series gates).
* **Timing:** 300ms RC timer (safely below the 500ms rule limit) to ignore heel-and-toe blips.
* **Fail-Safe Latch:** SR latch (74HC02) requires a full LVMS power cycle to reset.
* **Sensor Fault Detection:** Window comparators detect shorts to GND or 5V, and broken wires (via pull-ups).

## System Architecture
The design follows a clear signal flow:
1. **Power:** 12V from LVMS -> Fuse/TVS -> 5V Regulator (LM2937ES).
2. **Decision:** Comparators check Brake (>25 bar) and Throttle (>25%).
3. **Logic:** AND gate combines conditions; OR gates combine sensor faults.
4. **Memory:** Latch holds the trip.
5. **Output:** MOSFET driver opens the SDC relay (Omron G5Q).

## Files
* `BSPD_Design_Report.pdf` – Full schematic, component justification, and PCB layout.

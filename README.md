# DrainSakhi — Smart Drainage Blockage and Overflow Warning System

## Project status
This repository contains a **starter implementation and proposed design** for an educational tabletop prototype. It has not been field-validated. Do not claim that it reliably detects real drain blockages until it is built, calibrated, and tested.

## Problem
Blocked or overflowing drains can contribute to waterlogging and unhygienic surroundings. DrainSakhi explores whether water-level monitoring at two points can flag unusual patterns for human inspection.

## Proposed solution
Two ultrasonic sensors measure distance to the water surface. An ESP32 compares the readings and activates an LED and buzzer when a configured abnormal pattern persists.

A difference in readings is only a possible warning sign, not proof of blockage.

## Components
- ESP32 development board
- 2 ultrasonic sensors (e.g., HC-SR04 for a tabletop model)
- LED and suitable current-limiting resistor (for a bare LED)
- Active buzzer/module compatible with the selected GPIO and voltage
- Breadboard, jumper wires, and voltage dividers/level shifters

## Wiring used by `drainsakhi.ino`
| Component | ESP32 GPIO |
|---|---:|
| Upstream TRIG | 5 |
| Upstream ECHO (through level shifting) | 18 |
| Downstream TRIG | 17 |
| Downstream ECHO (through level shifting) | 16 |
| LED | 2 |
| Active buzzer input | 23 |

## Safety
**HC-SR04 ECHO commonly outputs 5 V; ESP32 GPIO is not 5 V tolerant. Never connect ECHO directly to an ESP32 GPIO.** Use an appropriate voltage divider or level shifter on both ECHO lines. Keep electronics dry and test only with a small controlled model. Do not deploy this unvalidated design in a public drain.

## Software setup
1. Install Arduino IDE.
2. Install ESP32 board support using the official Espressif/Arduino instructions.
3. Open `drainsakhi.ino`.
4. Verify wiring and select the correct ESP32 board and port.
5. Compile and upload; open Serial Monitor at 115200 baud.
6. Record baseline readings and calibrate thresholds for your model.

## Decision logic
1. Read both sensor distances.
2. Ignore invalid/no-echo readings.
3. Check for high-water distance or an unusually large distance difference.
4. Require the condition to persist for three samples before activating the LED and buzzer.

Thresholds are example values and must be calibrated.

## Test plan
See `tests/test-cases.md`. Mark tests as passed only after performing them and recording observations.

## Contents
- `drainsakhi.ino` — ESP32 starter code
- `docs/technical-design.md` — architecture and limitations
- `tests/test-cases.md` — test plan and blank results log

## License
No license is included. Add one if you decide how others may reuse the code.

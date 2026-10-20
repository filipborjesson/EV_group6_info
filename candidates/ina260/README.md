# Adafruit INA260 (Current, Voltage, and Power Monitor)

Status: Candidate — not finalized.

Assigned member: Royal A.

This directory contains research and development material for the Adafruit INA260 current, voltage, and power monitor.

- Datasheets and manuals: `documents/`
- Connection diagrams: `wiring/`
- Code: `firmware/`
- Test procedures and results: `tests/`

Documentation inclues power requirements, interfaces, proposed pins, and compatibility concerns.

## Proposed MCU

Current documentation assumes the ESP32-DevKitC V4 as the proposed MCU.

- [ESP32-DevKitC V4 User Guide](https://docs.espressif.com/projects/esp-dev-kits/en/latest/esp32/esp32-devkitc/user_guide.html)
- [ESP32-DevKitC V4 Schematic](https://dl.espressif.com/dl/schematics/esp32_devkitc_v4_sch.pdf)

Final wiring and compatibility should be verified against the hardware selected for the vehicle.
# Proposed wiring, pin assignments, and diagrams

### Connection Diagram (XIAO ESP32S3 Sense ↔ ESP32-DevKitC)

```
   XIAO ESP32S3 Sense                    ESP32-DevKitC V4
  +-------------------+                +-------------------+
  |                   |                |                   |
  |  D6 (GPIO43, TX) -+----- Blue ---->+- GPIO16 (RX2)     |
  |  D7 (GPIO44, RX) -+<---- Yellow ---+- GPIO17 (TX2)     |
  |  GND             -+----- Black ----+- GND              |
  |                   |                |                   |
  |  USB-C (5 V in)   |                |  USB (5 V in)     |
  +-------------------+                +-------------------+
          ^
          |
   5 V supply or 3.7 V LiPo (BAT pads)
```

### Pin Assignments

| XIAO Pin | GPIO | Assigned To | Notes |
|---|---|---|---|
| D6 | GPIO43 | UART TX → DevKitC RX2 (GPIO16) | Status / detection messages |
| D7 | GPIO44 | UART RX ← DevKitC TX2 (GPIO17) | Commands from main controller |
| GND | — | DevKitC GND | Common ground required for UART |
| D0–D5 | GPIO1–6 | Unassigned | Available for future use |
| D8–D10 | GPIO7–9 | microSD (onboard) | Shared SPI bus, do not reassign |

### Reserved Pins (Sense board)

* GPIO10–18, 38–40, 47–48: camera
* GPIO41–42: microphone
* GPIO21: microSD chip select / user LED

### Power Wiring

| Option | Connection | Notes |
|---|---|---|
| Bench testing | USB-C to laptop or power bank | Simplest option |
| On the vehicle | 3.7 V LiPo on BAT+ / BAT− pads | Recharges over USB-C |
| External 5 V | 5V pin with a series diode | Diode protects the USB port (per Seeed) |

### Wiring Notes

* TX on one board always connects to RX on the other.
* Both boards are 3.3 V logic, so no level shifter is needed.
* The ground wire is required even if the boards have separate power supplies.
* Keep the UART wires short and away from motor wires to reduce noise.
* DevKitC pins GPIO16/17 are proposed; confirm with the team that no other component is using them.

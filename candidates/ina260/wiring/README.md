# Proposed wiring, pin assignments, and diagrams

## Reference Diagrams

- [Adafruit INA260 Pinout Guide](https://learn.adafruit.com/adafruit-ina260-current-voltage-power-sensor-breakout/pinouts)
- [Adafruit INA260 Schematic and Design Files](https://learn.adafruit.com/adafruit-ina260-current-voltage-power-sensor-breakout/downloads)

## Proposed Connections

| INA260 Pin | ESP32-DevKitC | Function |
|---|---|---|
| VIN | 3V3 | Sensor power |
| GND | GND | Common ground |
| SDA | GPIO21 | I2C data |
| SCL | GPIO22 | I2C clock |
| ALERT | TBD | Optional interrupt/alert |
| VIN+ | Power source | High-current input |
| VIN- | Load | High-current output |


             ESP32-DevKitC
            ┌──────────────┐
       3V3 ─┤              ├──── GPIO21 (SDA)
       GND ─┤              ├──── GPIO22 (SCL)
            └──────────────┘
                │   │
                │   │
                ▼   ▼
             ┌────────┐
      3V3 ───┤ VIN    │
      GND ───┤ GND    │
GPIO21 ──────┤ SDA    │
GPIO22 ──────┤ SCL    │
             │ INA260 │
             └────────┘
             VIN+  VIN-
               │    │
               │    └────────► Load
               │
               ▼
          Power Supply (+)
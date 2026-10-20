# Datasheets, Manuals, Schematics, and Source Links

## Technical Resources

### INA260

- [Texas Instruments INA260 Datasheet](https://www.ti.com/lit/ds/symlink/ina260.pdf)
- [Adafruit INA260 Product Guide](https://cdn-learn.adafruit.com/downloads/pdf/adafruit-ina260-current-voltage-power-sensor-breakout.pdf)
- [Adafruit INA260 Design Resources and Schematic](https://learn.adafruit.com/adafruit-ina260-current-voltage-power-sensor-breakout/downloads)
- [Adafruit INA260 Arduino Guide](https://learn.adafruit.com/adafruit-ina260-current-voltage-power-sensor-breakout/arduino)

### ESP32-DevKitC V4

- [ESP32-DevKitC V4 User Guide](https://docs.espressif.com/projects/esp-dev-kits/en/latest/esp32/esp32-devkitc/user_guide.html)
- [ESP32-DevKitC V4 Schematic](https://dl.espressif.com/dl/schematics/esp32_devkitc_v4_sch.pdf)


## Purpose

The Adafruit INA260 is being evaluated for monitoring current, bus voltage, and power in the Smart EV.


## Proposed Controller

Current documentation assumes the ESP32-DevKitC V4 as the proposed controller.

The INA260 uses I2C for communication. The proposed connections are:

- SDA: GPIO21
- SCL: GPIO22
- Sensor Power: 3.3 V
- Ground: GND


## INA260 Key Specifications

- Bus voltage measurement: 0-36 V
- Continuous current: up to 15 A from -40 C to +85 C
- Supply voltage: 2.7-5.5 V
- Interface: I2C / SMBus
- Resolution: 16-bit
- Integrated shunt: 2 mOhm
- High-side or low-side sensing
- Bidirectional current measurement
- Configurable averaging
- Programmable alert output
- 16 programmable I2C addresses


## Proposed Application

The INA260 will be evaluated for monitoring:

- Bus voltage
- Current consumption
- Power consumption
- Load changes during vehicle operation


## Compatibility

### ESP32-DevKitC

The INA260 supports a 3.3 V supply and I2C communication, making it suitable for evaluation with the ESP32-DevKitC.

Proposed interface:

- GPIO21 -> SDA
- GPIO22 -> SCL
- 3V3 -> INA260 VIN
- GND -> INA260 GND


### Vehicle Electrical System

Final vehicle compatibility depends on:

- Maximum battery voltage
- Continuous load current
- Startup current
- Motor stall current
- INA260 location within the power system

These values must be compared against the INA260 electrical limits before vehicle integration.
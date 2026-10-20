# INA260 Documentation

## Purpose

The Adafruit INA260 is being evaluated for monitoring current,
bus voltage, and power in the Smart EV.

## Selected Controller

The proposed controller is the ESP32-DevKitC.

The INA260 communicates using I2C. The proposed ESP32 I2C
connections are:

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

The INA260 will monitor electrical behavior within the Smart EV,
including:

- Bus voltage
- Current consumption
- Power consumption
- Load changes during vehicle operation

## Compatibility

### ESP32-DevKitC

The INA260 and ESP32-DevKitC are compatible candidates for an
I2C-based interface.

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
- Location of the INA260 within the power system

These values should be compared against the INA260 electrical
limits before vehicle integration.

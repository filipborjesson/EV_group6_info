# Proposed Firmware Implementation and Setup instructions

## Controller

ESP32-DevKitC

## Interface

I2C

- SDA: GPIO21
- SCL: GPIO22

## Initial Firmware Objectives

1. Initialize ESP32 I2C.
2. Detect the INA260.
3. Initialize the INA260 library.
4. Read current.
5. Read bus voltage.
6. Read power.
7. Output measurements through Serial.

## Library

Adafruit INA260 Library

## Future Features

- Measurement averaging
- Configurable sampling/update rate
- Overcurrent alerts
- Continuous data logging

## Firmware Resources

- Adafruit INA260 Arduino Library:
  https://github.com/adafruit/Adafruit_INA260

- Adafruit INA260 Arduino Guide:
  https://learn.adafruit.com/adafruit-ina260-current-voltage-power-sensor-breakout/arduino

- Adafruit INA260 Library Documentation:
  https://adafruit.github.io/Adafruit_INA260/html/class_adafruit___i_n_a260.html
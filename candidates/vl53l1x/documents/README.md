# Datasheets, manuals, schematics, and source links
## Datasheets, Manuals, Schematics, and Source Links

### Technical Resources

**VL53L1X**

* [STMicroelectronics VL53L1X Datasheet](https://www.st.com/resource/en/datasheet/vl53l1x.pdf)
* [Adafruit VL53L1X Product Guide](https://cdn-learn.adafruit.com/downloads/pdf/adafruit-vl53l1x.pdf)
* [Adafruit VL53L1X Design Resources and Schematic](https://learn.adafruit.com/adafruit-vl53l1x/downloads)
* [Adafruit VL53L1X Pinouts](https://learn.adafruit.com/adafruit-vl53l1x/pinouts)
* [Adafruit VL53L1X Arduino Guide](https://learn.adafruit.com/adafruit-vl53l1x/arduino)

**ESP32-DevKitC V4**

* [ESP32-DevKitC V4 User Guide](https://docs.espressif.com/projects/esp-dev-kits/en/latest/esp32/esp32-devkitc/user_guide.html)
* [ESP32-DevKitC V4 Schematic](https://dl.espressif.com/dl/schematics/esp32_devkitc_v4_sch.pdf)

### Purpose

The Adafruit VL53L1X is being evaluated for distance and obstacle detection in the Smart EV.

### Proposed Controller

Current documentation assumes the ESP32-DevKitC V4 as the proposed controller.

The VL53L1X uses I2C for communication. The proposed connections are:

* SDA: GPIO21
* SCL: GPIO22
* Sensor Power: 3.3 V
* Ground: GND

### VL53L1X Key Specifications

* Measurement range: ~30-4000 mm
* Update rate: up to 50 Hz
* Emitter: 940 nm invisible laser (Class 1, eye-safe)
* Field of view: 27° typical
* Programmable region of interest (ROI) to narrow the field of view
* Interface: I2C (up to 400 kHz)
* Default I2C address: 0x29
* Supply voltage: 3-5 V (on-board 2.8 V regulator and level shifting)
* Shutdown (XSHUT) and interrupt (GPIO) pins
* Two STEMMA QT / Qwiic connectors
* Absolute distance measurement independent of target color and reflectance

### Proposed Application

The VL53L1X will be evaluated for monitoring:

* Forward obstacle distance
* Proximity detection for collision avoidance
* Distance changes during vehicle operation

### Compatibility

#### ESP32-DevKitC

The VL53L1X supports a 3.3 V supply and I2C communication, making it suitable for evaluation with the ESP32-DevKitC.

Proposed interface:

* GPIO21 -> SDA
* GPIO22 -> SCL
* 3V3 -> VL53L1X VIN
* GND -> VL53L1X GND
* XSHUT and GPIO (interrupt): optional, not connected for initial evaluation

#### Shared I2C Bus with INA260

The VL53L1X (0x29) and INA260 (default 0x40) use different I2C addresses and can share GPIO21/GPIO22 without conflict.

### Vehicle Integration

Final vehicle compatibility depends on:

* Required detection range and update rate
* Mounting height and angle relative to the road surface
* Ambient light conditions (sunlight reduces maximum range)
* Target surface types expected in the vehicle environment
* Protective cover window material in front of the sensor
* Vibration and wiring length to the controller

These values must be compared against the VL53L1X performance limits before vehicle integration.

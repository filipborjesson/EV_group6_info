# Adafruit VL53L1X (Time-of-Flight Distance Sensor)

Status: Candidate — not finalized.

Assigned member: TBD

Add datasheets and manuals to `documents/`, connection diagrams to `wiring/`, code to `firmware/`, and test procedures and results to `tests/`. Document power requirements, interfaces, proposed pins, and compatibility concerns.

VL53L1CX specifications:

Emitter: 940 nm invisible laser (Class1)
SPAD (single photon avalanche diode) receiving array with integrated lens
FlightSense™ ranging sensor for fast and accurate long distance ranging
Up to 400 cm distance measurement
Up to 50 Hz ranging frequency
Typical full field-of-view (FoV): 27 °
Programmable region-of-interest (ROI) size on the receiving array, allowing the sensor FoV to be reduced
Programmable ROI position on the receiving array, providing multizone operation control from the host
Can be hidden behind many cover window materials
I²C interface (up to 400 kHz)
Shutdown and interrupt pins
Default I2C address 0x29 (can be changed in software by using shutdown pin to disable other sensors on the same bus)
Product Dimensions: 25.5mm x 17.5mm x 4.6mm / 1.0" x 0.7" x 0.2"

Product Weight: 1.8g / 0.1oz

### Wiring

#### VL53L1X Breakout Pinout

| VL53L1X Pin | Function |
|---|---|
| VIN | Power input (3-5 V) |
| GND | Ground |
| SCL | I2C clock |
| SDA | I2C data |
| GPIO | Interrupt output (data ready), optional |
| XSHUT | Shutdown input (pull LOW to turn sensor off), optional |

#### Option A: Header Pins / Jumper Wires

| ESP32-DevKitC Pin | VL53L1X Pin | Wire Color (suggested) |
|---|---|---|
| 3V3 | VIN | Red |
| GND | GND | Black |
| GPIO21 | SDA | Blue |
| GPIO22 | SCL | Yellow |
| GPIO18 (optional) | XSHUT | Green |
| GPIO19 (optional) | GPIO (interrupt) | White |

#### Option B: STEMMA QT / Qwiic Cable

Use a STEMMA QT to male header cable (JST SH 4-pin):

| Cable Wire | ESP32-DevKitC Pin | Signal |
|---|---|---|
| Red | 3V3 | Power |
| Black | GND | Ground |
| Blue | GPIO21 | SDA |
| Yellow | GPIO22 | SCL |

#### Wiring Diagram

```
ESP32-DevKitC V4              Adafruit VL53L1X
+----------------+            +----------------+
|           3V3  |------------| VIN            |
|           GND  |------------| GND            |
|        GPIO21  |------------| SDA            |
|        GPIO22  |------------| SCL            |
|        GPIO18  |- - - - - - | XSHUT  (opt.)  |
|        GPIO19  |- - - - - - | GPIO   (opt.)  |
+----------------+            +----------------+
```

#### Shared I2C Bus with INA260

Both sensors connect in parallel on the same I2C lines:

| ESP32 Pin | VL53L1X | INA260 |
|---|---|---|
| 3V3 | VIN | VCC |
| GND | GND | GND |
| GPIO21 | SDA | SDA |
| GPIO22 | SCL | SCL |

```
              3V3 ----+-------------+
              GND ----+-------------+
ESP32      GPIO21 ----+-- VL53L1X --+-- INA260
           GPIO22 ----+   (0x29)    +   (0x40)
```

The VL53L1X can also be daisy-chained to the INA260 using the second STEMMA QT connector on each board.

#### Wiring Notes

* Connect all grounds together (ESP32, sensor, and any external supply).
* The Adafruit breakout includes on-board I2C pull-up resistors; no external resistors are needed.
* Keep I2C wires short (under ~30 cm) for reliable communication; use shielded or twisted wiring for longer runs in the vehicle.
* XSHUT and GPIO are only required for multiple VL53L1X sensors (address reassignment) or interrupt-driven reading.
* Remove the protective tape from the sensor window before use.
* Do not power the sensor from the vehicle battery directly; use the ESP32 3V3 pin or a regulated 3.3-5 V supply.

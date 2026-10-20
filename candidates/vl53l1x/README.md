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

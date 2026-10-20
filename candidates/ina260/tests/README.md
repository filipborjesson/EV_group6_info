# Test Procedures, Observations, and Results

## Test 1 - ESP32 I2C Communication

**Objective:**  
Verify communication between the ESP32-DevKitC and INA260.

**Connections:**
- GPIO21 -> SDA
- GPIO22 -> SCL
- 3V3 -> VIN
- GND -> GND

**Procedure:**  
Run an I2C scan or INA260 initialization program from the ESP32.

**Pass Criteria:**
- INA260 is detected on the I2C bus
- INA260 initialization succeeds


## Test 2 - Voltage Measurement

**Objective:**  
Verify INA260 bus voltage measurements.

**Procedure:**  
Apply a known DC voltage and compare the INA260 reading against a trusted multimeter.

**Pass Criteria:**
- INA260 reports a stable voltage
- Reading is reasonably consistent with the reference measurement


## Test 3 - Current Measurement

**Objective:**  
Verify INA260 current measurements.

**Procedure:**  
Connect a controlled DC load through the INA260 and compare its reading against a reference measurement.

**Pass Criteria:**
- INA260 detects current through the load
- Reading is reasonably consistent with the reference measurement


## Test 4 - Power Measurement

**Objective:**  
Verify INA260 power measurements.

**Procedure:**  
Operate a known DC load and record voltage, current, and reported power.

**Pass Criteria:**
- INA260 produces a stable power reading
- Reported power is reasonably consistent with voltage and current measurements


## Test 5 - Continuous Logging

**Objective:**  
Verify reliable measurement over time.

**Procedure:**  
Continuously record voltage, current, and power during a controlled test.

**Pass Criteria:**
- Measurements are recorded continuously
- No unexpected communication failures occur
- Changes in load are reflected in the recorded data


## Test 6 - Smart EV Compatibility

**Objective:**  
Verify that the INA260 can safely operate within the Smart EV electrical system.

**Procedure:**  
Compare the finalized vehicle voltage and current requirements against the INA260 datasheet specifications.

**Pass Criteria:**
- Maximum bus voltage remains within the sensor measurement limit
- Expected current remains within the supported operating range
- ESP32 communication and power requirements remain compatible

**Status:** Pending final vehicle electrical specifications.
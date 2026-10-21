# Test procedures, observations, and results
### Test Procedures, Observations, and Results

#### Test Equipment

* ESP32-DevKitC V4
* Adafruit VL53L1X breakout
* USB cable and computer running Arduino IDE (Serial Monitor at 115200 baud)
* Tape measure or ruler (mm resolution)
* Flat test targets: white card, black card, cardboard, metal surface
* Optional: INA260 breakout (shared I2C bus test)

#### Test 1: Power and I2C Detection

**Procedure**
1. Wire the sensor to the ESP32 (3V3, GND, GPIO21 SDA, GPIO22 SCL).
2. Upload the I2C scanner sketch.
3. Record the detected addresses.

**Expected:** Device found at 0x29.

| Item | Expected | Observed | Pass/Fail |
|---|---|---|---|
| Sensor power LED | On | | |
| I2C address detected | 0x29 | | |

#### Test 2: Distance Accuracy

**Procedure**
1. Upload the basic distance sketch (timing budget 50 ms).
2. Mount the sensor facing a flat white target, perpendicular to the beam.
3. Place the target at each distance below, measured from the sensor face.
4. Record 10 readings at each distance and average them.

**Error % = |Average − Actual| / Actual × 100**

| Actual Distance (mm) | Average Reading (mm) | Min (mm) | Max (mm) | Error (%) | Pass/Fail |
|---|---|---|---|---|---|
| 50 | | | | | |
| 100 | | | | | |
| 250 | | | | | |
| 500 | | | | | |
| 1000 | | | | | |
| 2000 | | | | | |
| 3000 | | | | | |
| 4000 | | | | | |

#### Test 3: Minimum Range

**Procedure**
1. Move the target slowly toward the sensor, starting at 100 mm.
2. Record the closest distance at which readings remain stable and accurate.

| Item | Expected | Observed |
|---|---|---|
| Minimum stable distance (mm) | ~30-40 | |
| Behavior below minimum | Inaccurate or error | |

#### Test 4: Target Surface Effect

**Procedure**
1. Place each target at a fixed distance of 1000 mm.
2. Record 10 readings per surface and average them.

| Target Surface | Actual (mm) | Average Reading (mm) | Error (%) | Notes |
|---|---|---|---|---|
| White card | 1000 | | | |
| Black card | 1000 | | | |
| Cardboard | 1000 | | | |
| Metal | 1000 | | | |

#### Test 5: Ambient Light Effect

**Procedure**
1. Place a white target at 1000 mm and 2000 mm.
2. Take readings indoors (room light), in dim light, and near sunlight or outdoors.

| Condition | Actual (mm) | Average Reading (mm) | Readings Stable? (Y/N) | Notes |
|---|---|---|---|---|
| Indoor, room light | 1000 | | | |
| Indoor, dim | 1000 | | | |
| Sunlight / outdoor | 1000 | | | |
| Indoor, room light | 2000 | | | |
| Sunlight / outdoor | 2000 | | | |

#### Test 6: Update Rate vs Timing Budget

**Procedure**
1. Change `setTimingBudget()` to each value below.
2. Count readings over 10 seconds (or timestamp each reading with `millis()`).
3. Note the noise in readings with the target at 1000 mm.

| Timing Budget (ms) | Readings per Second | Reading Spread at 1000 mm (max − min, mm) |
|---|---|---|
| 20 | | |
| 50 | | |
| 100 | | |
| 200 | | |

#### Test 7: Angle / Field of View

**Procedure**
1. Place a small target (about 50 mm wide) at 1000 mm, centered on the sensor.
2. Move it sideways in steps and record when the sensor stops detecting it.

| Lateral Offset (mm) | Detected? (Y/N) | Reading (mm) |
|---|---|---|
| 0 | | |
| 100 | | |
| 200 | | |
| 300 | | |

#### Test 8: Shared I2C Bus with INA260 (Optional)

**Procedure**
1. Connect both sensors to GPIO21/GPIO22.
2. Run the I2C scanner, then read both sensors in one sketch.

| Item | Expected | Observed | Pass/Fail |
|---|---|---|---|
| Addresses detected | 0x29 and 0x40 | | |
| Both sensors read without errors | Yes | | |

#### Observations

* 
* 
* 

#### Results Summary

| Test | Result | Pass/Fail |
|---|---|---|
| 1. Power and I2C Detection | | |
| 2. Distance Accuracy | | |
| 3. Minimum Range | | |
| 4. Target Surface Effect | | |
| 5. Ambient Light Effect | | |
| 6. Update Rate vs Timing Budget | | |
| 7. Angle / Field of View | | |
| 8. Shared I2C Bus | | |

#### Conclusion

The VL53L1X [is / is not] suitable for distance and obstacle detection in the Smart EV based on the results above. Recommended settings: timing budget of ___ ms, mounting height of ___ mm, and detection range of ___ to ___ mm.

# Test procedures, observations, and results
### Test Procedures, Observations, and Results

* XIAO ESP32S3 Sense with camera board and heat sink installed
* USB-C cable and computer running Arduino IDE (Serial Monitor at 115200 baud)
* microSD card (FAT32, 32 GB or smaller)
* Wi-Fi network or phone hotspot
* Optional: USB power meter, thermometer or IR temperature gun, ESP32-DevKitC V4 + 3 jumper wires

#### Test 1: Power and Upload

**Procedure**
1. Connect the XIAO by USB-C.
2. Upload a basic sketch that prints to the Serial Monitor.

| Item | Expected | Observed | Pass/Fail |
|---|---|---|---|
| Board powers on (LED) | On | | |
| Upload succeeds | Yes | | |
| Serial Monitor output | Text appears | | |

#### Test 2: Camera Detection and Stream

**Procedure**
1. Upload the CameraWebServer example (see `firmware/`).
2. Open the printed IP address in a browser and start the stream.

| Item | Expected | Observed | Pass/Fail |
|---|---|---|---|
| Camera initializes | No "camera init failed" error | | |
| Camera model detected | OV5640 / OV3660 / OV2640 | | |
| Live stream opens | Video visible in browser | | |

#### Test 3: Frame Rate vs Resolution

**Procedure**
1. Change the resolution in the web interface.
2. Record the frame rate shown (or count frames over 10 seconds).

| Resolution | Frame Rate (fps) | Image Quality Notes |
|---|---|---|
| QVGA (320x240) | | |
| VGA (640x480) | | |
| HD (1280x720) | | |

#### Test 4: Wi-Fi Range

**Procedure**
1. Stream at VGA resolution.
2. Move the laptop away from the XIAO and note stream quality at each distance.

| Distance (m) | Stream Quality (smooth / laggy / drops) | Notes |
|---|---|---|
| 1 | | |
| 5 | | |
| 10 | | |
| 20 | | |

#### Test 5: Heat and Current During Streaming

(Seeed measured ~140 mA average / ~347 mA peak while streaming, and 63.6 °C without a heat sink.) 

**Procedure**
1. Stream continuously for 10+ minutes.
2. Record board temperature and current (USB power meter) at each interval.

| Time (min) | Temperature (°C) | Current (mA) | Notes |
|---|---|---|---|
| 0 | | | |
| 5 | | | |
| 10 | | | |

#### Test 6: microSD Write

**Procedure**
1. Upload the microSD test sketch (see `firmware/`).
2. Check the card on a computer afterward.

| Item | Expected | Observed | Pass/Fail |
|---|---|---|---|
| Card mounts | "Write OK" printed | | |
| File on card | test.txt present | | |

#### Test 7: UART Link to DevKitC (Optional)

**Procedure**
1. Wire XIAO D6 → DevKitC GPIO16, XIAO D7 → DevKitC GPIO17, GND → GND.
2. Upload the UART test sketches (see `firmware/`) to both boards.

| Item | Expected | Observed | Pass/Fail |
|---|---|---|---|
| DevKitC receives XIAO message | "XIAO: hello" every second | | |
| XIAO receives DevKitC message | "DevKitC: hello" every second | | |

#### Observations

*Record anything unexpected: stream drops, resets, overheating, camera model differences.*

#### Results Summary

| Test | Result | Notes |
|---|---|---|
| 1. Power and Upload | | |
| 2. Camera Stream | | |
| 3. Frame Rate | | |
| 4. Wi-Fi Range | | |
| 5. Heat and Current | | |
| 6. microSD Write | | |
| 7. UART Link | | |

#### Conclusion
*Note if ESP32S3 Sense is suitable. Note if any changes must be made (heat sink, power supply, stream quality, etc)

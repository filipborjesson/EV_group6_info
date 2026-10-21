# Firmware examples and setup instructions
### Firmware Examples and Source Code

* [Adafruit VL53L1X Arduino Library (GitHub)](https://github.com/adafruit/Adafruit_VL53L1X)
* [Adafruit CircuitPython VL53L1X Library (GitHub)](https://github.com/adafruit/Adafruit_CircuitPython_VL53L1X)
* [ST VL53L1X Ultra Lite Driver API (STSW-IMG009)](https://www.st.com/en/embedded-software/stsw-img009.html)
* [Arduino-ESP32 Installation Guide](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html)

### Setup Instructions (ESP32-DevKitC + Arduino IDE)

#### 1. Install ESP32 Board Support

1. Open Arduino IDE → **File → Preferences**
2. In **Additional Boards Manager URLs**, add:
   `https://espressif.github.io/arduino-esp32/package_esp32_index.json`
3. Go to **Tools → Board → Boards Manager**, search **esp32**, and install **esp32 by Espressif Systems**
4. Select **Tools → Board → ESP32 Arduino → ESP32 Dev Module**

#### 2. Install the VL53L1X Library

1. Go to **Sketch → Include Library → Manage Libraries**
2. Search **Adafruit_VL53L1X** and install it (accept any dependencies)

#### 3. Wire the Sensor

* ESP32 3V3 → VL53L1X VIN
* ESP32 GND → VL53L1X GND
* ESP32 GPIO21 → VL53L1X SDA
* ESP32 GPIO22 → VL53L1X SCL

Remove the protective tape from the sensor window before testing.

#### 4. Upload the Test Sketch

1. Connect the ESP32 by USB and select the correct port under **Tools → Port**
2. Upload the sketch below
3. Open **Tools → Serial Monitor** at **115200 baud**

### Example Firmware: Basic Distance Reading

```cpp
#include <Wire.h>
#include "Adafruit_VL53L1X.h"

#define SDA_PIN 21
#define SCL_PIN 22

Adafruit_VL53L1X vl53 = Adafruit_VL53L1X();

void setup() {
  Serial.begin(115200);
  while (!Serial) delay(10);

  Wire.begin(SDA_PIN, SCL_PIN);

  if (!vl53.begin(0x29, &Wire)) {
    Serial.print("VL53L1X not found, error: ");
    Serial.println(vl53.vl_status);
    while (1) delay(10);
  }
  Serial.println("VL53L1X found");

  if (!vl53.startRanging()) {
    Serial.print("Could not start ranging, error: ");
    Serial.println(vl53.vl_status);
    while (1) delay(10);
  }

  vl53.setTimingBudget(50);   // ms per measurement (15, 20, 33, 50, 100, 200, 500)
  Serial.print("Timing budget (ms): ");
  Serial.println(vl53.getTimingBudget());
}

void loop() {
  if (vl53.dataReady()) {
    int16_t distance = vl53.distance();
    if (distance == -1) {
      Serial.print("Read error: ");
      Serial.println(vl53.vl_status);
      return;
    }
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" mm");
    vl53.clearInterrupt();
  }
}
```

### Example Firmware: I2C Bus Scanner

Use this to confirm the sensor is detected at 0x29 (and the INA260 at 0x40 if both are connected).

```cpp
#include <Wire.h>

void setup() {
  Serial.begin(115200);
  Wire.begin(21, 22);
  Serial.println("Scanning I2C bus...");
  for (uint8_t addr = 1; addr < 127; addr++) {
    Wire.beginTransmission(addr);
    if (Wire.endTransmission() == 0) {
      Serial.print("Device found at 0x");
      Serial.println(addr, HEX);
    }
  }
  Serial.println("Scan complete");
}

void loop() {}
```

### Expected Results

* Serial Monitor prints "VL53L1X found" followed by distance readings in mm
* Readings change as an object moves toward or away from the sensor
* Valid readings begin at roughly 30 mm; closer objects may read inaccurately

### Troubleshooting

* **"VL53L1X not found":** check SDA/SCL wiring, power, and run the I2C scanner
* **Readings stuck or noisy:** confirm the protective tape is removed and nothing covers the sensor window
* **Short range outdoors:** sunlight reduces maximum range; test indoors first
* **No serial output:** confirm 115200 baud and the correct COM port

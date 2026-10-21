# Firmware examples and setup instructions
### Firmware Examples and Source Code

* [Seeed XIAO ESP32S3 Getting Started Wiki](https://wiki.seeedstudio.com/xiao_esp32s3_getting_started/)
* [Arduino-ESP32 Installation Guide](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html)
* CameraWebServer example: built into the ESP32 Arduino package (**File → Examples → ESP32 → Camera → CameraWebServer**)

### Setup Instructions (XIAO ESP32S3 Sense + Arduino IDE)

#### 1. Install ESP32 Board Support

1. Open Arduino IDE → **File → Preferences**
2. In **Additional Boards Manager URLs**, add:
   `https://espressif.github.io/arduino-esp32/package_esp32_index.json`
3. Go to **Tools → Board → Boards Manager**, search **esp32**, and install **esp32 by Espressif Systems**

#### 2. Select the Board and Settings

1. **Tools → Board → ESP32 Arduino → XIAO_ESP32S3**
2. **Tools → PSRAM → OPI PSRAM** (required for the camera)
3. Connect the XIAO by USB-C and select the port under **Tools → Port**

#### 3. Upload the Camera Web Server

1. Open **File → Examples → ESP32 → Camera → CameraWebServer**
2. Find the list of camera models (in the main sketch or `board_config.h`, depending on version) and enable only:
   `#define CAMERA_MODEL_XIAO_ESP32S3`
3. Enter your Wi-Fi network name and password in the sketch
4. Upload, then open **Tools → Serial Monitor** at **115200 baud**
5. Copy the IP address printed in the Serial Monitor into a browser on the same network

### Example Firmware: UART Link Test (XIAO side)

Sends a message to the DevKitC once per second and prints anything it receives.

```cpp
#define XIAO_TX 43  // D6
#define XIAO_RX 44  // D7

void setup() {
  Serial.begin(115200);                                   // USB serial monitor
  Serial1.begin(115200, SERIAL_8N1, XIAO_RX, XIAO_TX);    // link to DevKitC
}

void loop() {
  Serial1.println("XIAO: hello");

  while (Serial1.available()) {
    Serial.write(Serial1.read());
  }
  delay(1000);
}
```

### Example Firmware: UART Link Test (DevKitC side)

```cpp
#define RX2_PIN 16
#define TX2_PIN 17

void setup() {
  Serial.begin(115200);
  Serial2.begin(115200, SERIAL_8N1, RX2_PIN, TX2_PIN);
}

void loop() {
  while (Serial2.available()) {
    Serial.write(Serial2.read());     // print what the XIAO sends
  }
  Serial2.println("DevKitC: hello");
  delay(1000);
}
```

### Example Firmware: microSD Test

```cpp
#include "FS.h"
#include "SD.h"
#include "SPI.h"

void setup() {
  Serial.begin(115200);
  while (!Serial) delay(10);

  if (!SD.begin(21)) {               // GPIO21 = microSD chip select on the Sense board
    Serial.println("microSD mount failed");
    return;
  }

  File f = SD.open("/test.txt", FILE_WRITE);
  if (f) {
    f.println("XIAO ESP32S3 Sense SD test");
    f.close();
    Serial.println("Write OK");
  } else {
    Serial.println("Could not open file");
  }
}

void loop() {}
```

### Expected Results

* **CameraWebServer:** Serial Monitor prints an IP address; opening it in a browser shows the camera controls and a live stream.
* **UART test:** each board's Serial Monitor shows the other board's "hello" message every second.
* **microSD test:** Serial Monitor prints "Write OK" and `test.txt` appears on the card.

### Troubleshooting

* **"Camera init failed":** PSRAM is not set to OPI PSRAM, the wrong camera model is selected, or the camera board is not fully seated.
* **No Serial Monitor output:** check that **Tools → USB CDC On Boot** is **Enabled**, and that the baud rate is 115200.
* **Upload fails:** hold the **BOOT** button while plugging in USB-C, then upload again.
* **Can't open the stream:** the laptop must be on the same Wi-Fi network as the XIAO. University networks with a login page (eduroam) may not work; use a phone hotspot or a lab router.
* **microSD mount failed:** card must be FAT32 and 32 GB or smaller.
* **No UART messages:** check that TX goes to RX on both sides and that the grounds are connected.

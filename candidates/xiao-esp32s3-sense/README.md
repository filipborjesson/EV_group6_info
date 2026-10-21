# Seeed Studio XIAO ESP32S3 Sense (Camera and Wi-Fi Streaming)

Status: Candidate — not finalized.

Assigned member: Jonathan Miller

Add datasheets and manuals to `documents/`, connection diagrams to `wiring/`, code to `firmware/`, and test procedures and results to `tests/`. Document power requirements, interfaces, proposed pins, and compatibility concerns.

### Specifications

* Processor: ESP32-S3, dual-core, 240 MHz
* Memory: 8 MB PSRAM / 8 MB flash
* Wireless: 2.4 GHz Wi-Fi, Bluetooth LE 5.0 (U.FL external antenna connector)
* Camera: OV5640, up to 2592 x 1944
* Microphone: digital PDM microphone
* Storage: onboard microSD slot (up to 32 GB)
* GPIO: 11 edge pins, 2 on the B2B connector
* Interfaces: I²C, SPI, UART, I²S, ADC
* Logic: 3.3 V
* Power input: 5 V USB-C or 3.7 V LiPo battery on the BAT pads (onboard charging)
* 3V3 output: up to 700 mA, shared with the board's own camera and Wi-Fi
* Operating temperature: -20 °C to 65 °C
* Dimensions: 21 x 17.8 x 15 mm
* Price: $13.90 (Seeed Studio)

### Wiring

#### XIAO ESP32S3 Pinout

| XIAO Pin | GPIO | Function | Available with Sense board? |
|---|---|---|---|
| D0 | GPIO1 | Digital / analog | Yes |
| D1 | GPIO2 | Digital / analog | Yes |
| D2 | GPIO3 | Digital / analog | Yes |
| D3 | GPIO4 | Digital / analog | Yes |
| D4 | GPIO5 | I2C SDA (default) | Yes |
| D5 | GPIO6 | I2C SCL (default) | Yes |
| D6 | GPIO43 | UART TX | Yes |
| D7 | GPIO44 | UART RX | Yes |
| D8 | GPIO7 | SPI SCK | Shared with microSD |
| D9 | GPIO8 | SPI MISO | Shared with microSD |
| D10 | GPIO9 | SPI MOSI | Shared with microSD |
| 5V | — | 5 V from USB (VBUS) | — |
| 3V3 | — | 3.3 V regulated output | — |
| GND | — | Ground | — |

D8–D10 are shared with the onboard microSD card when the Sense camera board is attached, leaving 8 free pins.

Reserved on the Sense board (do not use):
* GPIO10–18, 38–40, 47–48 (camera)
* GPIO41–42 (microphone)
* GPIO21 (microSD chip select / user LED)

#### Proposed Connection to ESP32-DevKitC (UART)

The XIAO handles the camera and streams video over Wi-Fi. A UART link to the main controller is proposed for status messages or detection results.

| XIAO Pin | ESP32-DevKitC Pin | Signal | Wire Color (suggested) |
|---|---|---|---|
| D6 (GPIO43, TX) | GPIO16 (RX2) | XIAO → DevKitC data | Blue |
| D7 (GPIO44, RX) | GPIO17 (TX2) | DevKitC → XIAO data | Yellow |
| GND | GND | Common ground | Black |

TX connects to RX in both directions. Both boards use 3.3 V logic, so no level shifting is needed.

#### Power Options

| Option | Connection | Notes |
|---|---|---|
| USB-C | 5 V from a USB supply or power bank | Simplest for bench testing |
| LiPo battery | 3.7 V cell on BAT+ / BAT− pads | Charges from USB-C when plugged in |
| 5V pin | External 5 V into the 5V pin | Requires a diode in series (per Seeed) to protect the USB port |

#### Power Consumption (Seeed measurements)

| Mode | Average | Peak |
|---|---|---|
| Idle (USB 5 V) | ~38 mA | — |
| Wi-Fi active | ~110 mA | — |
| Camera streaming (USB 5 V) | ~140 mA | ~347 mA |
| Camera streaming (battery) | ~155 mA | ~366 mA |

### Notes

* The board gets hot while streaming: Seeed reported 63.6 °C without a heat sink and about 10 °C less with one. Install the included heat sink on the thermal pad.
* Separate the camera expansion board by sliding it sideways; never pull straight up, to avoid damaging the B2B (board-to-board) connector.
* An external antenna can be used on the U.FL connector if Wi-Fi range is too short.
* Only 8 edge pins are free once the camera and microSD are in use.

### Compatibility Notes

* A separate microSD breakout may not be needed if we use the Sense board's onboard microSD slot.
* Filip's notes and the VL53L1X folder assume the ESP32-DevKitC V4 as the main controller; this board is proposed as a camera add-on linked over UART. To be confirmed with the team.
* Power budget: camera streaming peaks near 350 mA, which must be covered by the vehicle's battery alongside the motors and sensors.
* Camera: units may ship with OV5640, OV3660, or OV2640 sensors; confirm which one arrives before writing camera code.

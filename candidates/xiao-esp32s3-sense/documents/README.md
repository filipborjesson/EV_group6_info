# Datasheets, manuals, schematics, and source links

### Resources and Links: 
**XIAO ESP32S3 Sense**

* [Seeed XIAO ESP32S3 Sense Product Page](https://www.seeedstudio.com/XIAO-ESP32S3-Sense-p-5639.html)
* [Seeed XIAO ESP32S3 Getting Started Wiki](https://wiki.seeedstudio.com/xiao_esp32s3_getting_started/)
* [XIAO ESP32S3 Sense Schematic (PDF)](https://files.seeedstudio.com/wiki/SeeedStudio-XIAO-ESP32S3/new-res/202003753_XIAO%20ESP32S3%20Sense_v1.5_SCH_260226.pdf.pdf)
* [Sense Expansion Board Schematic (PDF)](https://files.seeedstudio.com/wiki/SeeedStudio-XIAO-ESP32S3/res/XIAO_ESP32S3_Exp_Board_v1.2_SCH_PDF_260810.pdf)
* [XIAO ESP32S3 Sense Pinout Sheet (XLSX)](https://files.seeedstudio.com/wiki/SeeedStudio-XIAO-ESP32S3/res/XIAO_ESP32S3_Sense_Pinout.xlsx)

**ESP32-S3 Chip**

* [ESP32-S3 Datasheet (PDF)](https://files.seeedstudio.com/wiki/SeeedStudio-XIAO-ESP32S3/res/esp32-s3_datasheet.pdf)
* [ESP32-S3 Technical Reference Manual (Espressif)](https://www.espressif.com/sites/default/files/documentation/esp32-s3_technical_reference_manual_en.pdf)

**Camera**

* [OV5640 Camera Datasheet (PDF)](https://files.seeedstudio.com/wiki/SeeedStudio-XIAO-ESP32S3/res/OV5640_datasheet.pdf)

**Software**

* [Arduino-ESP32 Installation Guide](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html)

### Purpose
The XIAO ESP32S3 Sense is being evaluated for camera and Wi-Fi Streaming module
* Runs the camera and streams video over Wi-Fi
* Connects to DevKitC over UART

### Specifications
* Processor: ESP32-S3, dual-core, up to 240 MHz
* Memory: 8 MB PSRAM / 8 MB flash
* Wireless: 2.4 GHz Wi-Fi, Bluetooth LE 5.0, U.FL external antenna connector
* Camera: OV5640, up to 2592 x 1944 (some units ship with OV3660 or OV2640)
* Microphone: digital PDM microphone
* Storage: onboard microSD slot, up to 32 GB
* GPIO: 11 edge pins (8 free with the Sense board attached)
* Interfaces: I²C, SPI, UART, I²S, ADC
* Logic level: 3.3 V
* Power input: 5 V USB-C or 3.7 V LiPo (onboard charging)
* Current draw: ~38 mA idle, ~110 mA Wi-Fi, ~140 mA average / ~350 mA peak while streaming
* Operating temperature: -20 °C to 65 °C

### Compatibility 

#### ESP32-DevKitC
* Both board use 3.3V logic, directly connect over UART
* XIAO D6 (TX) → DevKitC GPIO16 (RX2), XIAO D7 (RX) → DevKitC GPIO17 (TX2), shared GND

#### microSD Breakout (#254)
* The Sense board has its own microSD, this might be unnecessary, or the two could split the data (images on XIAO, sensors on DevKitC)

#### Pins
* There are 8 edge pins free once camera and microSD are in use

### Integration
* Camera should face forward with clear view; the board is small and should mount easily
* The board reaches ~63.6 °C while streaming without a heat sink (Seeed test); the included heat sink lowers this by ~10 °C. Leave airflow around the board.
* The board needs its own 5V or LiPo supply that can handle ~350 mA peaks, seperate of motor power

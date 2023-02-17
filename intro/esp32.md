# Introduction to ESP32

It's a microcontroller (like an Arduino) with built in WiFi and Bluetooth. Much faster and more capable than an Arduino though. 

Arduino: 8-bit processor, 20 MHz, 2KByte RAM, 32KByte flash, 1Kbyte EEPROM, 23 I/O pins
ESP32: 32-bit processor, 160 or 240 MHz, 512Kbyte RAM, 384KByte flash, various board types, typically 34-44 I/O pins

## Programming the ESP32 with the Arduino IDE

There are other ways to program an ESP32, it can even run Micro Python natively. But for familiarity and use of legacy code we'll use the Arduino IDE.

Official docs - https://espressif-docs.readthedocs-hosted.com/projects/arduino-esp32/en/latest/installing.html

* Download the latest Arduino IDE
* Open settings, "Additional Board Manager URLs" and enter https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
* Ok this and install
* Restart the IDE
* Go to Tools->Board->Boards Manager
* Type in esp32 and click install
* 


### Installing extra packages


# ESP32-S3 Webradio

ESP32 web radio client integrated with Home Assistant & Logitech Media Server (LMS). Features voice control via HA, Bluetooth speaker mode, and BLE thermometer tracking. Part of my personal home automation stack (OMV/Arch).

## Hardware

- **MCU:** ESP32-S3 N16R8 (16MB Flash, 8MB PSRAM)
- **Amplifier:** TPA3116 D2 (XH-M543)
- **Power:** Laptop adapter 19V -> DC-DC Stepdown (MP2307) -> ESP32 5V
- **Speakers:** 2x10W (8 Ohm)
- **Piezo:** Active buzzer on GPIO

## Pinout

| Function | GPIO | Description |
|----------|------|-------------|
| I2S BCLK | GPIO5 | DAC clock |
| I2S LCLK | GPIO6 | Word select |
| I2S DIN | GPIO7 | Data out |
| I2S MCLK | GPIO4 | Master clock |
| Amp MUTE | GPIO48 | TPA3116 SD pin |
| Piezo | GPIO47 | Series 100Ω resistor |

## Features

- **Webradio:** LMS client streaming via Home Assistant
- **Bluetooth Speaker:** AirPlay/BT audio input
- **BLE Tracking:** 4x Bluetooth thermometers (Xiaomi HHCCJCY01)
- **Notifications:** HA triggers -> Piezo beep
- **Pop-free Startup:** MUTE pin control during boot

## Installation

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd esp32-home-auto
   ```

2. **Create secrets.yaml:**
   ```bash
   cp secrets.yaml.example secrets.yaml
   ```

3. **Edit secrets.yaml with your credentials:**
   - WiFi SSID and password
   - Home Assistant API password and encryption key
   - OTA password
   - Web server credentials
   - BLE thermometer MAC addresses (4x)

4. **Compile and upload via ESPHome:**
   ```bash
   esphome compile esp32-webradio.yaml
   esphome upload esp32-webradio.yaml
   ```

5. **Add device to Home Assistant:**
   - The device will auto-discover via the API
   - Configure entities in HA dashboard

## Requirements

- ESPHome 2023.12+
- Home Assistant 2023.12+
- Python 3.9+

## License

Use at your own risk. Experimental electrical dev project. 🛠️

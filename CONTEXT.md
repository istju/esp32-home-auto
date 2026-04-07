# ESP32-S3 Webradio Projekt Kontextus

## Hardver
- **MCU:** ESP32-S3 N16R8 (16MB Flash, 8MB PSRAM)
- **Erősítő:** TPA3116 D2 (XH-M543)
- **Táp:** Laptop adapter 19V -> DC-DC Stepdown (MP2307) -> ESP32 5V
- **Hangszóró:** 2x10W (8 Ohm)
- **Piezo:** Aktív buzzer GPIO-n

## Pinout (ESP32-S3)
| Funkció | Pin | Megjegyzés |
|---------|-----|------------|
| I2S BCLK | GPIO5 | DAC órajel |
| I2S LCLK | GPIO6 | Word select |
| I2S DIN | GPIO7 | Data out |
| I2S MCLK | GPIO4 | Master clock |
| Amp MUTE | GPIO48 | TPA3116 SD pin |
| Piezo | GPIO47 | Sorba 100Ω |

## Szoftver
- **Firmware:** ESPHome (YAML + custom C++)
- **Integráció:** Home Assistant (OMV szerver)
- **Audio:** LMS kliens + AirPlay
- **Szenzorok:** 4x Bluetooth hőmérő (ESP32 BLE tracker)

## Követelmények
- Pop-mentes bekapcsolás (MUTE pin vezérlés)
- Zajmentes tápellátás (DC-DC shielded)
- HA notification -> Piezo csipogás
# ESP32 Webradio GPIO Pinout

## Audio (I2S)
| GPIO | Function | Component |
|------|----------|-----------|
| GPIO4 | MCLK | DAC master clock |
| GPIO5 | BCLK | DAC bit clock |
| GPIO6 | LCLK | DAC word select |
| GPIO7 | DIN | DAC data out |

## Outputs
| GPIO | Function | Component |
|------|----------|-----------|
| GPIO47 | PWM | Piezo buzzer (1000Hz) |
| GPIO48 | GPIO | TPA3116 Amp MUTE (SD pin) |

## Reserved/Available
| GPIO | Status |
|------|--------|
| GPIO0-3 | Available |
| GPIO8-46 | Available |
| GPIO9-46 | Available (check PSRAM usage) |

## Notes
- I2S uses GPIO4-7 (fixed for ESP32-S3 I2S peripheral)
- GPIO47/48 are high-numbered GPIOs, avoid conflicts
- BLE thermometers use radio, no GPIO pins

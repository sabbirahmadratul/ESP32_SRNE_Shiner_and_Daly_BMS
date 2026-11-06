# Classic ESP32 conversion notes

## Target
- PlatformIO environment: `esp32dev`
- Intended hardware: original ESP32 / ESP32-WROOM-32 / ESP32-WROOM-32D
- Flash layout: 4 MB (`firmware/partitions_4mb.csv`)

## Removed / disabled hardware-specific features
- ESP32-S3 native USB CDC / USB mode build flags
- GPIO48 NeoPixel status LED
- GPIO0 BOOT-button interrupt, triple-press pairing and long-press local factory reset
- GPIO-mapped UART1 RS485 controller transport

## Retained
- Wi-Fi and first-boot SoftAP provisioning
- BLE controller and BMS discovery/communication
- Firebase Realtime Database integration
- OTA code path, now restricted to chip family `ESP32`
- Flutter Android/Web application and Firebase rules

## Limitations
- Controller communication in this build is BLE-only; RS485 is not available.
- The setup SoftAP opens automatically on an unconfigured device. Since the BOOT-button handler was removed, an already-configured gateway cannot reopen setup mode using a physical button. The authenticated cloud factory-reset command remains in the firmware.
- The web-flasher manifest is deliberately empty. Existing ESP32-S3 binaries are not compatible with classic ESP32 and must not be relabelled or flashed to it.
- The included 4 MB partition layout reserves two OTA app slots. Confirm the compiled application fits the `0x1C0000` app partition.

## Build and verification status
The source and configuration have been converted, but a PlatformIO toolchain was not available in the editing environment. This ZIP has **not** been compiled or hardware-tested. Open `firmware/` in PlatformIO, build the `esp32dev` environment, then test Wi-Fi provisioning, BLE pairing, Firebase publishing and OTA on the actual board before relying on it.

"# NoxBrain website flasher · classic ESP32 conversion

The previous manifest referenced ESP32-S3 images. Those images must never be flashed to the classic ESP32 target. The manifest has therefore been cleared intentionally and the web installer remains disabled until a real `esp32dev` build is produced and verified.

After building with PlatformIO, create and verify the classic ESP32 bootloader (offset `0x1000`), partition table (`0x8000`), OTA data (`0xE000`) and application (`0x10000`) artifacts. Only then should a new manifest and matching release metadata be published. Do not relabel or reuse ESP32-S3 binaries as ESP32 binaries.

This converted firmware uses BLE for controller/BMS communication. GPIO48 LED, GPIO0 BOOT-button handling and the GPIO-mapped RS485 transport are intentionally removed. Initial setup Wi-Fi opens on first boot; there is no physical-button recovery/re-pairing mode in this build.

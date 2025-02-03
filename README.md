```markdown
# ESP32-CAM Face Recognition Door Lock

A smart door lock system using ESP32-CAM for face recognition, enabling secure and contactless entry.

## Description

This project leverages the ESP32-CAM module to create a face recognition-based door access system. It detects faces in real-time, cross-checks them against enrolled profiles, and triggers a relay to unlock the door upon a match. Features include live video streaming, face enrollment via a web interface, and LED status indicators.

## Features
- Real-time video streaming over websockets.
- Face detection using the **MTMN model**.
- Face enrollment mode (save up to 7 profiles).
- Recognition mode with relay control for door access.
- Red/Green LED indicators for access denial/granted states.
- Web interface for enrollment and management.

## Hardware Setup (Pin Configuration)
| Component      | ESP32-CAM Pin |
|----------------|---------------|
| Relay          | GPIO 12       |
| Red LED        | GPIO 13       |
| Green LED      | GPIO 15       |
| Camera Data Pins| Y2-Y9 (GPIO 2-9) |
| Camera XCLK    | GPIO 10       |
| Camera PCLK    | GPIO 11       |
| Camera VSYNC   | GPIO 3        |

**Note:** Pins are configured for the `CAMERA_MODEL_AI_THINKER` module. Adjustments may be needed for other camera models. Circuit diagrams should be validated against your hardware.

## Getting Started
1. **Prerequisites**:
   - ESP32-CAM module with OV2640 camera.
   - Arduino IDE or PlatformIO with ESP32 support.
   - Libraries: `esp32-face`, `ArduinoWebsockets`, `esp_http_server`.

2. **WiFi Configuration**:
   Update the credentials in `FaceDoorEntryESP32Cam.ino`:
   ```cpp
   const char* ssid = "YourSSID";
   const char* password = "YourPassword";
   ```

3. **Upload & Run**:
   - Connect the ESP32-CAM via USB-to-UART.
   - Compile and upload the code. Ensure PSRAM is enabled in IDE settings.

## Code Overview
- **`FaceDoorEntryESP32Cam.ino`**: Main workflow (WiFi setup, camera init, server handlers).
  - `app_facenet_main()`: Initializes face recognition models.
  - `handle_message()`: Processes web commands (enroll/delete faces).
  - Recognition logic triggers the relay via `open_door()`.

## Notes
- Performance depends on lighting conditions. Ensure faces are well-lit.
- The relay is active-high (`HIGH` unlocks the door). Adjust polarity if needed.
- Face data is stored in ESP32's flash memory (non-volatile).
```
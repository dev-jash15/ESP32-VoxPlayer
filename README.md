# 🎙️ ESP32-VoiceTube-Remote

**A voice-controlled Bluetooth remote designed to control YouTube video playback on a PC.**

![Platform](https://img.shields.io/badge/platform-ESP32-green.svg) ![Connectivity](https://img.shields.io/badge/connectivity-Bluetooth-blue.svg) ![Status](https://img.shields.io/badge/status-functional-success.svg)

## 📖 Overview

This project turns an ESP32-S3 into a wireless voice remote. Instead of processing video locally, the ESP32 listens for voice commands, processes them on-edge (offline), and sends control signals via **Bluetooth** to a connected PC.

This allows for hands-free control of a YouTube video player running on a computer (Windows/Mac/Linux) without needing a keyboard or mouse.

### ✨ Key Features
* **Voice Activation:** Uses an I2S Microphone (INMP441) to detect spoken commands.
* **Bluetooth Connectivity:** Establishes a wireless link between the ESP32 and the PC.
* **Low Latency:** Rapid processing of voice keywords to trigger playback actions instantly.
* **PC Integration:** Maps voice commands to standard YouTube keyboard shortcuts (or Serial commands).

---

## 🛠️ Hardware Requirements

| Component | Function |
| :--- | :--- |
| **ESP32 / ESP32-S3** | The main controller and Bluetooth interaction unit. |
| **INMP441 Microphone** | Omnidirectional I2S MEMS microphone for high-quality audio capture. |
| **PC / Laptop** | Runs the YouTube video player (connected via Bluetooth). |
| **Micro USB Cable** | For power and programming. |

---

## 🔌 Wiring (I2S Mic)

The microphone is connected via the I2S interface to minimize noise and CPU overhead.

| INMP441 Pin | ESP32 Pin (Configurable) |
| :--- | :--- |
| **SCK** | GPIO 14 |
| **WS** | GPIO 15 |
| **SD** | GPIO 32 |
| **L/R** | GND (Set to Left Channel) |
| **VDD** | 3.3V |
| **GND** | GND |

---

## 🗣️ Supported Commands

The system is trained to recognize the following keywords. When recognized, the ESP32 sends the corresponding action over Bluetooth:

| Voice Command | Bluetooth Action | PC Result (YouTube) |
| :--- | :--- | :--- |
| **"PLAY"** | Sends `Space` / `k` | Toggles Play/Pause |
| **"PAUSE"** | Sends `Space` / `k` | Toggles Play/Pause |
| **"NEXT"** | Sends `Shift+N` | Plays next video |
| **"PREVIOUS"** | Sends `Shift+P` | Plays previous video |

*(Note: Exact key mappings depend on the Bluetooth implementation mode selected in `config.h`)*

---

## 🚀 Installation & Setup

### 1. ESP32 Firmware
1.  Open the project in **PlatformIO** or **Arduino IDE**.
2.  Install required libraries:
    * `ESP32-A2DP` (if using A2DP mode) or `BleKeyboard` (if using HID mode).
    * `TensorFlow Lite Micro` (or your specific speech recognition lib).
3.  Flash the code to your ESP32.

### 2. PC Connection
1.  Power on the ESP32.
2.  Open your PC's **Bluetooth Settings**.
3.  Scan for new devices.
4.  Connect to **"ESP32-Voice-Remote"**.
5.  Once paired, the ESP32 acts as an input device.

### 3. Running
1.  Open YouTube in your browser.
2.  Ensure the browser window is in focus.
3.  Speak a command (e.g., "NEXT") and watch the video change.

---

## 📂 Project Structure

```text
ESP32-VoiceTube-Remote/
├── src/
│   ├── main.cpp          # Main logic (Voice detection loop)
│   ├── BluetoothMgr.cpp  # Handles BT connection and sending signals
│   └── VoiceModel.cpp    # Speech recognition logic/TFLite model
├── include/
│   ├── config.h          # Pin definitions and BT settings
│   └── commands.h        # Mapping voice keywords to BT signals
├── README.md
└── platformio.ini        # Project configuration

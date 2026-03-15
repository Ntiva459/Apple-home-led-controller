# ESP32 HomeKit RGB LED Strip Controller

![ESP32](https://img.shields.io/badge/ESP32-IoT-blue)
![HomeKit](https://img.shields.io/badge/HomeKit-Compatible-green)
![Platform](https://img.shields.io/badge/Platform-Arduino-orange)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

Control a **12V RGB LED strip** using an **ESP32** and **Apple HomeKit**.

This project uses the **HomeSpan library** to turn an ESP32 into a **HomeKit RGB LightBulb accessory**, allowing you to control **power, color, brightness, and saturation** directly from the **Apple Home app**.

The ESP32 drives the LED strip through **MOSFET transistors**, enabling safe control of **12V LED strips using PWM**.

---

# Features

• Native **Apple HomeKit support**  
• Control **On / Off**  
• Adjust **Brightness**  
• Change **Hue (Color)**  
• Change **Saturation**  
• Smooth PWM LED control  
• Works with **iPhone / iPad Home App**  
• Simple hardware setup  

---

# Hardware Required

- ESP32 Dev Board
- 12V RGB LED Strip *(common anode)*
- 3 × N-Channel MOSFETs *(IRLZ44N / IRLZ34N or similar logic-level MOSFETs recommended)*
- 12V Power Supply
- Optional Gate Resistors (~220Ω)
- Wires / Breadboard

---

# Wiring

| ESP32 Pin | LED Channel |
|-----------|-------------|
| GPIO 25 | Red |
| GPIO 26 | Green |
| GPIO 27 | Blue |

### Wiring Concept

```
ESP32 GPIO ---- Gate (MOSFET)

MOSFET Drain ---- LED Color Channel
MOSFET Source ---- GND

LED Strip +12V ---- 12V Power Supply

ESP32 GND ---- Power Supply GND
```

⚠ **Important**

The **ESP32 GND and the LED power supply GND must be connected together.**

Otherwise the MOSFETs will not switch correctly.

---

# Software Requirements

- Arduino IDE
- ESP32 Arduino Core
- HomeSpan Library

Install HomeSpan from Arduino Library Manager:

```
Sketch → Include Library → Manage Libraries
Search: HomeSpan
```

Or install manually:

https://github.com/HomeSpan/HomeSpan

---

# WiFi Configuration

Update your WiFi credentials inside the code:

```cpp
const char* ssid = "YOUR_WIFI";
const char* password = "YOUR_PASSWORD";
```

---

# Installation

1. Connect the ESP32 to your computer
2. Open the project in **Arduino IDE**
3. Select your **ESP32 board**
4. Install required libraries
5. Upload the sketch
6. Open **Serial Monitor (115200 baud)**

You will see a **HomeKit QR Code**.

Scan it with the **Apple Home App** to add the accessory.

---

# How It Works

The ESP32 runs a **HomeKit accessory server** using the **HomeSpan library**.

When the Home app changes a value like:

- Power
- Hue
- Saturation
- Brightness

the accessory calls the `update()` function.

The HSV color values are converted to RGB values and written to the LED pins using PWM.

Example:

```cpp
setRGB(int(r * 255), int(g * 255), int(b * 255));
```

This sets the brightness of each LED channel.

---

# PWM Output Pins

```
Red   → GPIO 25
Green → GPIO 26
Blue  → GPIO 27
```

---

# Serial Monitor Output

When everything is working correctly you should see:

```
Connecting to Wi-Fi...
Wi-Fi connected!
HomeKit RGB LightBulb ready!
Scan QR in Serial Monitor.
```

---

# Possible Improvements

Future upgrades could include:

• LED animation effects  
• Smooth fading transitions  
• Multiple LED strip support  
• WiFi configuration portal  
• HomeKit scenes support  

---

# Author

**Tivadar**

DIY Electronics • Smart Home • ESP32 Projects

---

# License

MIT License

You are free to use, modify, and distribute this project.

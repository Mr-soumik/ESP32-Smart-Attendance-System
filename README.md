# 🪪 ESP32 Smart Attendance System with Local Web Dashboard

An offline-first, real-time IoT Smart Attendance System powered by an **ESP32 microcontroller**, an **MFRC522 RFID module**, and a **0.96" SSD1306 I2C OLED display**. 

The system reads contactless UID cards/fobs in milliseconds, confirms access locally via animated OLED screens, audio beeps, and dual status LEDs, and dynamically updates an asynchronous, browser-based attendance portal hosted directly on the ESP32—**completely offline without third-party cloud services or internet access**[cite: 1, 2].

---

## 🌟 Key Features

* **Instant Contactless Sensing:** Reads 13.56 MHz RFID tags/cards via high-speed SPI communication using the RC522 transceiver module[cite: 1, 2].
* **Interactive OLED Graphical Interface:** Displays startup initialization, Wi-Fi network handshake status, scanning prompts, student name, UID, and real-time punch-in timestamps[cite: 1].
* **Local Real-Time Web Dashboard:** Hosts an asynchronous HTTP web server on the ESP32 that renders dynamic attendance records directly to any connected laptop, tablet, or smartphone browser[cite: 1, 2].
* **100% Offline-First Architecture:** Operates over a local Wi-Fi network or SoftAP without relying on external cloud endpoints or internet access[cite: 2].
* **Dual Feedback Loop:** Integrated green/red status LEDs and an active buzzer for instant audio-visual entry confirmation[cite: 1].

---

## 🛠️ Hardware Requirements

| Component | Specification / Model | Quantity |
| :--- | :--- | :--- |
| **Microcontroller** | ESP32 DevKit V1 (30-pin or 38-pin)[cite: 1] | 1 |
| **RFID Module** | RC522 (13.56 MHz RFID Reader/Writer)[cite: 1, 2] | 1 |
| **RFID Transponders** | Mifare Classic 1K Cards / S50 Key Fobs | Multiple |
| **Display** | 0.96" Monochrome I2C OLED Display (SSD1306, 128x64)[cite: 1] | 1 |
| **Indicators** | 5mm LEDs (1x Green, 1x Red) + 220Ω Resistors[cite: 1] | 2 |
| **Audio Feedback** | 5V Active Buzzer[cite: 1] | 1 |
| **Prototyping** | Full-size Breadboard & Male-to-Male / Male-to-Female Jumper Wires[cite: 1] | 1 set |
| **Power Supply** | Micro-USB Cable (5V / 1A)[cite: 1] | 1 |

---

## 📌 Pin Mapping & Wiring Schematics

### 1. RC522 RFID Reader (SPI Interface)
| RC522 Pin | ESP32 Pin | Description |
| :--- | :--- | :--- |
| **VCC** | `3.3V` | Supply Voltage (Do **NOT** connect to 5V) |
| **RST** | `GPIO 22` | Module Reset |
| **GND** | `GND` | Ground Reference |
| **MISO** | `GPIO 19` | Master-In Slave-Out (SPI) |
| **MOSI** | `GPIO 23` | Master-Out Slave-In (SPI) |
| **SCK** | `GPIO 18` | Serial Clock (SPI) |
| **SDA (SS)** | `GPIO 5` | Slave Select (CS) |

### 2. 0.96" SSD1306 OLED Display (I2C Interface)
| OLED Pin | ESP32 Pin | Description |
| :--- | :--- | :--- |
| **VCC** | `3.3V` / `5V` | Power Supply |
| **GND** | `GND` | Ground Reference |
| **SCL** | `GPIO 22` | I2C Serial Clock |
| **SDA** | `GPIO 21` | I2C Serial Data |

### 3. Peripheral Indicators (LEDs & Buzzer)
| Component | ESP32 Pin | Note |
| :--- | :--- | :--- |
| **Green LED (Anode)** | `GPIO 2` | Active HIGH via 220Ω resistor[cite: 1] |
| **Red LED (Anode)** | `GPIO 4` | Active HIGH via 220Ω resistor[cite: 1] |
| **Active Buzzer (+)** | `GPIO 15` | Digital drive output[cite: 1] |
| **All Cathodes / GND** | `GND` | Common Ground Bus[cite: 1] |

---

## 💻 Software & Library Requirements

Make sure you have the latest version of the [Arduino IDE](https://www.arduino.cc/en/software) installed with ESP32 board support enabled.

Install the following libraries via the **Arduino Library Manager** (`Sketch` -> `Include Library` -> `Manage Libraries`):

1. **MFRC522** by *GithubCommunity / miguelbalboa*
2. **Adafruit SSD1306** by *Adafruit*
3. **Adafruit GFX Library** by *Adafruit*
4. **ESPAsyncWebServer** by *me-no-dev* (or standard `WebServer.h`)
5. **AsyncTCP** by *me-no-dev*

---

## 🚀 Getting Started & Flashing

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/Mr-soumik/esp32-smart-attendance-system.git](https://github.com/Mr-soumik/esp32-smart-attendance-system.git)
   cd esp32-smart-attendance-system

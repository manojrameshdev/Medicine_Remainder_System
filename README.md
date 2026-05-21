<div align="center">

#  IoT Medicine Reminder System

**A hardware-software integrated solution designed to track medication schedules in real-time using physical smart boxes and a synchronized web dashboard.**

[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat-square)](https://github.com/manojrameshdev/Medicine_Remainder_System/issues)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](https://opensource.org/licenses/MIT)

</div>

---

## 🎥 Project Demo

<div align="center">
  <img src="https://raw.githubusercontent.com/manojrameshdev/Medicine_Remainder_System/main/images/demo_video.gif" alt="Medicine Reminder System Demo" width="100%" style="border-radius: 10px; max-width: 800px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"/>
</div>

---

## 📑 Table of Contents
- [About the Project](#-about-the-project)
- [Key Features](#-key-features)
- [Hardware & Software Showcase](#-hardware--software-showcase)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
- [Future Enhancements](#-future-enhancements)
- [License](#-license)
- [Contact](#-contact)

---

## 📖 About the Project

Managing daily medications is critical for health, but keeping track of physical pillboxes can be difficult. This project bridges the gap between physical hardware and digital tracking. By utilizing a microcontroller setup, the system monitors specific medicine boxes (Box 1, Box 2, Box 3) and updates a locally hosted web interface in real-time. 

Users can check their smartphone or laptop to see a live countdown timer and the current "Taken" or "Not Taken" status of their medications.

---

## ✨ Key Features

- **🔌 IoT Integration:** Connects physical breadboard/microcontroller hardware to a live web server.
- **⏱️ Real-Time Syncing:** Actions taken on the physical boxes instantly update the web dashboard across all connected devices.
- **📱 Responsive Web Interface:** The dashboard is fully responsive, ensuring a clean and accessible view on both mobile phones and desktop monitors.
- **🚦 Status Tracking:** Clear visual indicators for each medicine slot (e.g., Box 1, Box 2) showing if the dose is pending or completed.
- **🌐 Local Network Hosting:** Runs securely on a local IP address for fast, localized access without requiring external internet routing.

---

## 🖼️ Hardware & Software Showcase

<div align="center">
  
  <img src="https://raw.githubusercontent.com/manojrameshdev/Medicine_Remainder_System/main/images/demo_2.jpeg" alt="Hardware Setup and Desktop View" width="48%" />
  &nbsp;
  <img src="https://raw.githubusercontent.com/manojrameshdev/Medicine_Remainder_System/main/images/web_output.jpeg" alt="Mobile Dashboard View" width="22%" style="vertical-align: top;" />
  
  <br/>
  <i>(Left: Physical microcontroller setup syncing with the desktop interface. Right: Responsive mobile web dashboard.)</i>
</div>

---

## 🛠️ Tech Stack

*Update the hardware components below based on your exact breadboard setup.*

**Hardware:**
- Microcontroller (e.g., NodeMCU ESP8266 / ESP32 / Arduino)
- Breadboard & Jumper Wires
- Sensors/Buttons (for detecting box interaction)
- LEDs / Buzzers (for physical alerts)

**Software & Web:**
- **Frontend:** HTML, CSS, JavaScript
- **Backend:** C++ (Arduino IDE) / Python 
- **Networking:** Local WiFi Web Server (via Microcontroller)

---

## 🚀 Getting Started

To replicate this setup on your local network:

### Prerequisites
* Arduino IDE (or VS Code with PlatformIO)
* ESP8266/ESP32 board manager installed
* Necessary hardware components listed above

### Installation & Setup

1. **Clone the repository**
   ```sh
   git clone [https://github.com/manojrameshdev/Medicine_Remainder_System.git](https://github.com/manojrameshdev/Medicine_Remainder_System.git)
Open the hardware code
Navigate to the hardware folder and open the .ino or .cpp file in your Arduino IDE.

Configure WiFi Credentials
Update the code with your local WiFi SSID and PASSWORD.

C++
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
Flash the Microcontroller
Connect your board via USB and upload the code.

Access the Dashboard
Open the Serial Monitor to find the generated local IP address (e.g., 10.55.93.18), and type it into any web browser on the same network.

🔮 Future Enhancements
1. Add cloud database integration (like Firebase) for remote monitoring.

2. Implement user authentication for secure access.

3. Add historical data logging to track adherence over weeks/months.

4. Integrate SMS or email push notifications.

📝 License
Distributed under the MIT License. See LICENSE for more information.

📬 Contact
Manoj Ramesh - GitHub: @manojrameshdev
Repository: Medicine_Remainder_System

Repository: Medicine_Remainder_System

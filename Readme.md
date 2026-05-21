# 💊 Smart Medicine Reminder System using ESP32

![ESP32](https://img.shields.io/badge/ESP32-IoT-blue)
![Arduino](https://img.shields.io/badge/Arduino-C++-green)
![Status](https://img.shields.io/badge/Status-Working-brightgreen)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## 🚀 Overview

The **Smart Medicine Reminder System** is an IoT-based embedded system built using the ESP32 microcontroller. It helps users take medicines on time by providing **audio-visual alerts** and allows real-time monitoring through a **web interface**.

This system combines **hardware alerts (LED + buzzer)** with a **software dashboard**, ensuring reliability and ease of use.

---

## 🎯 Objectives

- Ensure timely medication intake  
- Provide a simple user interface using buttons  
- Display real-time information using LCD  
- Enable remote monitoring via web interface  
- Build a standalone embedded system  

---

## 🎥 Demo Preview

![Demo](images/demo.gif)

---

## 📷 Project Gallery

### 🔌 Circuit Diagram
![Circuit Diagram](images/circuit_diagram.png)

### 🧪 Hardware Setup
![Setup](images/demo.jpg)

### 📱 Web Interface Output
![Web UI](images/web_output.jpg)

---

## ⚙️ Features

- ⏰ Real-time tracking using DS3231 RTC  
- 📺 16x2 LCD display (I2C interface)  
- 🔴🔵🟢 Three LED indicators for medicine boxes  
- 🔔 Buzzer alert for reminder notification  
- 🎛️ Push buttons for user input (SET, INC, OK)  
- 🌐 Web dashboard (view-only monitoring)  
- 🔋 Works independently without PC  

---

## 🔧 Technologies Used

- **Hardware:**
  - ESP32 Microcontroller
  - DS3231 RTC Module
  - 16x2 LCD Display (I2C)
  - LEDs, Buzzer, Push Buttons

- **Software:**
  - Arduino IDE
  - Embedded C++
  - WiFi (IoT communication)
  - I2C Protocol

---

## 🧠 System Working

1. User enters **set mode** using SET button  
2. Alarm times are configured using INC and OK buttons  
3. RTC continuously tracks current time  
4. When alarm time matches:
   - Corresponding LED turns ON  
   - Buzzer is activated  
5. User presses OK button:
   - Marks medicine as **Taken**  
   - Stops buzzer  
6. Status updates:
   - On LCD display  
   - On web dashboard  

---

## 🔌 Components Used

- ESP32 Dev Board  
- DS3231 RTC Module  
- 16x2 LCD (I2C)  
- LEDs (Red, Blue, Green)  
- Active Buzzer  
- Push Buttons (3)  
- Resistors (220Ω)  
- Breadboard  
- Jumper Wires  
- USB Power Supply  

---

## 🏗️ Project Structure

```text
Medicine_Reminder_System/
│
├── code/
│   └── esp32_medicine_reminder.ino
│
├── images/
│   ├── circuit_diagram.png
│   ├── demo.jpg
│   ├── demo.gif
│   └── web_output.jpg
│
├── docs/
│
├── components.txt
└── README.md
🌐 Web Interface

The web dashboard provides real-time monitoring of:

Current Time
Medicine Status:
✅ Taken
❌ Not Taken

💡 The dashboard refreshes automatically every 2 seconds.

👉 Access it via ESP32 IP address in browser

🔥 Key Highlights
Standalone embedded system
Real-time alert mechanism
IoT-based monitoring
Efficient use of I2C communication
Simple and user-friendly interface
⚠️ Limitations
No data storage (history not saved)
Requires WiFi for web interface
Manual interaction needed for confirmation
🚀 Future Improvements
❗ Missed dose detection system
📊 Data logging (history tracking)
📱 Mobile app integration
🔔 Notification alerts (SMS/App)
☁️ Cloud integration
👨‍💻 Author

Manoj R

⭐ Support

If you like this project, consider giving it a ⭐ on GitHub!

📌 Conclusion

This project demonstrates the integration of embedded systems and IoT to solve a real-world problem. It highlights the use of ESP32 for real-time applications and provides a foundation for further development in smart healthcare systems.
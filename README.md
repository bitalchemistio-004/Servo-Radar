# Servo-Radar
An ESP32-based ultrasonic sentry radar that continuously sweeps an area, locks onto targets within 15cm, and triggers a synchronized visual (LED) and audio (passive buzzer) alarm.
# ESP32 Sentry Radar System 📡

An autonomous radar system built with an ESP32 that sweeps an area using an ultrasonic sensor. When an object is detected within a 15 cm range, the system enters "Sentry Mode"—stopping the servo to lock onto the target while triggering a passive buzzer and an LED alert. 

Once the target leaves the detection zone, the alarms turn off, and the radar automatically resumes its sweep.

## ✨ Features
* **Active Target Lock:** The servo halts and maintains its position on the target until the object moves out of range.
* **Smart Audio Handling:** Utilizes a state-tracker to drive a passive buzzer using the `tone()` function without crashing the ESP32 hardware timers.
* **Visual Indication:** An LED illuminates instantly upon target lock.
* **Safe Servo Sweeping:** Built-in clamping logic prevents the servo from attempting to sweep out-of-bounds (0°-180°), protecting the motor from grinding or drawing excess current.

## 🛠️ Hardware Required
* 1x ESP32 Development Board
* 1x HC-SR04 Ultrasonic Sensor
* 1x Servo Motor (e.g., SG90)
* 1x Passive Buzzer
* 1x LED (Any color)
* 1x Resistor (220Ω - 1kΩ for the LED)
* Breadboard & Jumper Wires

## 🔌 Wiring & Pinout

| Component | ESP32 Pin | Notes |
| :--- | :--- | :--- |
| **Ultrasonic TRIG** | GPIO 32 | Output |
| **Ultrasonic ECHO** | GPIO 33 | Input |
| **Servo Signal** | GPIO 14 | Powered via 3V3 or 5V |
| **Passive Buzzer** | GPIO 27 | Other leg to GND |
| **LED Anode (+)** | GPIO 26 | Connected via Resistor |
| **LED Cathode (-)**| GND | |

## 💻 Software & Libraries
This code requires the following library to properly drive the servo motor using the ESP32's PWM timers:
* **ESP32Servo** by Kevin Harrington, John K. Bennett (Install via the Arduino IDE Library Manager).

## 🚀 How to Install and Run
1. Wire up the hardware according to the pinout table above.
2. Open the `.ino` file in the Arduino IDE.
3. Go to **Sketch > Include Library > Manage Libraries**, search for `ESP32Servo`, and install it.
4. Select your ESP32 board and COM port from the **Tools** menu.
5. Click **Upload**.
6. Open the **Serial Monitor** (set to `115200` baud) to view real-time distance and lock-on data.

## 📝 Future Improvements
* Build an accompanying web dashboard using ESP32 WebSockets to view the radar sweeps remotely.
* Add an adjustable potentiometer to control the target detection range on the fly without reprogramming.

# Smart-Exam-Hall-Monitoring-and-Management-System
An LPC2148-based embedded system that automates examination timing, temperature monitoring, secure configuration, and real-time alerts for efficient exam hall management.
## Project Overview
The Smart Exam Hall Monitoring and Management System is an embedded solution designed to improve the efficiency and accuracy of examination hall management. The system uses the LPC2148 microcontroller to integrate an RTC, 16×2 LCD, 4×4 matrix keypad, LM35 temperature sensor, multiplexed 7-segment displays, LEDs, buzzer, and external interrupts.The LCD displays the current date, time, and room temperature, while the keypad allows the invigilator to securely configure the RTC, exam start time, and examination duration. Once the exam starts, the system automatically records the start time and runs a countdown displayed on the 7-segment displays. Green, yellow, and red LEDs indicate the remaining examination time, while a buzzer signals completion. The system also provides pause/resume functionality and automatically records the exam end time, reducing manual timing errors and simplifying examination monitoring.
## Features
* **Real-Time Clock** — Displays the current date and time.
* **Exam Countdown** — Tracks the remaining examination time.
* **Exam Configuration** — Sets the exam start time and duration.
* **Temperature Monitoring** — Monitors room temperature using LM35.
* **Secure Access** — Protects configuration settings with a password.
* **Time Display** — Shows remaining time on dual 7-segment displays.
* **Status Indication** — Provides Green, Yellow, and Red LED alerts.
* **Pause / Resume** — Controls the countdown during interruptions.
* **Exam Completion Alert** — Activates the buzzer when the exam ends.
* **Automatic Time Logging** — Records exam start and end times.
* **Interrupt-Based Control** — Enables quick configuration and timer control.
## Hardware Components
| Component              | Purpose                                       |
| ---------------------- | --------------------------------------------- |
| **LPC2148**            | Main controller for the complete system       |
| **RTC**                | Provides real-time date and time              |
| **16×2 LCD**           | Displays time, temperature, and system status |
| **4×4 Matrix Keypad**  | Used for password and exam configuration      |
| **7-Segment Displays** | Displays the remaining exam time              |
| **LM35 Sensor**        | Measures room temperature                     |
| **LEDs**               | Indicates exam time status                    |
| **Buzzer**             | Alerts when the examination ends              |
| **Switches**           | Used for interrupt-based control              |
| **USB-UART / DB-9**    | Used for programming and communication        |
## Block Diagram
<img width="1536" height="1024" alt="block-diagram png" src="https://github.com/user-attachments/assets/e19cdee9-f8de-46c8-992d-24a9c690f4c8" /> 

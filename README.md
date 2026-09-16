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
<img width="1536" height="1024" alt="block diagram png" src="https://github.com/user-attachments/assets/62628c03-1505-48e5-b991-47292409dfbd" />

## Pin Configuration

| Signal / Component | LPC2148 Pin(s) | Description |
|---|---|---|
| LCD Data | P0.8 – P0.15 | 8-bit data |
| LCD RS / EN | P0.16 / P0.17 | LCD control |
| 4×4 Keypad | P1.16 – P1.23 | 4×4 key input |
| 7-Segment Data | P1.24 – P1.31 | Segment data |
| 7-Segment Select | P0.20 / P0.21 | Digit 1 / Digit 2 |
| Status LEDs | P0.2 / P0.3 / P0.4 | Green / Yellow / Red |
| Pause LED | P0.25 | Pause indication |
| Buzzer | P0.23 | Final-stage alert |
| LM35 | P0.28 | Temperature input |
| Interrupts | P0.1 / P0.7 | Admin / Pause-Resume |
## System Architecture

```text
├── main_pro.c              # Main program and initialization
├── interrupt_p.c/h         # EINT0/EINT1 interrupt handling
├── rtc_mpt.c/h             # RTC operation
├── rtc_edit.c              # RTC configuration
├── kpm_mp.c/h              # 4×4 keypad handling
├── lcd_t.c/h               # LCD driver
├── adc_mpt.c/h             # ADC driver
├── lm35_mpt.c/h            # LM35 temperature measurement
├── led_mpt.c/h             # LED status control
├── buzzer_mpt.c/h          # Buzzer control
├── 7seg_mpt.c/h            # 7-segment display driver
├── timer.c/h               # Examination countdown timer
├── delay.c/h               # Delay functions
└── types_t.h, defines.h    # Common definitions
```
## System Working

The Smart Exam Hall Monitoring and Management System operates as follows:

1. **System Initialization**

   * The LPC2148 microcontroller initializes the RTC, LCD, keypad, ADC, LM35, LEDs, buzzer, 7-segment displays, timer, and interrupts.

2. **Normal Display**

   * The LCD continuously displays the current **RTC time** and **room temperature** measured using the LM35 sensor.

3. **Exam Configuration**

   * The administrator presses **EINT0** to enter the protected configuration mode.
   * A password is requested through the keypad.
   * After successful authentication, the administrator can configure the **RTC time, exam start time, and exam duration** using the keypad.

4. **Exam Start**

   * When the configured exam start time is reached, the system automatically starts the examination countdown.
   * The exam start time is recorded using the RTC.

5. **Countdown and Display**

   * The Timer0 module controls the examination countdown.
   * The remaining examination time is displayed on the **two multiplexed 7-segment displays**.
   * The LCD continues to display the RTC time and room temperature.

6. **Visual Alerts**

   * **Green LED:** More than 10 minutes remaining.
   * **Yellow LED:** Final 10 minutes.
   * **Red LED:** Final 1 minute.

7. **Pause and Resume**

   * The administrator can use **EINT1** to pause the examination countdown.
   * Pressing EINT1 again resumes the countdown.

8. **Temperature Monitoring**

   * The LM35 continuously measures the room temperature through the ADC.
   * The converted temperature value is displayed on the LCD.

9. **Exam Completion**

   * When the countdown reaches **zero**, the buzzer is activated to indicate the end of the examination.
   * The red LED indicates the final exam status.
   * The examination end time is recorded using the RTC.

10. **System Continuation**

    * After the examination ends, the system returns to its normal monitoring state and continues displaying the RTC time and temperature.
## Project Workflow

```text
                    ┌──────────────────────┐
                    │   System Power ON    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ System Initialization│
                    │  LPC2148 Peripherals │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Display RTC Time   │
                    │  & Room Temperature  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      EINT0 Pressed   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Password Check     │
                    └──────────┬───────────┘
                               │
                       ┌───────┴───────┐
                       │               │
                    Invalid          Valid
                       │               │
                       ▼               ▼
                ┌────────────┐  ┌─────────────────────┐
                │   Return   │  │ Configure RTC /     │
                │ to Normal  │  │ Start Time / Duration│
                └────────────┘  └──────────┬──────────┘
                                           │
                                           ▼
                                ┌──────────────────────┐
                                │  Wait for Exam Start  │
                                │       Time            │
                                └──────────┬───────────┘
                                           │
                                           ▼
                                ┌──────────────────────┐
                                │     Start Exam        │
                                │ Record Start Time     │
                                └──────────┬───────────┘
                                           │
                                           ▼
                                ┌──────────────────────┐
                                │   Start Countdown     │
                                │     Timer0            │
                                └──────────┬───────────┘
                                           │
                    ┌──────────────────────┼──────────────────────┐
                    │                      │                      │
                    ▼                      ▼                      ▼
             ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
             │ LCD Display  │     │ 7-Segment    │     │ LM35 + ADC   │
             │ RTC + Temp   │     │ Remaining    │     │ Temperature  │
             └──────────────┘     │ Time         │     └──────────────┘
                                  └──────────────┘
                                           │
                                           ▼
                                ┌──────────────────────┐
                                │   LED Status Alert    │
                                │ Green / Yellow / Red  │
                                └──────────┬───────────┘
                                           │
                                           ▼
                                ┌──────────────────────┐
                                │      EINT1 Pressed?   │
                                └──────────┬───────────┘
                                           │
                                     Yes   │
                                           ▼
                                ┌──────────────────────┐
                                │   Pause / Resume     │
                                │     Countdown        │
                                └──────────┬───────────┘
                                           │
                                           ▼
                                ┌──────────────────────┐
                                │   Countdown = Zero?  │
                                └──────────┬───────────┘
                                           │
                                           ▼
                                ┌──────────────────────┐
                                │    Activate Buzzer   │
                                │   Record End Time    │
                                └──────────┬───────────┘
                                           │
                                           ▼
                                ┌──────────────────────┐
                                │ Return to Monitoring │
                                │    State             │
                                └──────────────────────┘
``` 
## Development Tools and Environment

* **Microcontroller:** LPC2148 ARM7
* **Programming Language:** Embedded C
* **IDE:** Keil µVision
* **Programming Tool:** Flash Magic
* **Compiler:** ARM Compiler
* **Debugging:** Serial communication through USB-UART / DB-9
* **Development Platform:** Embedded Systems Hardware Setup
## Future Scope

* Integration of **IoT connectivity** for remote monitoring of examination halls.
* Addition of **centralized monitoring** for managing multiple examination halls.
* Automatic **data logging and report generation** for exam start and end times.
* Integration of **wireless communication** for real-time status updates.
* Integration of additional **environmental sensors** for monitoring hall conditions.
* Enhancement of the system with **automated attendance and student monitoring**.
* Use of advanced security features for improved **exam hall management and monitoring**.
## Developed By

Bhonagiri Vedha sri

**Project**:Smart Exam Hall Monitoring and Management System.

Laboratory Activity 1: Timers, Interrupts, and Task Scheduling

Course: BCA143 Firmware Programming  
Student: Macasero, Princess Nashema  
Date: June 13, 2026  

Project Description
This project explores timer interrupts and task scheduling on the RT-Spark Development Board. Two hardware timers are configured to fire at different intervals, controlling LEDs and triggering foreground tasks. A button-triggered external interrupt is also incorporated to illustrate event-driven scheduling behavior.

Hardware
- RT-Thread RT-Spark Development Board (STM32F407ZGT6)
- LEDs: PF11 (Red), PF12 (Blue)
- User Button: PA0
- Debug Pin: PE0

Features
- TIM2: 1 Hz periodic interrupt (high priority)
- TIM3: 2 Hz periodic interrupt (medium priority)
- External interrupt on button press
- Foreground/background system architecture
- Timing measurement and analysis

Timing Measurements

Parameter	Definition	Measured Value	Units
TRelease(TIM2)	Timer interrupt occurs	1.0	seconds
TLatency(Task A)	Delay before Task A starts	24.94	µs
TISR(TIM2)	Time in ISR	4.31	µs
TTask(Task A)	Task A execution time	50	ms
TResponse(Task A)	Total response time	50.02443	ms

Sequence Diagram
![Sequence Diagram](sequence_diagram.png)

Build Instructions
1. Open project in STM32CubeIDE
2. Build: Project → Build All
3. Connect RT-Spark via USB
4. Upload: Run → Debug or Run

 Analysis
Maximum latency for Task A** is 70ms — occurs when both Task A (50ms) and Task B (20ms) are executing simultaneously when the interrupt fires.
2. Effect on TLatency — if Task B is running when TIM2 fires, Task A must wait until Task B finishes, increasing latency by up to 20ms.
3. Worst-case TResponse** is 120ms — computed as 70ms waiting time plus 50ms Task A execution time.
4. With preemptive scheduler** — higher priority tasks run immediately when triggered, reducing latency to near zero.

References
1. Castor, P. R. P. (2025). Software Design Basics [Lecture 2]. BCA143 Firmware Programming, MSU-IIT.
2. STMicroelectronics. (2024). STM32F4 HAL Driver User Manual.
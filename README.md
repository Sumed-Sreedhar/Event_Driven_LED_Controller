# Event-Driven LED Controller (STM32)

**Status:** Completed and tested on hardware | STM32F446RE

---

## What It Does
An **event-driven LED controller** designed to demonstrate how **external interrupts and timers** can be used to build responsive, non-blocking embedded systems.

- Button presses change the **system mode**
- LED behavior is executed via a **hardware timer**
- No polling loops, no blocking delays
- All LED control is centralized and deterministic

This project represents the transition from basic GPIO handling to **explicit state-based, event-driven design**.

---

## System Architecture
- **MCU:** STM32F446RE (Nucleo)
- **Input:** Push button (GPIO + EXTI)
- **Output:** LED (GPIO)
- **Timing:** Hardware timer interrupt
- **Debug:** On-board ST-Link debugger

---

## Operating States
The system operates in the following modes, selected via button press:

- **OFF** — LED remains off  
- **ON** — LED remains on  
- **SLOW BLINK** — LED toggles at a slow, fixed interval  
- **FAST BLINK** — LED toggles at a faster interval  

Each button press cycles the system to the next mode.

---

## System Behavior
- Button presses are captured using **EXTI interrupts**
- EXTI callbacks update the **current system state only**
- LED behavior is executed inside a **timer ISR**
- The timer ISR reads the active state and applies the correct LED behavior
- LED writes occur from a **single control point**

This avoids duplicated logic and ensures predictable timing behavior.

---

## Core Concepts Demonstrated
- Event-driven input handling using EXTI  
- Timer-based output control  
- Explicit state representation for system behavior  
- Separation of event detection and action execution  
- Non-blocking firmware design  

---

## Design Intent
The goal of this project was to:

- Eliminate polling and delay-based control  
- Understand how events drive state transitions  
- Learn how timers act as time bases rather than delays  
- Enforce ISR discipline and responsibility separation  
- Build scalable logic using explicit system states  

---

## What I Learned
- Why EXTI ISRs should be minimal and non-blocking  
- How timers safely drive time-based behavior  
- How explicit states simplify embedded logic  
- How event-driven designs scale better than polling-based systems  
- How to structure STM32 HAL projects cleanly  

---

## Limitations
- Fixed number of operating modes  
- No automatic mode timeout  
- No debouncing logic  

These limitations were intentional and later addressed in more advanced projects.

---

## Follow-Up Work
This project directly led to:
- Interrupt-Driven LED Pattern Controller  
- Hierarchical state-machine designs  
- More complex timer-driven behavior systems  

---

## Tools & Environment
- STM32CubeIDE  
- STM32 HAL  
- Linux development environment  
- Git & GitHub for version control  

---

## Repository Structure
```
Event_Driven_LED_Controller/
├── Core/
│   ├── Src/
│   └── Inc/
├── README.md
└── ...
```

---

## Status
Completed and tested on hardware.

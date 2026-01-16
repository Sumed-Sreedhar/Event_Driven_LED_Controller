# GPIO Status Controller (STM32)

**Status:** Completed and hardware-validated | STM32F446RE

---

## What It Does
A **state-based GPIO controller** demonstrating event-driven embedded design using **external interrupts (EXTI)** and **timer interrupts**.

- Button inputs trigger **state transitions**
- LED behavior is driven **exclusively by a timer ISR**
- No blocking delays, no polling loops
- Single point of output control for deterministic behavior

This project was built to move beyond naïve polling-based designs and understand how real embedded systems react to events.

---

## System Architecture
- **MCU:** STM32F446RE (Nucleo)
- **Inputs:** Push button(s) via GPIO + EXTI
- **Outputs:** LED(s)
- **Timing:** Hardware timer interrupt
- **Debug:** On-board ST-Link

---

## Operating Modes
The system operates in four distinct modes:

- **OFF** — LED permanently off  
- **ON** — LED permanently on  
- **SLOW BLINK** — LED toggles at a fixed slow interval  
- **FAST BLINK** — LED toggles at a faster interval  

### Control Flow
- Button presses **do not** control the LED directly  
- EXTI ISRs only update the **system state**
- The timer ISR reads the current state and applies the correct LED behavior

This enforces strict separation between **event detection** and **action execution**.

---

## Key Engineering Decisions

### 1. Event-Driven Over Polling (Core Design Choice)
**Problem:** Polling-based GPIO designs waste CPU time and scale poorly as complexity increases.

**Solution:** Used EXTI interrupts to capture button events and timers as the sole time base.

**Takeaway:** Events should modify state; time-driven logic should act on state.

---

### 2. Single Point of Hardware Control
**Problem:** Driving outputs from multiple ISRs leads to race conditions and unpredictable behavior.

**Solution:** All LED control is centralized in the timer ISR.

**Takeaway:** Each peripheral should have a clear owner to ensure deterministic execution.

---

### 3. Minimal ISR Design
**Problem:** Heavy logic inside ISRs causes latency and hard-to-debug issues.

**Solution:** EXTI callbacks only update state variables; no delays, no GPIO writes.

**Takeaway:** ISRs should be short, predictable, and side-effect–limited.

---

## What I Learned
- Why EXTI ISRs must be minimal and non-blocking  
- How timers act as **time bases**, not delay mechanisms  
- How state machines simplify embedded logic  
- The importance of peripheral ownership  
- How to structure STM32 HAL projects cleanly  

---

## Limitations
- No automatic mode timeout  
- Debouncing handled simplistically  
- Designed for clarity, not feature density  

These limitations were intentional and addressed in follow-up projects.

---

## If I Extended This Project
1. Add **mode timeout logic** (automatic state decay)  
2. Implement **timer-based debouncing**  
3. Support multiple outputs with shared state logic  
4. Reimplement using **register-level (bare-metal) code**  

---

## Tools & Environment
- STM32CubeIDE  
- STM32 HAL  
- Linux development environment  
- Git & GitHub for version control  

---

## Status
Completed and tested on hardware.

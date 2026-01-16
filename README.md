GPIO Status Controller (STM32)
Overview:

This project implements a GPIO-driven status controller on the STM32F446RE using an event-driven design.
Button inputs trigger state changes via EXTI interrupts, while a timer interrupt controls LED behavior based on the current system state.

The goal is to separate event detection from action execution, avoiding blocking delays and large conditional logic.

Hardware Used:

STM32F446RE (Nucleo)

Push button(s)

LED(s)

On-board debugger (ST-Link)

Core Concepts Demonstrated:

GPIO input/output configuration

External interrupts (EXTI)

Timer interrupts

Event-driven state machine design

Interrupt Service Routine (ISR) discipline

Single point of hardware control

System Behavior:-

The system operates in multiple modes:

OFF – LED off

ON – LED on

Slow Blink – LED toggles at a slow rate

Fast Blink – LED toggles at a faster rate

Button presses do not directly control the LED.
They only update the system state.
The timer ISR reads the state and applies the correct LED behavior.

This ensures:

Clean separation of responsibilities

Predictable timing behavior

Scalable logic without nested if/else blocks

Design Intent:-

This project was intentionally designed to:

Avoid polling-based delays

Prevent logic duplication across ISRs

Model how real embedded systems react to events rather than loops

The LED is controlled from one place only, enforcing deterministic behavior.

What I Learned:

Why EXTI ISRs should be minimal and non-blocking

How timers act as time bases, not delays

How state machines simplify embedded logic

The importance of ownership over peripherals

How to structure HAL-based projects cleanly

Possible Improvements:

Add mode timeout logic (automatic state decay)

Add debouncing using timer-based validation

Extend to multiple LEDs or outputs

Convert to bare-metal (register-level) implementation

Tools & Environment:

STM32CubeIDE

STM32 HAL

Linux (development environment)

Git & GitHub for version control

Status:
Completed and functional on hardware.

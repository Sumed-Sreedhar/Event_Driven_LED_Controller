GPIO Status Controller (STM32)
Overview

This project implements a GPIO-driven status controller on the STM32F446RE using an event-driven design.
Button inputs trigger state changes via EXTI interrupts, while a timer interrupt controls LED behavior based on the current system state.

The goal is to separate event detection from action execution, avoiding blocking delays and large conditional logic.

Hardware Used

STM32F446RE (Nucleo)

Push button(s)

LED(s)

On-board debugger (ST-Link)

Core Concepts Demonstrated

GPIO input/output configuration

External interrupts (EXTI)

Git & GitHub for version control

Status: Completed and functional on hardware.

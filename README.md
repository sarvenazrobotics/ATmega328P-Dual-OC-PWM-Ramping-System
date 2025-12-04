# Dual PWM LED Brightness Controller

A bare-metal embedded project for the **ATmega328P** that demonstrates hardware PWM generation and timer-based brightness ramping for LEDs.

## Features
- Dual-channel non-inverted **Fast PWM** output (8-bit) using **Timer0**
  - OC0A → PD6
  - OC0B → PD5
- Smooth **brightness ramping** on OC0B (increases every second)
- Timing reference via **Timer2 in CTC mode** (planned for future tasks like multiplexing)

##  Hardware Setup
- **Microcontroller**: ATmega328P (e.g., Arduino Uno, bare chip)
- **LEDs**: Connected to **PD5** and **PD6** (with current-limiting resistors)
- **Clock**: Assumes 16 MHz external crystal (adjust `F_CPU` if different)

## Files
- `main.c` – Main source code (PWM + timer setup)
- `Makefile` – (Optional) for compiling with avr-gcc

##  Notes
- Uses **Timer0** for PWM → avoid `delay_ms()` implementations that rely on Timer0 (may cause timing conflicts).
- Timer2 is configured for CTC mode but currently unused beyond setup—can be extended for display multiplexing (e.g., 7-segment).

##  Build & Flash
```bash
avr-gcc -mmcu=atmega328p -Os -o main.elf main.c
avr-objcopy -O ihex main.elf main.hex
avrdude -p m328p -c <programmer> -U flash:w:main.hex

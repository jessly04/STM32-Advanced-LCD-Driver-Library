# STM32-Advanced-LCD-Driver-Library
This repository contains a full-custom hardware abstraction layer (HAL) designed to interface an STM32F030 R8T6 microcontroller with a standard 16x2 character LCD. The project demonstrates advanced embedded C concepts, including manual register configuration, pointer-based string manipulation, and real-time data formatting.
### Key Technical Features
- **Cross-port Data Bus:** Engineered a 4-bit data bus that spans across GPIO Ports A, B, and C, requiring precise bit-masking to maintain data integrity across non-sequential pins
- **Data Visualization API** Implemented LCDSendAnInteger() and LCDSendAFloat() functions using sprintf and snprintf to render dynamic sensor data
- **Coordinate Mapping:** Developed an LCDSetCursorPosition(x, y) function to manage the LCD's internal DDRAM (Display Data RAM) addresses, allowing for precise character placement (Line1: 0x00, Line 2: 0x40)
- **Low-Level Hardware Control:** Manually configured the STM32's MODER (Mode Register), OTYPER (Output Type Register), and OSPEEDR (Output Speed Register) to bypass the standard HAL (Hardware Abstraction Layer) and optimize peripheral performance
### Hardware
- **Microcontroller**: STM32F030 R8T6
- **Programmer:** ST-Link V2
- **Signal Conditioning:** ULN2003
- **Output:** 16x2 Character LCD
### Challenge & Solution
Because the STM32 operates at 3.3V and the LCD operates at 5V, we utilized ULN2003 to step up the voltage. We implemented a software inversion layer within LCD_HIGH() and LCD_LOW() and swapped the BSRR (Bit Set/Reset Register) logic in the driver. We ensured that the high-level application code remains intuitive while the hardware signals are correctly translated for the inverted hardware
### Project Structure
- LCD.c / LCD.h: The core driver library that contains the initialization, timing pulses, and data transfer logic
- main.c: Demonstration code that includes the "Moving X" experiment and real-time float rendering
- GPIO_Init(): Manual configuration of the ARM Cortex-M0 peripheral clock (RCC) and GPIO modes
**Project Collaboration**
This project was co-developed by Jessica Ly and Daniel Meija Mendez.We worked together across the full stack, including hardware interfacing, register-level C programming, and system debugging.


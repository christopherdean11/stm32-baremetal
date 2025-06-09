## Prerequisites Setup

### Tools
- **STM32 development board**
- **arm-none-eabi-gcc toolchain** (GNU ARM Embedded Toolchain)
- **VS Code** with C/C++ extension
- **OpenOCD** or **ST-Link utilities** for programming/debugging
- **Make** for build automation
- **Git** for version control

### Initial Setup Steps
1. Install the ARM GCC toolchain from ARM's official site
2. Install OpenOCD for programming/debugging
3. Set up VS Code with the C/C++ extension
4. Clone or download STM32 reference manual and datasheet for your specific chip

## Activity 1: Know Your Board
- **Exercise:** Identify your STM32 chip model (STM32F103, STM32F411, etc.)
- **Research:** Download the reference manual and datasheet for your specific chip
- **Practice:** Locate the LED pin on your board's schematic
- **Deliverable:** Document which GPIO port and pin your LED is connected to


## Deliverables
### Tools
* arm toolchain
  - https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads
  - or on mac: `brew install --cask gcc-arm-embedded`

* OpenOCD
  - Windows: https://github.com/openocd-org/openocd/releases
  - Mac: `brew install open-ocd`,


### Chip Documentation
* Chip: `STM32F334R8T6`
* Nucleo Board Manual: https://www.st.com/resource/en/user_manual/dm00105823.pdf
* MCU Datasheet: https://www.st.com/resource/en/datasheet/stm32f334r8.pdf
* MCU Reference Manual: https://www.st.com/resource/en/reference_manual/rm0364-stm32f334xx-advanced-armbased-32bit-mcus-stmicroelectronics.pdf


### Notes
* User LED `LD2` for this nulceo board is connected to GPIO `PA5`


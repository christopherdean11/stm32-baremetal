### Activity 2: Memory Map Deep Dive
- **Exercise:** Study the STM32 memory map in the reference manual
- **Practice:** Understand the difference between Flash, SRAM, and peripheral memory regions
- **Research:** Find the base addresses for GPIO, RCC (Reset and Clock Control), and other peripherals
- **Deliverable:** Create a cheat sheet with key memory addresses for your chip


### Notes
#### Flash vs SRAM vs Peripherals
- Flash is non-volatile storage for the program and data
- SRAM is volatile memory
- Peripheral memory is memory mapped registers to control things like timers, DACs, ADCs, GPIO

#### Memory Map
Memory map in section 2.2.2 (pg 48), Table 1
* GPIOA =  `0x4800 0000` - `0x4800 03FF` -> 1k total - AHB2
* RCC = `0x4002 1000` - `0x4002 13FF` -> 1k total - AHB1
* SRAM = `0x2000 0000` - `0x2000 2FFF` -> 12k total
* System Memory = `0x1FFF D800` - `0x1FFF F7FF` -> 8k total
* Main Flash Memory = `0x0800 0000` - `0x800 FFFF` -> 64k total
* Main Flash/SRAM/System Memory Alias = `0x0000 0000` - `0x0000 FFFF` -> 64k total

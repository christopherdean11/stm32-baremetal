# Bare Metal STM32 Embedded C Learning Path

This learning plan will teach you embedded C programming from the ground up, starting with bare metal register manipulation and building to more complex projects.

 -from the Claude AI

## Prerequisites Setup

### Tools You'll Need
- **STM32 development board** (you have this!)
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

## Phase 1: Understanding the Hardware (Week 1)

### Activity 1: Know Your Board :white_check_mark:
- **Exercise:** Identify your STM32 chip model (STM32F103, STM32F411, etc.)
- **Research:** Download the reference manual and datasheet for your specific chip
- **Practice:** Locate the LED pin on your board's schematic
- **Deliverable:** Document which GPIO port and pin your LED is connected to

### Activity 2: Memory Map Deep Dive :white_check_mark:
- **Exercise:** Study the STM32 memory map in the reference manual
- **Practice:** Understand the difference between Flash, SRAM, and peripheral memory regions
- **Research:** Find the base addresses for GPIO, RCC (Reset and Clock Control), and other peripherals
- **Deliverable:** Create a cheat sheet with key memory addresses for your chip

### Activity 3: Register-Level Understanding
- **Exercise:** Read about GPIO registers (MODER, ODR, IDR, etc.) in the reference manual
- **Practice:** Understand how to configure pins as input/output using register bits
- **Research:** Learn about the RCC registers needed to enable peripheral clocks
- **Deliverable:** Hand-draw a diagram showing how to configure your LED pin

## Phase 2: First Bare Metal Program (Week 2)

### Activity 4: Minimal Startup Code
- **Exercise:** Write a minimal startup.s file in ARM assembly
- **Practice:** Understand the vector table and reset handler
- **Code:** Create a basic linker script for your STM32
- **Deliverable:** A working startup.s that can jump to your main() function

### Activity 5: LED Blink - Pure Register Manipulation
- **Exercise:** Write C code to blink LED using only register addresses
- **Practice:** Use volatile pointers to access memory-mapped registers
- **Debug:** Use a debugger to step through and verify register values
- **Deliverable:** A working LED blink program with no HAL/libraries

```c
// Example structure for your first program
#define RCC_BASE     0x40023800
#define GPIOA_BASE   0x40020000
#define RCC_AHB1ENR  *(volatile uint32_t *)(RCC_BASE + 0x30)
#define GPIOA_MODER  *(volatile uint32_t *)(GPIOA_BASE + 0x00)
#define GPIOA_ODR    *(volatile uint32_t *)(GPIOA_BASE + 0x14)

void main(void) {
    // Enable GPIOA clock
    RCC_AHB1ENR |= (1 << 0);
    
    // Configure PA5 as output
    GPIOA_MODER &= ~(3 << (5 * 2));
    GPIOA_MODER |= (1 << (5 * 2));
    
    while(1) {
        GPIOA_ODR |= (1 << 5);   // LED ON
        delay(1000000);
        GPIOA_ODR &= ~(1 << 5);  // LED OFF
        delay(1000000);
    }
}
```

### Activity 6: Build System Creation
- **Exercise:** Create a Makefile for your project
- **Practice:** Configure compiler flags, linker settings, and build rules
- **Setup:** Configure VS Code tasks for building and flashing
- **Deliverable:** A complete build system that compiles and flashes your code

## Phase 3: Intermediate Embedded Concepts (Weeks 3-4)

### Activity 7: Interrupts and Timers
- **Exercise:** Implement a timer-based LED blink using interrupts
- **Practice:** Configure NVIC (Nested Vector Interrupt Controller)
- **Research:** Understand interrupt priorities and handlers
- **Deliverable:** LED blink controlled by timer interrupt, not blocking delays

### Activity 8: UART Communication
- **Exercise:** Implement UART transmission from scratch
- **Practice:** Configure baud rate, data bits, stop bits using registers
- **Debug:** Send "Hello World" to a terminal program
- **Deliverable:** Bidirectional UART communication without HAL

### Activity 9: Button Input with Debouncing
- **Exercise:** Read button input using GPIO registers
- **Practice:** Implement software debouncing
- **Research:** Understand pull-up/pull-down resistors in code
- **Deliverable:** Button-controlled LED with proper debouncing

## Phase 4: Advanced Topics (Weeks 5-6)

### Activity 10: ADC (Analog-to-Digital Converter)
- **Exercise:** Configure ADC to read analog values
- **Practice:** Implement polling and interrupt-based ADC reading
- **Project:** Create a simple voltmeter displaying values over UART
- **Deliverable:** ADC-controlled LED brightness

### Activity 11: PWM (Pulse Width Modulation)
- **Exercise:** Configure timer for PWM output
- **Practice:** Control LED brightness with PWM
- **Research:** Understand timer modes and prescaler calculations
- **Deliverable:** Smooth LED breathing effect using PWM

### Activity 12: SPI Communication
- **Exercise:** Implement SPI master mode from scratch
- **Practice:** Communicate with an external device (like an OLED display)
- **Debug:** Use oscilloscope or logic analyzer to verify signals
- **Deliverable:** SPI communication with external peripheral

## Phase 5: Complete Projects (Weeks 7-8)

### Project 1: Digital Thermometer
- Use ADC to read temperature sensor
- Display temperature on UART terminal
- Implement temperature-based LED indicators
- Add button interface for Celsius/Fahrenheit switching

### Project 2: Simple Data Logger
- Read multiple sensors (temperature, light, etc.)
- Store data in internal Flash memory
- Implement UART commands to retrieve stored data
- Add real-time clock functionality

### Project 3: Motor Control System
- Implement PWM motor control
- Add encoder feedback reading
- Create simple PID control loop
- Interface with UART for control commands

## Essential Learning Resources

### Documentation (Critical!)
- **STM32 Reference Manual** - Your chip's specific manual
- **ARM Cortex-M Programming Manual** - Understanding the core
- **STM32 Datasheet** - Pin configurations and electrical characteristics

### Development Tools
- **arm-none-eabi-gcc** - The compiler toolchain
- **OpenOCD** - For programming and debugging
- **ST-Link Utility** - Alternative programming tool
- **PuTTY/Tera Term** - Serial terminal for UART communication

### Hardware Tools (Recommended)
- **Logic Analyzer** - For debugging digital signals
- **Oscilloscope** - For analog signal analysis
- **Multimeter** - Basic electrical measurements

## Key Learning Principles

### 1. Always Read the Manual
- Every register bit has a purpose
- Timing requirements are critical
- Electrical characteristics matter

### 2. Start Simple, Build Complexity
- Get one thing working before adding features
- Test each component individually
- Document your register configurations

### 3. Understand Before Abstracting
- Know what each register does
- Understand the hardware behavior
- Only create abstractions after mastering the basics

### 4. Debug Methodically
- Use the debugger to inspect register values
- Verify clock configurations first
- Check pin configurations before blaming code logic

## Common Beginner Mistakes to Avoid

1. **Forgetting to enable peripheral clocks** - Most common cause of "nothing works"
2. **Incorrect pin configuration** - Double-check MODER, PUPDR, and AFR registers
3. **Timing issues** - Not waiting for peripheral ready flags
4. **Interrupt configuration errors** - Forgetting to enable in NVIC
5. **Linker script problems** - Incorrect memory regions or stack placement

## Debugging Strategies

### Using the Debugger
- Set breakpoints in your code
- Inspect register values in real-time
- Step through code line by line
- Use memory viewer to check peripheral registers

### Hardware Debugging
- Use LED indicators for code flow
- Toggle GPIO pins to measure timing
- Use UART for debug output
- Verify power supply and connections

Remember: The "hard way" is actually the smart way. Understanding registers and hardware behavior will make you a much better embedded developer than relying on abstractions from day one!
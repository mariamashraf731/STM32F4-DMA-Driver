# ⚡ STM32F4 DMA Driver (Direct Memory Access)

![Platform](https://img.shields.io/badge/Hardware-STM32F401-blue)
![Language](https://img.shields.io/badge/Language-Embedded%20C-green)
![Peripheral](https://img.shields.io/badge/Driver-DMA-orange)
![IDE](https://img.shields.io/badge/Toolchain-STM32CubeIDE-red)

## 📌 Project Overview
This repository contains a **High-Performance DMA Driver** developed for the **STM32F401 Microcontroller**. The driver enables direct data transfer between memory and peripherals without CPU intervention, significantly optimizing system performance and reducing CPU load.

It demonstrates deep knowledge of the **AMBA Bus Matrix**, **Stream/Channel configuration**, and **Interrupt Handling** in ARM Cortex-M4 architectures.

## ⚙️ Key Features
* **Memory-to-Memory Transfer:** Efficient bulk data copying.
* **Peripheral-to-Memory:** (e.g., ADC data acquisition).
* **Memory-to-Peripheral:** (e.g., UART/SPI transmission).
* **Interrupt Management:** Handling `Transfer Complete`, `Half Transfer`, and `Transfer Error` interrupts.
* **Circular Mode Support:** Continuous data buffering for real-time signal processing.

## 🛠️ Technical Architecture
### DMA Controller Configuration
The driver configures the DMA streams based on the STM32F4 architecture:
* **Stream Selection:** Maps specific peripherals to DMA streams.
* **Priority Levels:** manages arbitration between multiple streams (Low, Medium, High, Very High).
* **FIFO vs. Direct Mode:** Configures data packing/unpacking and burst transfers.

### File Structure
* `Core/Src/DMA.c`: Core implementation of DMA initialization and IRQ handlers.
* `Core/Inc/DMA.h`: Configuration macros and function prototypes.
* `Core/Src/main.c`: Example application demonstrating data transfer.

## 🚀 Usage Example
```c
#include "DMA.h"

// Define source and destination buffers
uint32_t src_buffer[100];
uint32_t dest_buffer[100];

int main(void) {
    HAL_Init();
    
    // Initialize DMA for Mem-to-Mem transfer
    DMA_Config_t dmaConfig;
    dmaConfig.Direction = DMA_MEMORY_TO_MEMORY;
    dmaConfig.DataSize = DMA_DATA_32BIT;
    dmaConfig.Mode = DMA_NORMAL;
    
    DMA_Init(&dmaConfig);
    
    // Start Transfer
    DMA_Start((uint32_t)src_buffer, (uint32_t)dest_buffer, 100);
    
    while (1) {
        // CPU is free to do other tasks here!
    }
}
```
## 🔧 Hardware Requirements
* MCU: STM32F401CCU6 (Black Pill) or similar STM32F4 Discovery board.
* Debugger: ST-Link V2.

## 👨‍💻 Skills Demonstrated
* Bare-Metal Programming.
* System Optimization & Throughput Analysi
* ARM Cortex-M4 Architectur
* Peripheral Driver Developme
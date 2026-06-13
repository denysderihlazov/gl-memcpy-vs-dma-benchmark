# Bare Metal Training 02: Memcpy vs DMA Benchmark

This project investigates and compares the execution speed of CPU-driven memory copying using `memcpy()` against Direct Memory Access (DMA) memory-to-memory transfers on the STM32F407VGT6 microcontroller.

## Goal

The goal is to measure copy time for different buffer sizes from 4 bytes to 16384 bytes and determine when DMA becomes more efficient than `memcpy()`.

## Measurement Method

The benchmark uses the internal DWT cycle counter (`DWT->CYCCNT`) to measure execution time in CPU cycles.

DMA transfers are measured using polling instead of interrupts.  
This avoids interrupt handling overhead and provides more deterministic timing measurements for benchmarking.

UART output is used only after each measurement to export results in CSV format, so it does not affect measured copy time.

## Planned Test Methods

1. Standard `memcpy()` CPU-driven memory copy
2. DMA memory-to-memory transfer using HAL polling
3. Optional: DMA memory-to-memory transfer using low-level registers

## Hardware Setup

- MCU: STM32F407VGT6
- DMA configuration: Memory-to-Memory
- DMA data width: 8-bit / Byte
- Measurement: internal `DWT->CYCCNT` cycle counter
- External verification: Kingst LA2016 logic analyzer using GPIO pulse
- CSV export: UART after measurement

## Output Format

```csv
Size,Memcpy_Ticks,DMA_HAL_Ticks
4,...
8,...
16,...
...
16384,...
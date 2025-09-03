---
title: MicroMouse Programming Language
---

# Programming Language

Most MicroMouse robots are programmed in C or C++ because those are the most widely supported languages by MCUs. However, any other language that can be compiled to your MCU’s architecture can also work as long as you have a hardware API to control peripherals. 

Your MCU’s manufacturer will almost certainly provide a C API to control GPIO pins and other features of the MCU. C++ is essentially a superset of C, so it can call most C APIs without issue. Other languages may have an FFI that you can use to call the C API, or there might exist a community-supported port of the API (e.g. [stm32-rs](https://github.com/stm32-rs/stm32-rs) for Rust on STM32 boards). 

Some hardware might officially support languages other than C and C++ out of the box, but this is rare. One example of this is the Raspberry Pi Pico which supports MicroPython.


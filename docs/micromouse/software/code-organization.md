---
title: MicroMouse Code Structure & Organization
---

# Code Structure & Organization

Programming a MicroMouse is no easy task. It is essential that you stay organized and start coding your MicroMouse the right way before you run into problems. 

Code organization is important. Writing all your code in one file is not going to work well in the long term. Splitting your program into different subsystems is essential for you and others to follow and understand what your code is doing. In an OO language like C++, each subsystem should be its own class: "Drive", "Vision", "Navigation", etc. In non-OO languages like C, simply put these subsystem implementations into their own files. 

You will undoubtedly need to write drivers for your specific hardware components on your robot. The code for these should be abstracted away into their own classes/files and should not be placed within your subsystem code. This will make your code easier to follow and save you from having to refactor an entire subsystem if you decide to switch sensor types in the future. It will also make it easier to create multiple hardware implementations – good for desktop simulation or for running your code on a different robot. 

Depending on your MCU, your project structure may vary. For many MCUs (Arduinos), we recommend using [PlatformIO](https://platformio.org/) to simplify your build system and give your project some organization. PlatformIO also provides a simple way to write [Unit Tests](unit-testing.md). Do not plan on writing your entire MicroMouse code in the Arduino IDE – it was not made for doing this. 

For STM32, you should use the STM32 CubeIDE or CubeMX to set up your project.

If you would like to get more advanced and design your own build system, consider using CMake to build your MicroMouse code. See the [firmware for our PCB mouse](https://github.com/petelilley/micromouse/tree/main/firmware) for inspiration.


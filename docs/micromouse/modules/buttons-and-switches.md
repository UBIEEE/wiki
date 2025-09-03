---
title: MicroMouse Buttons and Switches Module
---

# Buttons and Switches

Every MicroMouse robot needs a way for its handler to interact with it in between runs at competitions. Your robot must have an easy way to start and stop a run, and it is also a good idea to provide a way to change its speed and search algorithm, and a way to reset the maze data in case of a crash.

!!! tip
    You can reuse other sensors on your robot to act like buttons.

    For example, many MicroMouse robots use their navigation IR sensors to detect a hand wave in front of them, signaling that they should start a run. This is a good way to start the maze navigation, since you will not risk accidentally moving the robot while trying to press a button.

    Additionally, some robots use their wheels as dials to cycle through speed or algorithm options using their encoders. This works best if your robot has a screen or an LED array to provide feedback.

Raspberry Pi Picos and some Arduinos come with a programmable built-in button, but you will almost always want to add more. 

Adding physical buttons or switches is relatively easy. There are 4 main types of electrical switches: SPST, SPDT, DPST, and DPDT. DPST and DPDT switches are essentially just two SPST or SPDT combined into one. Triple-Pole and greater switches also exist but are rare.

See the diagrams for each type of switch:

![Switches](../../assets/micromouse/switches-light-bg.png#only-light){ width=200 }
![Switches](../../assets/micromouse/switches-dark-bg.png#only-dark){ width=200 }

For Single-Pole Single-Throw (SPST) switches, connect A to VCC and connect B to your MCU.
If your MCU has an internal pull-down resistor, enable it in code. Otherwise, add a pull-down resistor between B and GND. In this configuration, the pin will read low when the button is not pressed, and high when it is pressed. Alternatively, you can connect A to GND and add a pull-up resistor between B and VCC if you prefer that the pin reads high when the button is not pressed.

Single-Pole Double-Throw (SPDT) switches are similar, but they do not require a pull-up or pull-down resistor. Simply connect A to VCC, B to GND, and C to your MCU. Check the switch's "default" position in the datasheet to determine whether the pin will read high or low when it is not pressed.

!!! tip
    Some MCUs allow you to configure a pin to trigger an interrupt when it changes state. This interrupt can be used to call a function in your code whenever the button is pressed or released.
    If your MCU does not support this, you can still check the pin in a loop and wait for it to change state for the same effect.


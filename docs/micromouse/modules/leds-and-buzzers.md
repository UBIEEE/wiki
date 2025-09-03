---
title: MicroMouse LEDs and Buzzers Module
---

# LEDs and Buzzers

Often it is helpful to know what your MicroMouse is thinking while it is driving around. Unless your MicroMouse has wireless capabilities, LEDs and/or a Buzzer are must-haves.

LEDs are nice because they look cool and can immediately let you know when something is happening. However, it is important not to add too many, since LEDs can draw a lot of current. Your power distribution system is going to limit how many you can add.

!!! tip
    One handy trick you can do for debugging: with multiple nearby LEDs, you can display an error code in binary. With 5 LEDs, you can display 31 different error codes ($2^{5}-1$). With 6, 63 ($2^{6}-1$). 

Buzzers are another helpful addition to your robot for debugging. 
Simple buzzers are controlled using a PWM signal with 50% duty cycle. Changing the frequency of the signal will change the audio frequency produced by the buzzer. For most low-quality buzzers, these frequencies will not directly correlate with each other, but you can spend the time to "tune" your buzzer by figuring out which PWM frequencies correspond to which notes. Once your buzzer is tuned, you can program your favorite songs into your firmware for your MicroMouse to play while it’s driving around!

<!-- TODO add a video of a cool song playing -->

These [Piezo Buzzers from Adafruit](https://www.adafruit.com/product/160) work well for MicroMouse robots.


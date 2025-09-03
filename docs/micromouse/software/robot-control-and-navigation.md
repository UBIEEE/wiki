---
title: MicroMouse Robot Control & Navigation Software
---

# Robot Control & Navigation

Maze navigation is probably the most complicated part of the MicroMouse program since it takes a lot of testing and fine-tuning.  

"Navigation" refers to the process of taking readings from sensors (wall sensors, motor encoders, IMU, etc.), then determining where the MicroMouse is in the maze and how to move. This process can be deceptively hard – just driving in a straight line for more than a few inches can be a considerabe challenge. 

## PID Control

!!! note
    While PID Controllers may have other applications on your robot besides navigation, I decided to put this section here because it is most commonly used for navigation tasks.

Wikipedia does a good job of explaining PID controllers and how they work:

!!! quote "[Wikipedia](https://en.wikipedia.org/wiki/Proportional%E2%80%93integral%E2%80%93derivative_controller)"
    A __proportional–integral–derivative controller__ (PID controller or three-term controller) is a feedback-based control loop mechanism commonly used to manage machines and processes that require continuous control and automatic adjustment. It is typically used in industrial control systems and various other applications where constant control through modulation is necessary without human intervention. The PID controller automatically compares the desired target value (setpoint or SP) with the actual value of the system (process variable or PV). The difference between these two values is called the _error value_, denoted as $e(t)$.

    It then applies corrective actions automatically to bring the PV to the same value as the SP using three methods: The proportional (P) component responds to the current error value by producing an output that is directly proportional to the magnitude of the error. This provides immediate correction based on how far the system is from the desired setpoint. The integral (I) component, in turn, considers the cumulative sum of past errors to address any residual steady-state errors that persist over time, eliminating lingering discrepancies. Lastly, the derivative (D) component predicts future error by assessing the rate of change of the error, which helps to mitigate overshoot and enhance system stability, particularly when the system undergoes rapid changes. The PID output signal can directly control actuators through voltage, current, or other modulation methods, depending on the application. 

???+ example "Simple P Controller Example"
    One application for a PID controller is to make a motor spin to a specific position. For this example, you can control a motor with a percent output (0 for stopped, 1.0 for full speed forward), and you have an encoder that will provide the position of the motor. 

    Your target position is $60$ degrees. This is your setpoint (SP). 

    Your motor's current position is $0$ degrees. This is your process variable (PV). 

    Your error $e(t) = \text{SP} – \text{PV} = 60$ degrees. 

    Feeding this error into a simple Proportional (P) controller with $K_p = 0.01$ will give you a motor output of $60 \times 0.01 = 0.6$. 

    A short amount of time later, check the new position and re-run the controller. The new position is $20$ degrees, so your error is now $40$. Your motor's new output is $40 \times 0.01 = 0.4$. Notice how the motor is slowing down as it approaches the setpoint.

    Continue this process and eventually the setpoint will be reached. 


Some applications for PID controllers on MicroMouse robots include:

- To control each drive motor's velocity or position (using Encoder readings)
- To control the robot's angular velocity when turning (using IMU and/or Encoder readings)
- To center the robot in between walls (using wall sensor readings)

### Tuning PID Controllers

Tuning PID controllers is the process of adjusting the P, I, and D values to get the desired behavior for your system.

!!! quote "[WPILib Docs](https://docs.wpilib.org/en/2020/docs/software/advanced-control/introduction/tuning-pid-controller.html)"
    These steps apply to position PID controllers. Velocity PID controllers typically don’t need $K_d$.

    1. Set $K_p$, $K_i$, and $K_d$ to zero.
    2. Increase $K_p$ until the output starts to oscillate around the setpoint.
    3. Increase $K_d$ as much as possible without introducing jittering in the system response.

    Plot the position setpoint, velocity setpoint, measured position, and measured velocity. The velocity setpoint can be obtained via numerical differentiation of the position setpoint (i.e. $v_{desired,k}=\frac{r_k-r_{k-1}}{\Delta t}$). Increase $K_p$ until the position tracks well, then increase $K_d$ until the velocity tracks well.

    If the controller settles at an output above or below the setpoint, one can increase $K_i$ such that the controller reaches the setpoint in a reasonable amount of time. However, a steady-state feedforward is strongly preferred over integral control (especially for PID control).

    !!! warning "Important"
        Adding an integral gain to the controller is an incorrect way to eliminate steady-state error. A better approach would be to tune it with an integrator added to the plant, but this requires a model. Since we are doing output-based rather than model-based control, our only option is to add an integrator to the controller.

    Beware that if $K_i$ is too large, integral windup can occur. Following a large change in setpoint, the integral term can accumulate an error larger than the maximal control input. As a result, the system overshoots and continues to increase until this accumulated error is unwound.

## Detecting Walls and Staying Centered in the Cell

Here are a few resources that may be helpful:

- [Peter Harrison - "Wall and Line Tracking for MicroMouse and Linefollowers" Presentation](https://youtu.be/22l6MrAwN-o?si=5YQR3eSrgfoJ3-JN)
- [Green - Calibration Strategy Tutorial](http://micromouseusa.com/?p=828)

## Navigation Styles

You will see two distinct styles of navigation done by MicroMouse robots: "start-and-stop" movement and "fluid" movement.

As you might expect, the easiest way to navigate the maze is to move forward one cell, stop, take measurements, then decide where to move next. This is a good starting point for most MicroMouse robots. This can still be complicated because you need error correction based on your wall sensor readings to prevent small errors from accumulating. Refer to the previous section on PID control for details about that.

Once you have established that your robot is capable of navigating the maze using the start-and-stop approach, consider implementing a navigation system to drive smoothly through the maze, making decisions while in motion. Despite how it may look, this approach is not much different than the previous one. The process is essentially the same except now there is no stopping. The tricky part is determining where to take readings from your sensors and when to start turning.

### Navigating Fast

After navigating the maze and determining the fastest path to the goal, your MicroMouse can optimize its movements to travel faster because now it knows exactly where to go.

A few things to do:

- Identify long straightaways in your desired path and calculate how much your robot should speed up during those sections.
- Determine how fast your robot can safely turn without crashing. You should increase your robot's turning radius to allow it to turn faster.
- Make sure that your robot can effectively center itself in the cell using its wall sensors, see the previous section for details. You will need a well-tuned system to travel fast without crashing.
- Use your robot's wall sensors to determine where it is based on presence of walls. When your sensors detect a wall or the absence of a wall, your robot can use the maze information it has previously gathered to help it determine how far it has traveled. This is good to supplement readings from your wheel encoders and other sensors.

#### Driving Diagonally

Check out this awesome presentation by Derek Hall about driving diagonally:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/Wh2HoS5W6Tc?si=BvnhB2J2pBntfu1I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


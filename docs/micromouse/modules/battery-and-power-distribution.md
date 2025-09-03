---
title: MicroMouse Battery and Power Distribution Module
---

# Battery and Power Distribution

Power distribution is a critical part of your MicroMouse design. The decisions you make here will dictate much of what your robot will look like as you move forward. 

## Picking a Battery

First you must select a battery to use. There are many different types of batteries, each with different strengths and weaknesses. Here is a list of some common battery chemistries that may be used for MicroMouse:

### Lithium Batteries

Lithium batteries come in two flavors: Lithium-Ion (Li-Ion) and Lithium Polymer (LiPo).

Lithium-Ion batteries use a liquid electrolyte and are usually rectangular or circular in shape. Li-Ion batteries have a high energy density and have long life spans.

Lithium Polymer batteries use solid or gel-like polymer electrolyte, which allows them to be made in all different shapes and sizes. LiPo batteries have a lower energy density than Li-Ion batteries but often have faster discharge rates.

Most MicroMouse robots use LiPo batteries.

???+ danger "Safety Warning"
    Lithium batteries can be very dangerous if used improperly and become a huge fire hazard if any of the following happens to them:

    - Punctured/damaged
    - Terminals shorted
    - Charged too fast/incorrectly

    Lithium battery fires are self-contained, meaning that they do not require any external fuel to continue burning. This means that Lithium battery fires are extremely difficult to put out. A normal everyday fire extinguisher will not suffice, only a class D fire extinguisher will do the job. Lithium battery fires also produce toxic fumes.

    There are usually warning signs before a lithium battery catches fire. Some include swelling/bulging, leaking, making noises, or smelling weird (a "sweet" smell, or burning).

    If ever you experience a Lithium battery fire, evacuate the area immediately. Call campus PD at 716-645-2222 for the fastest response time.

Li-Ion/LiPo batteries are made from either a single Li-Ion/LiPo cell, or multiple cells wired together in series. A single cell has a nominal voltage of 3.6 - 3.7 V, with a fully charged voltage of 4.2 V. It is important not to discharge a cell lower than 3 V; the lowest you go should be 3.3 V. Single-cell batteries can be charged easily using simple chargers (many are sold with one included). On the other hand, multi-cell batteries require advanced chargers that can evenly charge all cells at once.

Many MicroMouse robots use a single-cell battery and regulate it down to 3.3V (see [Regulating Battery Power](#regulating-battery-power)). If you are planning to use components that require more than 3.3V (most motors do), you can either boost that voltage up, or use a dual-cell battery and regulate it down to 5 or 6 V.

Li-Ion/LiPo batteries will have a capacity rating in mAh and a discharge rating in C. To determine how much current a battery can supply, use the following formula:

\[
I_{max} = \text{Capacity} \times \text{Discharge Rating}
\]

For example, a $500 \text{ mAh}$ battery with a $20 \text{ C}$ discharge rating can supply a maximum of $0.5 \text{ A} \times 20 = 10 \text{ A}$ of current.

When designing your robot, make sure that all of your components combined will not draw more current than your battery can supply. If you exceed this limit, your battery may overheat and become damaged or even catch fire.

### NiMH Batteries

Most rechargeable AA, AAA, 9V, etc. batteries will be Nickel-metal hydride (NiMH) batteries. These batteries are much safer than Li-Ion/LiPos, however they have lower capacities and lower discharge rates. If you decide to go this route, you will need to minimize the current draw from all your robot's components. If you are using weak motors and don’t plan on going very fast, you might be able to make it work. These batteries are also large and somewhat heavy. Each NiMH AA battery has a nominal voltage of 1.2V, so you would need five wired in series to get to 6V. With good design, anything is possible, just be aware of the constraints.

## Regulating Battery Power

Unless you are using a battery pack with a built-in regulator, you must add a system of your own.

You may wonder: why not just power components directly from the battery? This could be problematic because the output voltage from your battery will not be consistent. Some components (i.e. your MicroController) require a stable voltage to work properly, so random spikes in battery voltage could cause your robot to stop working.

Regulating the battery voltage solves this issue by dropping or raising it to a consistent level. For example, a MicroMouse using a nominal 7 V battery might regulate its voltage down to 5 V to power its 5 V Arduino and sensors. Sometimes a MicroMouse will need multiple regulators if it is using components with different operating voltages.

!!! note
    Almost all components on your robot will require a stable voltage (usually 5 V or 3.3 V) to work properly. However, motors are special. If you can, it is often a good idea to place them downstream of your regulator so that they get a consistent voltage. This is a must for advanced BLDC motors, but for brushed DC motors it is not as important. If your regulated voltage is significantly lower than your motor voltage or your motors draw too much current for your regulator, consider powering them directly from battery power instead (if the voltage is suitable). Note that as the battery drains, the motors will slow down relative to the battery's voltage. Your robot can compensate for this with well-tuned PID controllers.

There are multiple ways to drop/raise your battery voltage to a stable level. Each method has its own advantages and disadvantages. The main two methods are Low-dropout (LDO) voltage regulators and switching regulators.

### Low-Dropout (LDO) Voltage Regulators

LDOs are simple, plug-and-play components that will drop a voltage without issue. However, LDOs can be very inefficient under certain circumstances. LDO power dissipation is affected by the voltage drop and by the output current. Use the following formula to determine how much power will be lost using an LDO:

\[
P=\left(V_{in}-V_{out}\right) \times I_{out}
\]

??? example
    Dropping 2V with an output current of 500 mA would result in 1W of power lost, primarily to heat. Not great.

There are only really two reasons to justify using an LDO on a MicroMouse:

1. Space is _extremely_ limited
2. You plan on drawing very little current, so the power loss is negligible

We do not recommend using a LDO for your main voltage regulator. However, an LDO would be acceptable in situations where you need to drop the voltage a little bit to power a single sensor or something.

For your main voltage regulator, consider using a switching regulator instead of an LDO.

### Switching Regulators

Switching regulators are complex systems consisting of many components. These types of regulators are often considerably more efficient than LDOs and are therefore recommended for MicroMouse, especially when dropping more than a few volts and drawing more than a few hundred milliamps of current. However, switching regulators take up more space, are more expensive, and may introduce electrical noise into the output.

Designing a switching regulator circuit can be challenging; however, there are pre-designed boards available to buy that work well. Search for "buck converter" (for step-down regulators) or "boost converter" (for step-up regulators) to find options.

If you plan to design your own switching regulator (i.e. for a custom PCB MicroMouse), consider checking out [TI’s WEBENCH Power Designer](https://webench.ti.com/power-designer/switching-regulator?powerSupply=0) to generate an example circuit tuned specifically for your requirements. 


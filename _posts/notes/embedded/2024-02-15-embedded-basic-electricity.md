---
layout: post
title: "Basic knowledge about electricity."
date: 2024-02-15 12:00:10 +0900
categories: notes embedded
permalink: /:year/:month/:title
img_path: /imgs/ebd/202402/
---



## DC(Direct Current)/AC(Alternating Current)
Probably we have heard about the terms, DC and AC, at science class when we were in middle school or high school. And I know roughle how it is different one and another. But when it comes to embbeded engineering, It's difficult to explain the concept and its difference.

As per chatgpt, I could get following anwer.

**Questions :**
>I'd like to know how AC and DC electricity types are different and practically used in embedded engineering industry.

**Answer :**
>1. **AC (Alternating Current)**:
   - **Direction of Flow**: AC current changes direction periodically. When graphed, it forms a sinusoidal or wave-like pattern. The up curve represents current flowing positively, while the down curve signifies the alternate cycle where the current moves negatively. This oscillating behavior gives AC its name.
   - **Voltage Reversal**: In AC circuits, the voltage periodically reverses due to the changing current direction.
   - **Efficient Distribution**: AC became popular in the late 19th century because it efficiently distributes power at low voltages. Initially, power is conducted at very high voltages, and AC transformers step it down to household levels.
   - **Practical Use**:
     - **Power Distribution**: AC is widely used for power distribution. It efficiently travels over long distances from power plants to homes and industries.
     - **Household Appliances**: The lamp next to your bed, for instance, operates on AC. Its wave-like motion makes it an efficient traveler.
     - **Transformers**: AC voltage can be easily transformed from high to low voltages using transformers.
     - **Motors and Generators**: AC powers electric motors and generators due to its alternating nature.
2. **DC (Direct Current)**:
   - **Direction of Flow**: DC current flows steadily in one direction. When graphed, it appears as a flat line.
   - **Steady Charge Movement**: In DC, electrons move from the negative terminal to the positive terminal of a battery or power source at a constant rate.
   - **Applications**:
     - **Embedded Systems**: DC is commonly used in embedded engineering due to its simplicity and predictability. Here's why:
       - **Stable Behavior**: DC behaves predictably, making it ideal for low-level hardware interactions.
       - **Resource Optimization**: Manual memory management in languages like C allows efficient resource usage.
       - **Portability**: C code can be compiled for various architectures.
       - **Efficiency**: Minimal runtime overhead and direct hardware access.
     - **Battery-Powered Devices**: Devices like smartphones, laptops, and sensors rely on DC power from batteries.
     - **Electronics**: Many electronic components operate on DC, such as transistors, microcontrollers, and sensors.
3. **Hybrid Usage**:
   - Interestingly, some devices use both AC and DC:
     - **Laptops**: The nozzle-shaped plug delivers DC to the laptop's battery, but it receives AC from the wall plug. The power adapter in between transforms AC to DC.
     - **Mobile Phones**: They charge via AC adapters but operate on DC from the battery.
4. **Comparison**:
   - Safety: AC poses a higher risk due to its higher peak voltage. DC is generally safer.
   - Waveform Distortion: AC waveforms can be distorted by inductive and capacitive loads.
   - Precautions: Installing AC supply requires more precautions due to the risk of shock.
>
>In summary, AC and DC play crucial roles in our modern world, and their distinct characteristics make them suitable for different applications. Whether it's powering your bedside lamp or running complex embedded systems, understanding AC and DC is fundamental to electrical engineering. 🌟¹²³⁴⁵.

**Reference**
>1. What’s the difference between AC and DC? - Mit Engineering. https://engineering.mit.edu/engage/ask-an-engineer/whats-the-difference-between-ac-and-dc/
2. AC vs DC (Alternating Current vs Direct Current) - Diffen. https://www.diffen.com/difference/Alternating_Current_vs_Direct_Current.
3. Alternating Current (AC) vs. Direct Current (DC) - SparkFun Learn. https://learn.sparkfun.com/tutorials/alternating-current-ac-vs-direct-current-dc/all.
4. AC vs. DC Power - Accuenergy. https://www.accuenergy.com/articles/ac-versus-dc-power/.
5. AC vs DC Power: Exploring the Differences and Applications. https://www.anker.com/blogs/ac-power/ac-vs-dc-power-the-ultimate-guide-to-electrical-currents.



## Converter, Inverter

Converter :

Inverter :





## What is Ground in eletricity?

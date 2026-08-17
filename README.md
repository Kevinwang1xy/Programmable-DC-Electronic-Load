# Programmable-DC-Electronic-Load


[Demo Video]: https://drive.google.com/file/d/1uX11_nZpo1H0H63yr_2g6Bv6h3FJr6_b/view?usp=drive_link



The electric power source is one of the most fundamental aspects of any engineering product or project, and often one of the most overlooked. Whether complicated or simple, any product that uses DC power requires a stable and efficient power source. However, in many cases, engineers have no easy way to test exactly how a DC power source will behave under specific load conditions relevant to their project until the product is complete. This programmable DC electronic load project serves to resolve this issue proactively by allowing the engineer to confirm power source behavior under realistic conditions before integrating it into a larger system.

This is done by designing a circuit involving an N-channel power MOSFET, an LM324 operational amplifier IC, a 1 ohm/5 watt sense resistor, and a user interface section involving an Arduino ESP32 microcontroller with two I2C components: an MCP4725 DAC and an Adafruit OLED display, as well as a raw rotary encoder.

The circuit works by utilizing the properties of the MOSFET and the op-amp. When provided voltage signals at both the positive and negative input pins, an op-amp will attempt to drive its output in a way that makes the two input voltages equal. For this project, the LM324 op-amp takes one input, V_sense, from the MOSFET source/sense resistor node, and another input, V_ref, from the user-controlled voltage level provided by the ESP32 microcontroller. The output of the op-amp is wired to the gate of the MOSFET. The MOSFET drain connects directly to the power source that the user wishes to test, such as a 1.5 V AA battery.

When the user rotates the rotary encoder, the ESP32 changes V_ref. Since the ESP32 only has two default digital output voltage levels, 0 V or 3.3 V, the DAC is added to allow more precise analog voltage control. As V_ref changes, the op-amp attempts to make V_sense match V_ref by driving the MOSFET gate. This causes the MOSFET to increase or decrease the current flowing from drain to source, directly controlling the load current drawn from the power source.

This voltage-to-current conversion is maintained by the 1 ohm sense resistor in the MOSFET source path. Since V_sense = I × R, and R = 1 ohm, the voltage across the sense resistor corresponds directly to the current through the load. For example, 0.10 V across the sense resistor represents approximately 0.10 A of load current. The OLED display serves as a screen to show the current setting and resulting voltage levels, with the interface coded in C.

  

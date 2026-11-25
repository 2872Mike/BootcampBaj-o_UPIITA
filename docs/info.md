<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

This circuit implements a 4-input, 4-output combinational logic circuit to automatically regulate the fluid level and temperature inside a storage tank. The system keeps the inlet valve (S) open to fill the tank whenever the high-level sensor (A) is 0 and there is no temperature sensor fault; meanwhile, the outlet valve (Y0) only opens when the low-level sensor (B) detects fluid (1) and the temperature is within the proper range (C = 0 and D = 0). The heating element (Y1) activates strictly when a low temperature is detected (D = 1) without any fault conditions, while the alarm (Y2) triggers upon an over-temperature condition (C = 1) or physically impossible sensor faults—such as the high-level sensor activating without the low-level sensor (A = 1, B = 0), or both temperature sensors activating simultaneously (C = 1, D = 1)—forcing a safe shutdown of the valves and heater during those fault states.

## How to test

Once your Custom Chip (or logic gate circuit) is wired to the DIP Switch and LEDs, start the simulation and verify the critical scenarios from the truth table:
1. Filling and Heating Test (0001): Set A=0, B=0, C=0, D=1. Only S and H should turn on (fill and heat).
2. Normal Operation Test (0100 and 1100):
At 0100, both S and Y0 should turn on simultaneously (filling and draining at the right temperature).
At 1100, the tank is full and at the right temperature: S should turn off, leaving only Y0 on.
3. Overheating Test (0110 and 1110): Set C=1 with D=0. The alarm (Y3) must turn on, and both Y0 and H must turn off (at 0110, only S remains active).
4. Sensor Fault Tests (10xx and xx11):
Set A=1 and B=0 (any combination of C, D): all outputs must be 0 except for the alarm (Y3=1).
Set C=1 and D=1 (any combination of A, B): again, only the alarm (Y3=1) should turn on, locking out all other outputs.

## External hardware

4 LEDs (with 220\ \Omega to 330\ \Omega current-limiting resistors): The most straightforward way to visualize the logic state of each output:
Blue LED for S (filling).
Green LED for Y0 (draining).
Orange/Yellow LED for Y1 (heating).
Red LED for Y3 (alarm).
Optional for added realism in Wokwi: You can wire a Buzzer in parallel with output Y3 for an audible alarm, or Relay modules to S, Y1, and Y2 to simulate the power stage driving real solenoid valves and the heating element.

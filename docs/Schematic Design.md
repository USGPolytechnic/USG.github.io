---
title: Schematic Desgin
---
Below is the Humidity and Temperature subsystem created for Team 308, Fresh Start. 
The system uses the PIC microcontroller and regulates the 9V using an LDO and a switch to start the device up.
It is the individual susbsystem, but in the future will need to use the same power source to charge other teamates systems.
The PCB will be made to be compact with surface mount applications being the focus of this design. I also had to ensure that the surface mount chips were not too small to be used in the design due to the needs to place them down onto the actual pcb.

Download PDF: [Schematic_Design_308Ethan.pdf](https://docs.google.com/document/d/1R_pSA_grRBiEOySVnYVTawVCs2YtuYDbptRplWQcUcs/edit?tab=t.0)

Download Project: [Project Ethan JP.zip](https://github.com/user-attachments/files/19198007/Project.Ethan.JP.zip)

View the power budget or component selection to examine the BOM or voltage distribution for this design.
The BOM: [Here](https://docs.google.com/spreadsheets/d/1XDYP-75lMF53_pUxz10kB5wWfIxgC6Pn/edit?gid=1046845005#gid=1046845005)
The Purchase Slip: [Here](https://docs.google.com/spreadsheets/d/1szL4_3IZWjw0e24ai2LgEwiDuFHJ5Ls0/edit?gid=1685898793#gid=1685898793)

All these components use the 3.3V power rail, with currents listed above

External Power Source

| Component- Componet Name                | Supply Voltage | Output voltage | Max Current (mA) | Total current (mW) |
|--------------------------|-------------------|---------------------|------------------|------------|
| 9V power - #0930 Peralta labs     | Wall 120V      | 9V               | 5000            | 50000      |
|   |                  |                    |                 |          |
|  |  |  |  | |
| 3.3V regulator AMS1117-3.3V              | 9V       | 3.3V                | 2000            | 2000       |

The power budget has helped to estimate power needs by allowing us to use the correct fuses and to use the appropriate LDO to regulate voltage

**Schematic**

![Screenshot 2025-03-11 093350](https://github.com/user-attachments/assets/aa48b9cc-4702-4269-acf3-b9b52e117ee5)


**PCB** 

![image](https://github.com/user-attachments/assets/e321084d-0bac-43e1-ab30-9426a3a80da0)

**Final Prodcut PCB Printout Front and Back**

![IMG_3903](https://github.com/user-attachments/assets/abe144e8-7049-4c0d-a957-43d244809811)

![IMG_3904](https://github.com/user-attachments/assets/cabb0cf0-cee1-46a7-9b2c-666d70504920)

---
**Teams Final PCB design**
---

**Internet**
![image](https://github.com/user-attachments/assets/d8cc0b0d-5415-4143-afde-b6ceb6444252)

**Sensor**
![image](https://github.com/user-attachments/assets/b25837d6-d17e-4dfa-b05a-9b1cf3508820)

**HMI**
![image](https://github.com/user-attachments/assets/4483b70d-a024-4e62-96be-0379ea7bd6ea)

**Motor Driver**
![image](https://github.com/user-attachments/assets/1fa9834f-f6fb-4cda-a1a4-d665376c2281)

---
**How does my individual design (sensor) satisfy user needs and product requirements using in depth discussion**
---

My sensor satisfies user needs by providing the foundation for the project. When a user from the MQTT server requests the current temperature, the sensor provides the data. It communicates via serial communication, which is coded to output the temperature in Celsius. If the customer requires the temperature in another format, such as Fahrenheit or displayed on an HMI, the data can be converted using an equation or routed through TX to the HMI accordingly.

Specifically, the schematic ensures that each trace is properly assigned. This means that each clock line is routed directly to its required destination—the microcontroller, SNAP programmer, or serial sensor. The same applies to other types of signal lines. Additionally, it is crucial to control voltage backflow using diodes. When regulating voltage, I ensure it is exactly 3.3V, as any deviation could either damage components or cause them to malfunction due to insufficient voltage. Other critical elements, such as enable pins, are also powered correctly.

One issue I had to focus on during testing was ensuring that specific components on my PCB were properly grounded. I discovered that my barrel jack was not actually connected to ground, despite being designed that way in my PCB layout. This highlighted the importance of understanding PCB debugging and performing proper fixes. It appeared that the barrel jack was not correctly connected to the copper layer that serves as ground.

With these improvements, including sensor selection and optimization, the customer now has a working serial sensor that meets the class requirements—including compatibility with I2C and proper 3.3V operation.

**Team's design and decision making process**

For the sensor, we encountered a lot of problems, but we were able to fix all of them, ultimately achieving a full checkoff and a functioning data sender. Initially, the team observed that the HDC Texas Instruments sensor worked; however, after a voltage spike, it failed. As a result, we had to switch through three different types of sensors before settling on the AHT21.

We first tried the DHT11, but it failed to send data because it was not I2C, and our microcontroller requires a clock. Next, we attempted to use the class-provided sensor, but it also did not work—I honestly don't know why, but it was likely a coding issue. Finally, we found the AHT21, which many Arduino users identified as user-friendly. We reached the same conclusion; it was easy to code, transmitted data smoothly, had a comprehensive datasheet, and operated at a voltage that matched the PIC18F47Q10’s requirements for proper functionality.

For the PCB, I used my teammate’s design, which had the PIC working flawlessly. A drawback of my own PCB was the amount of noise present due to floating SNAP programmer traces, as well as issues with my voltage regulator. Specifically, my voltage regulator did not fully adhere to the datasheet—it was an equivalent circuit but had problems with the enable pin not sharing voltage in parallel with the Vin trace.

**What would version 2.0 look like for this design**

![image](https://github.com/user-attachments/assets/e321084d-0bac-43e1-ab30-9426a3a80da0)

For future projects, I need to stick to proven solutions and follow them strictly, ensuring I fully understand every aspect of the design before proceeding. Research is crucial, but so is avoiding unnecessary risks or improvisations that could lead to failure.

The voltage regulator needs to be completely reworked. The schematic should match the design shown in the image exactly:

During circuit assembly, I noticed that my PCB layout had several differences from the datasheet design. Even though Altium assisted in creating the layout, its automated trace linker should not have been followed blindly. Instead, I should have manually routed the traces to match the datasheet specifications.

For example, in my PCB design, if you examine the voltage regulator pins, I routed a trace under the component twice—something not specified in the datasheet. The first instance was to link Vin and EN together, which should have been harmless. However, I supplied Vin first, then Enable, rather than vice versa. This may have prevented the voltage regulator from powering up correctly.

The second mistake was routing the feedback trace directly to ground, which was a critical error that cost me hours of rework. According to the datasheet, feedback should have been connected after the inductor. Next time, I need to avoid such risks by strictly adhering to reference designs and verifying every detail before committing to a layout.

---
**Altium**
---

**Below is the Atium Export of these PDFs:**

[Schematic_Design_308Ethan.pdf](https://github.com/user-attachments/files/19718026/Schematic_Design_308Ethan.pdf)


I had 3/5 checkoffs. This is due to the microchip PIC18F47Q10 that was surface-mounted onto the board was not found by the SNAP. However, after connecting the same headers to a Curiousity nano externally, we were able to read values off of the sensor. It is unknown as of 4/11 why this issue exists.
Below is the code that was attempting to reach the PIC.

[Subsytem verification.X.zip](https://github.com/user-attachments/files/19718045/Subsytem.verification.X.zip)

Here is the Altium File, used to create the PCB and schematic: 

[Altium 041125.zip](https://github.com/user-attachments/files/19718059/Altium.041125.zip)

[Gerberfiles]([FInal PCB order.zip](https://github.com/user-attachments/files/20030549/FInal.PCB.order.zip)



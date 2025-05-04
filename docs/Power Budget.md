---
title: Power Budget Overview for Sensor
---


| Component                | Voltage Range (V) | Typical Voltage (V) | Max Current (mA) | Power (mW) |
|--------------------------|-------------------|---------------------|------------------|------------|
| PIC18F47Q10      | 2.3V-5.5V       | 3.3V                | 250mA            | 825mW      |
| Blue surface mount LED |    2.8V - 3.6V               |       3.3V              |        125mA          |    108mW        |
| Switch | 0-24 VDC | 0-24 V DC | 50 mA | 165mW|
| AHT21            | 2.7V - 5.5V       | 3.3V                | 20mA             | 66mW       |
| **Total (maximum) Power Consumption** | -                 | 3.3V                | 240mA            | 1164mW      |

**How I used the power budget to estimate power needs and any other conclusions**

I had to ensure that the 9V input from the barrel jack was sufficiently regulated by the APY voltage regulator. The sensor only delivers the correct serial data when it receives the proper voltage on Vin, and the microcontroller functions as intended—without risk of damage—only if it is precisely 3.3V. In practice, when either the sensor or the PIC18F47Q10 was not exactly 3.3V, we encountered problems.

Power Source & Voltage Regulator Selection

I need to ensure that this part receives the correct amperage. Due to the team planning to use 5V instead of 3.3V for this side of the circuit we then have two choices. These choices are to either use 3.3V for the whole board or to use an LDO, since it is a minimal change of 1.7V we hope that this LDO regulator may work in reducing the voltage running through my devices. I will have to construct a circuit that regualates the voltage similar to the voltage regulator lab we finished in class.
| Solution                        | Pros                                      | Cons                              |
|---------------------------------|-------------------------------------------|-----------------------------------|
| LDO Regulator               |                                           |            |
| AMS1117-3.3V     |Simple, Readily available, Low noise  |Higher heat dissipation       |
|                                 |                                           |                       |
| Switching Regulator         |                                         |                                       |
| LM2596-3.3V                 |  High efficiency, Low heat generation |  Bulkier, Requires additional components  |
| AP63203WU-7                 |  Outputs exactly 3.3V, Surface mount, High efficiency | Higher heat dissipation, complex/multiple parts on connection schematic |

Rationale: The AP63203WU-7 was chosen for its precise 3.3V output, surface-mount form factor, and high efficiency, making it ideal for this embedded system.

**Conclusion**
This component selection ensures an efficient, low-power, and scalable design for a weather monitoring system using a PIC18F47Q10-I/P and HDC2080DMBR temperature and humidity sensor.

No battery is included in this system, it will be a direct connection.



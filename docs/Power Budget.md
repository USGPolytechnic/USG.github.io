---
title: Power Budget Overview for Sensor
---


Power Budget Calculation

| Component                | Voltage Range (V) | Typical Voltage (V) | Max Current (mA) | Power (mW) |
|--------------------------|-------------------|---------------------|------------------|------------|
| PIC18F47Q10-I/P      | 1.5-5.5V       | 3.3V                | 250mA            | 825mW      |
| Blue surface mount LED |    1.87V - 3.0V      |     (3.0)       |  2A (will run <300mA)    |    0.9W |
| B3U-1000P Switch | 0-24 VDC | 0-24 V DC | 50 mA | 165mW|
| HDC2080DMBR              | 1.62V - 3.6V       | 3.3V                |       550nA      | 1.815mW     |
| **Total (maximum) Power Consumption** | -                 | 3.3V                | 240mA            | 1164mW      |


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



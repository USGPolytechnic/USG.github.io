---
Component Selection for Weather Monitoring System 
---
Part 1: Major Component Selections
---
If you wish to view on PDF click [here](https://docs.google.com/document/d/16eBhtJ1a93Trgb88zd__rfECLNrKxZGtmtAWUIEOJiY/edit?tab=t.0#heading=h.ge7hmtquj7cv).

**Humidity and Temperature sensor component selection**

![image](https://github.com/user-attachments/assets/c80c5c43-d310-479b-98bc-2712b3758539)


**Links:**

[SHT31](https://www.digikey.com/en/products/detail/sensirion-ag/SHT31-DIS-B2-5KS/5872252)

[DH22](https://www.digikey.com/en/products/detail/sparkfun-electronics/SEN-18364/14635373)

[HDC1010YPAR](https://www.ti.com/lit/ds/symlink/hdc1010.pdf?HQS=dis-dk-null-digikeymode-dsf-pf-null-wwe&ts=1738985127772&ref_url=https%253A%252F%252Fwww.ti.com%252Fgeneral%252Fdocs%252Fsuppproductinfo.tsp%253FdistId%253D10%2526gotoUrl%253Dhttps%253A%252F%252Fwww.ti.com%252Flit%252Fgpn%252Fhdc1010)

[AHT21](https://www.digikey.com/en/products/detail/universal-solder-electronics-ltd/26585/26606395?s=N4IgTCBcDaIIIAkAqYCMIC6BfIA)


**Choice:** Option 4, the AHT21 humidity and temperature sensor

**Rationale:** The HDC1010YPAR was initially chosen due to its high accuracy, low power consumption, and I2C compatibility with the ESP32 microcontroller. However after testing the sensor initially worked as intended but after introducing 5V to the sensor it fried, causing issues with the initial desingn, this also fried the PIC. Due to this we needed a strong sensor that was durable for hands on programming and debugging, this is when we came across the AHT21

Datasheet: [PDF](https://pdf.directindustry.com/pdf/aosong-electronics-co-ltd/data-sheet-aht21/121567-1002931.html) 
Product page: [Link](https://www.digikey.com/en/products/detail/universal-solder-electronics-ltd/26585/26606395?s=N4IgTCBcDaIIIAkAqYCMIC6BfIA)

**Microcontroller Selection**

![Screenshot 2025-02-26 at 11 23 28 AM](https://github.com/user-attachments/assets/3656cc10-62a0-4da1-a851-d4e9acff289b)

**Links:**

[ESP32](https://www.espressif.com/en/products/socs/esp32-s3)

[Pic18](https://www.microchip.com/en-us/product/pic18f47q10)

[STM32](https://estore.st.com/en/stm32f103c4t6a-cpn.html)

**Choice:** Option 2 PIC18F47Q10 microcontroller

**Rationale:** The PIC18F47Q10 was chosen for its reliability, simplicity, and cost-effectiveness in an industrial setting. You may view how the 3.3V consumption will have to be considered. This will use an LDO. 
---
Summary of Major Components Used
---
| Component                                     | How it interacts with this project |
|---------------------------------------------|-------------------------------------|
|AHT21 Sensor| I2C communication data regarding current temperature and humidity for team system|
|PIC18F47Q10| 3.3V input with 47 pins utilizing clock and data lines in microcontroller from sensor|
| AP63203WU-7| Voltage Regualtor meant to take the 9V and make it 3.3V using decription of layout in datasheet|

This concludes majpr components for a full list of compoents that were sused in the PCB vitit: [Full List](https://docs.google.com/spreadsheets/d/1XDYP-75lMF53_pUxz10kB5wWfIxgC6Pn/edit?gid=1046845005#gid=1046845005)


That is all for the devices that communicate. I also chose to add a debugging LED that goes from my RE3 pin on my PIC to the Snap programmer header pins, here are the details on this.
Part Name - Blue Micro LED® SMD LED

Specifications:

Voltage Range: 1.8V - 3.6V

Typical Voltage: 2.0V

Max Current: 20mA

Power: 40mW

Package Size: 0603, 0805, 1206, etc.

Colors Available: Red, Green, Blue, Yellow, White

You can find more details and the datasheet [here](https://s3-us-west-2.amazonaws.com/catsy.557/C18571.pdf) .

[Product link](https://www.digikey.com/en/product-highlight/d/dialight/microled-surface-mount-leds)


---
How do these components contained in the BOM and the Major components mentioned meet product requirements
---
In my decision-making process, I had to once again consider what my team needed and the requirements for this project. Initially, I was confused because I thought I had to use the PIC microcontroller, even though I really wanted to use the ESP. This led to a back-and-forth decision—ESP → PIC → ESP → PIC—which made the debugging process chaotic due to the many iterations we went through before finally finding a functional solution.

The final layout consists of the following components: a 9V intake from the barrel jack, which is regulated by the APY, passing through an SS14 diode to the sensor. The sensor then connects directly to the microcontroller, which emits data via the TX line from the RX line, based on coding from the SNAP. This specific layout fulfilled the class requirements and met my project’s needs.

Despite numerous debugging issues caused by human error in design and soldering, the project was ultimately successful. The carefully chosen components matched the requirements, were supplied with the correct voltage, and had the necessary connections. Because of this, we were able to overcome the challenges and finalize a working system.

---
Part 2. Microcontroller Pin Allocation
---
![Screenshot 2025-02-28 230141](https://github.com/user-attachments/assets/30d6df6f-e6e0-4e7c-b0bc-4bab29c253eb)


![Screenshot 2025-02-28 230214](https://github.com/user-attachments/assets/91ae99d7-4bb5-48ee-95ca-16be8f68d097)

It may be helpful to go to view the pin layout on schematic if you wish [Layout](https://ejpete10.github.io/test_Datasheet.github.io/Schematic%20Design/).

I previously selected esp32 but now I switched to PIC, here is the following information regarding the PIC.

| ESP Info                                      | Answer |
|---------------------------------------------|--------|
| Model                                       | PIC18F47Q10 |
| Product Page URL                            | [link](https://www.microchip.com/en-us/product/PIC18F47Q10) |
| Datasheet URL(s)                            | [link](https://ww1.microchip.com/downloads/aemDocuments/documents/MCU08/ProductDocuments/DataSheets/PIC18F27-47Q10-Microcontroller-Data-Sheet-DS40002043F.pdf) |
| Application Notes URL(s)                    | [link](https://www.microchip.com/en-us/application-notes) |
| Vendor link                                 | [link](https://www.digikey.com/en/products/detail/microchip-technology/PIC18F47Q10-I-PT/8653924) |
| Code Examples                               | [link](https://github.com/microchip-pic-avr-examples) |
| External Resources URL(s)                   | [link](https://www.youtube.com/results?search_query=PIC18F47Q10+tutorial) |
| Unit cost                                   | ~$3.00 |
| Absolute Maximum Current for entire IC      | 250 mA |
| Supply Voltage Range                        | 1.8V / 3.3V / 5.0V / 5.5V |
| Maximum GPIO current (per pin)              | 25 mA |
| Supports External Interrupts?               | Yes |
| Required Programming Hardware, Cost, URL    | PICkit 4 (~$50) [link](https://www.microchip.com/en-us/development-tool/PG164140) |
| Works with MPLabX?                          | Yes |
| Works with Microchip Code Configurator?     | Yes |

---
Pins Used for final desing
---

| Module | # Available | Needed | Associated Pins (or * for any) |
|--------|------------|--------|------------------------------|
| GPIO   | 36         | 4      | RB1-RB4 |
| ADC    | 35         | 0      | * |
| UART   | 2          | 2      | RC3, RC4 |
| SPI    | 2          | 0      | * |
| I2C    | 2          | 2      | RD6, RD7 |
| PWM    | 2          | 0      | * |
| ICSP   | 1          | 1      | RE3 |

**Comment Regarding Feedback:** This microcontroller meets my needs and allows me to connect the necessary pins for my components that I will be using to ensure I can read humidity and temperature and send them to my teammates. For further information, you may view Image A below that details what the microcontroller looks like and what pins are being used in my subsystem. As you can see, I had additional pins I used as headers, I did not detail them in the needed section as they are not necessarily needed but are useful if I find out later on in the creation of my system that a teammate would like to access my microcontroller or if something goes wrong in wiring. I like to attempt to be as prepared as possible for this difficult task.


![Screenshot 2025-02-28 221751](https://github.com/user-attachments/assets/7fb9a71e-cc66-4403-8724-e45bcf49031a)

Image A: My Microcontroller pins

**Description of role in the team:**
I am working on the sensor. This project was largely inspired by this working example of a weather monitoring system: [link](https://srituhobby.com/how-to-make-a-weather-monitoring-system-with-esp32-board/). The system will use a 3.3V supply for my part in the team and use I2C communication with the ESP32. I used the I2C communication for a sensor last semester so I am somewhat familiar with how it works, I am starting to familiarize myself with how the PIC18F47Q10 works although not 100% familiar with its software and communication styles, it is something that I am learning in this class. Another problem was that I could not use the DHT11, however, after looking at the datasheet of the DHT11, I found that the only major difference technically between my two devices was that the DHT was more expensive and had a measuring supply current of 980 µW instead of 220 µW. This will require me to design the voltage and current supply accordingly by using a low-dropout (LDO) regulator or a buck converter to provide a stable 3.3V supply from the main power source.
Additionally, I will verify that the power rail can supply at least the maximum operating current of the sensor, accounting for any potential inrush currents. A current-limiting resistor or a precision power supply with current regulation can help prevent overcurrent damage. Finally, I will confirm proper voltage levels using a multimeter and check signal integrity with an oscilloscope if necessary.

**Error Checking & Pin Availability**

**Enough Pins?** Yes, the PIC has sufficient GPIOs to accommodate all necessary peripherals.

**Conflicts?** I2C and UART do not share pins, ensuring proper communication.

**Power Requirements?** The PIC accepts 3.3V input, which matches the HDC1010YPAR’s voltage requirement.

**Final Microcontroller Choice & Rationale**

**Microcontroller Selected:** PIC18F47Q10

**Rationale:**

**Adequate I/O:** Sufficient GPIOs to handle all peripherals.
**Wireless Capabilities:** n/a. My system was switched from using the esp32 to now PIC due to programming concerns.
**Low Power Consumption:** Suitable for battery-powered weather monitoring applications.
**Strong Software Support:** Compatible with ESP-IDF, Arduino, and MicroPython.
**Community and Documentation:** Extensive online resources for troubleshooting and development.

**Next Steps**

Test I2C communication with the HDC1010YPAR sensor using PIC.
Validate power supply stability using a multimeter.

---
Power Budget Calculation
---
I have a total of two major components I will be working with, the microcontroller and the sensor that consume the most power. However I have attempted at including other components that may consume power to run the current through.

| Component                | Voltage Range (V) | Typical Voltage (V) | Max Current (mA) | Power (mW) |
|--------------------------|-------------------|---------------------|------------------|------------|
| PIC18F47Q10      | 2.3V-5.5V       | 3.3V                | 250mA            | 825mW      |
| Blue surface mount LED |    2.8V - 3.6V               |       3.3V              |        125mA          |    108mW        |
| Switch | 0-24 VDC | 0-24 V DC | 50 mA | 165mW|
| AHT21            | 2.7V - 5.5V       | 3.3V                | 20mA             | 66mW       |
| **Total (maximum) Power Consumption** | -                 | 3.3V                | 240mA            | 1164mW      |

**How I used the power budget to estimate power needs and any other conclusions**

I had to ensure that the 9V input from the barrel jack was sufficiently regulated by the APY voltage regulator. The sensor only delivers the correct serial data when it receives the proper voltage on Vin, and the microcontroller functions as intended—without risk of damage—only if it is precisely 3.3V. In practice, when either the sensor or the PIC18F47Q10 was not exactly 3.3V, we encountered problems.

---
Section B assigning my components to a power rail.
---

For my components they will all be running off of 3.3V. The only part that will not is the female to male headers in the daisy chain which do not necessarily consume power, they will run off of the 9V power line which is shared across the team. So yes, all of my major components are 3.3V power rail due to the safety margin of 25% I will need a fuse of around 200mA. This may be seen in the schematic. 

![Screenshot 2025-02-28 223938](https://github.com/user-attachments/assets/8ccaf36d-c60b-4480-96c6-120cf6a77d60)

Image B fuse of 200mA to ensure that the PIC does not exceed maximum current. 

In the case of the humidity sensor, the amperage that is being sent around is what it means by the low amperage. In my design review I talked to a representative from microchip to ensure that my schematic will work given my components as I try to make a keen point about not frying any equipment. 

---
Section C, The Power Regulator.
---

I will be using the AP63203WU-7 LDO, this is further explained in the power source and voltage regulator section. I had to go through multiple LDOs to ensure that I have something reliable. In my LAB that we did to find a 3.3V output using an LDO my classmates told me that I should not use that LDO because one it is not surface mount and two it is not a guaranteed 3.3V output. I need as close to 3.3V and something reliable that is surface mount for which is why I choose this component given the options. 

---
Section D, the external power supply.
---

In a past project I also needed a 9V power supply to then regulate for whatever voltage I needed to power my component. I used the peralta labs #0930 9V unregulated power supply. I can then plug this into its 694108301002 Wurth Electronics, which has 5.5mm outer diameter and 2.5mm inner diameter barrel connector.

---
Final Microcontroller Selection & Rationale
---
The PIC18F47Q10 is optimal due to its low power consumption, industrial reliability, and robust GPIO options. This selection ensures reliable performance and efficient integration with all sensors and peripherals. It is also highly compatible for the sensor part of the team’s circuit. Due to the I2C communication, it may communicate with the PIC18F47Q10 and carry the same voltage 3.3V. I would need to use pull-up resistors around some parts of the sensor and ensure correct amperage using these sensors as well. 

---
Further Commentary regarding the compatibility of the PIC to be used to program my system. 
---
When I began my research on trying to find a suitable project for this class, I run across this: 
https://srituhobby.com/how-to-make-a-weather-monitoring-system-with-esp32-board/.

Although this project emphasis the use of the esp32 board, I can still prgram the sensor with the pic and allow a teammate to use a esp32 to then read the information it is sending off, due to this, I wanted to ensure that the information that my board receives will be able to be sent off to the necessary team member, in this case Sanjit who is working on the HMI. This is why I  initially wanted to use the esp32 board but due to fulfilling the requirements of this project, I decided to take one for the team and use the PIC in order for us to use a PIC in this project. I can use I2C to read the data and then UART to send or a GPIO for my teammates to also attach to my system as needed, this PIC still does the job either way. The wifi and bluetooth I will leave to a teammate while ensuring they may access my information of the PIC. I will now also ensure that when I send in my BOM that I order extra PICs in case mine does not work for any reason, the BOM is linked in this document as well if you wish to access it.

---
Power Source & Voltage Regulator Selection
----
I need to ensure that this part receives the correct amperage. Due to the team planning to use 5V instead of 3.3V for this side of the circuit we then have two choices. These choices are to either use 3.3V for the whole board or to use an LDO, since it is a minimal change of 1.7V we hope that this LDO regulator may work in reducing the voltage running through my devices. I will have to construct a circuit that regulates the voltage similar to the voltage regulator lab we finished in class.

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
This component selection ensures an efficient, low-power, and scalable design for a weather monitoring system using a PIC18F47Q10 and HDC1010YPAR temperature and humidity sensor.

No battery is included in this system, it will be a direct connection.

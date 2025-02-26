---
Component Selection for Weather Monitoring System 
---
Part 1: Major Component Selections
---
If you wish to view on PDF click [here](https://docs.google.com/document/d/16eBhtJ1a93Trgb88zd__rfECLNrKxZGtmtAWUIEOJiY/edit?tab=t.0#heading=h.ge7hmtquj7cv).

**Humidity and Temperature sensor component selection**
![Screenshot 2025-02-26 at 11 24 26 AM](https://github.com/user-attachments/assets/394f2a90-8bde-4b19-8c31-9fe0bc293e6e)

**Links:**

[SHT31](https://www.digikey.com/en/products/detail/sensirion-ag/SHT31-DIS-B2-5KS/5872252)

[DH22](https://www.digikey.com/en/products/detail/sparkfun-electronics/SEN-18364/14635373)

[HDC1010YPAR](https://www.ti.com/lit/ds/symlink/hdc1010.pdf?HQS=dis-dk-null-digikeymode-dsf-pf-null-wwe&ts=1738985127772&ref_url=https%253A%252F%252Fwww.ti.com%252Fgeneral%252Fdocs%252Fsuppproductinfo.tsp%253FdistId%253D10%2526gotoUrl%253Dhttps%253A%252F%252Fwww.ti.com%252Flit%252Fgpn%252Fhdc1010)


**Choice:** Option 1, the HDC1010YPAR humidity and temperature sensor

**Rationale:** The HDC1010YPAR was chosen due to its high accuracy, low power consumption, and I2C compatibility with the ESP32 microcontroller. Datasheet: [PDF](https://www.ti.com/lit/ds/symlink/hdc1010.pdf?HQS=dis-dk-null-digikeymode-dsf-pf-null-wwe&ts=1738985127772&ref_url=https%253A%252F%252Fwww.ti.com%252Fgeneral%252Fdocs%252Fsuppproductinfo.tsp%253FdistId%253D10%2526gotoUrl%253Dhttps%253A%252F%252Fwww.ti.com%252Flit%252Fgpn%252Fhdc1010) Product page: [Link](https://www.digikey.com/en/products/detail/texas-instruments/HDC1010YPAR/6205553)

**Microcontroller Selection**

![Screenshot 2025-02-26 at 11 23 28 AM](https://github.com/user-attachments/assets/3656cc10-62a0-4da1-a851-d4e9acff289b)

**Links:**

[ESP32](https://www.espressif.com/en/products/socs/esp32-s3)

[Pic18](https://www.microchip.com/en-us/product/pic18f47q10)

[STM32](https://estore.st.com/en/stm32f103c4t6a-cpn.html)

**Choice:** Option 2 PIC18F47Q10 microcontroller

**Rationale:** The PIC18F47Q10 was chosen for its reliability, simplicity, and cost-effectiveness in an industrial setting. You may view how the 3.3V consumption will have to be considered. This will use an LDO. 

---
Part 2. Microcontroller Pin Allocation
---
![Screenshot 2025-02-26 at 11 18 07 AM](https://github.com/user-attachments/assets/5a534626-29b3-4805-875c-037f50a4fd90)

The project demanded me not to use ESP32, therefore the data relating to esp32 on this document are unrelated.

[(Find links to ESP32 data in PDF)](https://docs.google.com/document/d/16eBhtJ1a93Trgb88zd__rfECLNrKxZGtmtAWUIEOJiY/edit?tab=t.0#heading=h.ge7hmtquj7cv)

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


---
Component Selection for Weather Monitoring System 
---
Part 1: Major Component Selections
---
If you wish to view on [PDF] click. ((https://docs.google.com/document/d/16eBhtJ1a93Trgb88zd__rfECLNrKxZGtmtAWUIEOJiY/edit?tab=t.0#heading=h.ge7hmtquj7cv))

**Humidity and Temperature sensor component selection**

![Screenshot 2025-02-07 at 9 56 07 PM](https://github.com/user-attachments/assets/24f72a32-4cd6-4a67-83b4-0887e238015a)


**Links:**

[SHT31](https://www.digikey.com/en/products/detail/sensirion-ag/SHT31-DIS-B2-5KS/5872252)

[DH22](https://www.digikey.com/en/products/detail/sparkfun-electronics/SEN-18364/14635373)

[HDC1010YPAR](https://www.ti.com/lit/ds/symlink/hdc1010.pdf?HQS=dis-dk-null-digikeymode-dsf-pf-null-wwe&ts=1738985127772&ref_url=https%253A%252F%252Fwww.ti.com%252Fgeneral%252Fdocs%252Fsuppproductinfo.tsp%253FdistId%253D10%2526gotoUrl%253Dhttps%253A%252F%252Fwww.ti.com%252Flit%252Fgpn%252Fhdc1010)


**Choice:** Option 1, the HDC1010YPAR humidity and temperature sensor

**Rationale:** The HDC1010YPAR was chosen due to its high accuracy, low power consumption, and I2C compatibility with the ESP32 microcontroller. Datasheet: PDF Product page: Link

**Microcontroller Selection**

![Screenshot 2025-02-07 at 9 58 06 PM](https://github.com/user-attachments/assets/fba8fff1-b090-41e1-99ca-522dec631633)


**Links:**

[ESP32](https://www.espressif.com/en/products/socs/esp32-s3)

[Pic18](https://www.microchip.com/en-us/product/pic18f47q10)

[STM32](https://estore.st.com/en/stm32f103c4t6a-cpn.html)

**Choice:** Option 1 ESP32-S3-WROOM-1-N4 microcontroller

**Rationale:** The ESP32-S3-WROOM-1-N4 was chosen for its integrated Wi-Fi, Bluetooth, and low power consumption, making it ideal for remote weather monitoring. Later on in Power Consumption, you may view how the 3.3V consumption will have to taken in consideration. This will use an LDO. 

---
Part 2. Microcontroller Pin Allocation
---
![Screenshot 2025-02-07 at 10 04 09 PM](https://github.com/user-attachments/assets/8c4b1265-8eff-4810-8514-f933d0ff4170)
![Screenshot 2025-02-07 at 10 04 28 PM](https://github.com/user-attachments/assets/44638fbc-5ac2-4631-aaee-26c051906e96)
![Screenshot 2025-02-07 at 10 04 41 PM](https://github.com/user-attachments/assets/af1de4a5-e1bd-4810-9679-eae397ddceef)
![Screenshot 2025-02-07 at 10 04 56 PM](https://github.com/user-attachments/assets/f2b688a3-5e4b-4866-9fdb-48c5cb45f3b2)

[(Find links to ESP32 data in PDF)](https://docs.google.com/document/d/16eBhtJ1a93Trgb88zd__rfECLNrKxZGtmtAWUIEOJiY/edit?tab=t.0#heading=h.ge7hmtquj7cv)

**Description of role in the team:**
I am working on the sensor. This project was largely inspired by this working example of a weather monitoring system: [link](https://srituhobby.com/how-to-make-a-weather-monitoring-system-with-esp32-board/). The system will use a 3.3V supply for my part in the team and use I2C communication with the ESP32. I used the I2C communication for a sensor last semester so I am somewhat familiar with how it works, although I am not used to the ESP32 nor does the worked-out example have it to be used. Another problem was that I could not use the DHT11, however, after looking at the datasheet of the DHT11, I found that the only major difference technically between my two devices was that the DHT was more expensive and had a measuring supply current of 980 µW instead of 220 µW. This will make me have to design the voltage and current supply accordingly by using a low-dropout (LDO) regulator or a buck converter to provide a stable 3.3V supply from the main power source.
Additionally, I will verify that the power rail can supply at least the maximum operating current of the sensor, accounting for any potential inrush currents. A current-limiting resistor or a precision power supply with current regulation can help prevent overcurrent damage. Finally, I will confirm proper voltage levels using a multimeter and check signal integrity with an oscilloscope if necessary.

**Error Checking & Pin Availability**

**Enough Pins?** Yes, the ESP32 has sufficient GPIOs to accommodate all necessary peripherals.

**Conflicts?** I2C and UART do not share pins, ensuring proper communication.

**Power Requirements?** The ESP32 provides 3.3V output, which matches the HDC1010YPAR’s voltage requirement.

**Final Microcontroller Choice & Rationale**

**Microcontroller Selected:** ESP32-S3-WROOM-1-N4

**Rationale:**

**Adequate I/O:** Sufficient GPIOs to handle all peripherals.
**Wireless Capabilities:** Includes Wi-Fi and Bluetooth, which could be useful for future expansion.
**Low Power Consumption:** Suitable for battery-powered weather monitoring applications.
**Strong Software Support:** Compatible with ESP-IDF, Arduino, and MicroPython.
**Community and Documentation:** Extensive online resources for troubleshooting and development.

**Next Steps**

Test I2C communication with the HDC1010YPAR sensor using ESP-IDF or Arduino.
Validate power supply stability using a multimeter.

---
Part 3: Power Budget Calculation
---

![Screenshot 2025-02-07 at 10 11 22 PM](https://github.com/user-attachments/assets/78a559b3-23f5-42d1-948e-c32539dee213)


---
Part 4: Final Microcontroller Selection & Rationale
---
The ESP32-S3-WROOM-1-N4 is optimal due to its low power consumption, integrated communication (Wi-Fi/Bluetooth), and robust GPIO options. This selection ensures reliable performance and efficient integration with all sensors and peripherals. It is also highly compatible for the sensor part of the team’s circuit. Due to the I2C communication, it may communicate with the ESP32 and carry the same voltage 3.3V. I would need to use pull-up resistors around some parts of the sensor and ensure correct amperage using these sensors as well.

---
Part 5: Power Source & Voltage Regulator Selection
---
I need to ensure that this part receives the correct amperage. Due to the team planning to use 5V instead of 3.3V for this side of the circuit, we then have two choices. These choices are to either use 3.3V for the whole board or to use an LDO, since it is a minimal change of 1.7V we hope that this LDO regulator may work in reducing the voltage running through my devices. I will have to construct a circuit that regulates the voltage similar to the voltage regulator lab we finished in class.
![Screenshot 2025-02-07 at 10 12 32 PM](https://github.com/user-attachments/assets/34829415-c0f8-4861-9685-44d3526598a9)

---
Part 6: Conclusion
---
This component selection ensures an efficient, low-power, and scalable design for a weather monitoring system using an ESP32-S3-WROOM-1-N4 and HDC1010YPAR temperature and humidity sensor.


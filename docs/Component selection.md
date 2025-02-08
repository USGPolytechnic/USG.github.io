Component Selection for Weather Monitoring System 1. Major Component
Selections

Humidity and Temperature sensor component selection

Solution Pros Cons HDC1010YPAR HDC1010YPAR

Surface mount link to product \$1.4 each

High accuracy (±0.2°C, ±2% RH), Low power consumption, I2C interface,
Compact SMD package Higher cost than basic sensors DHT22

Through-hole link to product \$6.5 I2C, Wide availability, Easy to
interface Larger size, Lower accuracy, expensive, Slower response time,
through- hole, will have to make it surface-mount capable. SHT31

Surface mount Link \$2.4 High precision, I2C, Factory calibrated, large
voltage range, visually pleasing and compact design. Requires careful
PCB design, seems like the same specs as the HDC, slightly more
expensive than the HDC. Choice: Option 1, the HDC1010YPAR humidity and
temperature sensor Rationale: The HDC1010YPAR was chosen due to its high
accuracy, low power consumption, and I2C compatibility with the ESP32
microcontroller. Datasheet: PDF Product page: Link Microcontroller
Selection Solution Pros Cons ESP32-S3-WROOM-1-N4 (Selected) esp32 c3
risc v nodemcu board

Link \$ 3.50 Dual-core processor, Low power consumption, Integrated
Wi-Fi and Bluetooth, Rich GPIO support More complex than simpler MCUs,
Requires proper firmware development PIC18F47Q10 Microchip
PIC18F47Q10-I/P PIC Microcontroller MCU, PIC18, 40-Pin PDIP

link to product \$1.5 Low cost, Simple to use, Industrial Reliability No
integrated Wi-Fi/Bluetooth, Limited computational power, no I2C
STM32F103

link to product \$4.07

High-performance ARM Cortex-M3, Large community support No native Wi-Fi,
Higher power consumption, price Rationale: The ESP32-S3-WROOM-1-N4 was
chosen for its integrated Wi-Fi, Bluetooth, and low power consumption,
making it ideal for remote weather monitoring. Later on in Power
Consumption, you may view how the 3.3V consumption will have to taken in
consideration. This will use an LDO.

2\. Microcontroller Pin Allocation HDC1010YPAR Pin ESP32-S3 Pin
Description SDA GPIO 8 (default) I2C Data Line (Can be reassigned to any
GPIO) SCL GPIO 9 (default) I2C Clock Line (Can be reassigned to any
GPIO) VCC 3.3V or 5V Power Supply (Ensure logic level compatibility) GND
GND Ground Connection ADR GND (0x40) or VCC (0x41) I2C Address Selection
Peripheral Pin(s) Allocated Notes Power and Ground 3.3V, GND Required
for all components UART (Communication with teammates) TX: GPIO1, RX:
GPIO3 Default UART pins I2C (HDC1010YPAR Sensor) SCL: GPIO22, SDA:
GPIO21 Required for I2C communication SPI (Optional, if needed for other
sensors) PICO: GPIO13, POCI: GPIO12, CS: GPIO14 Only if using SPI
peripherals ADC (Analog Sensors, if needed) ADC1_CH0 (GPIO1), ADC1_CH3
(GPIO4) Example pins for ADC functionality DAC (If needed for audio
output) DAC1 (GPIO25), DAC2 (GPIO26) Built-in DACs on ESP32 PWM (LED
control or motor control) GPIO5, GPIO18 Can be used for indicators
General GPIO (Buttons, Indicators, etc.) GPIO16, GPIO17 Configurable for
general use ESP 32 Table:

ESP Info Answer Comments Model ESP32-S3-WROOM-1-N4 This is the part
number Product Page URL Link Found on Espressif.com ESP32-S3-WROOM-1-N4
Datasheet URL Link Do not paste links directly into the table. Use a
link ESP32 S3 Datasheet URL Link to download

Has more detail on functions ESP32 S3 Technical Reference Manual URL
ESP32-S3 Technical Reference Manual Has details on I/O multiplexing,
USB, and others Vendor link Digi-Key Product Page Digikey, Jameco, etc.
Do not paste links directly into the table. Use a link Code Examples
ESP-IDF Examples URL(s) for libraries on GitHub or other sites related
to the microcontroller and your planned peripherals External Resources
URL(s) Link to resources page Search on Google and YouTube for other
resources for each specific microcontroller. Unit cost Approximately
\$3.50 USD Find on Digi-Key, Jameco, MPJA, or Octopart Absolute Maximum
Current for the entire IC 500 mA Find in the microcontroller datasheet
Supply Voltage Range Min: 3.0 V / Nominal: 3.3 V / Max: 3.6 V / Absolute
Max: 3.6 V Min / Nominal / Max / Absolute Max, as found in datasheet
Maximum GPIO current (per pin) 40 mA As found in datasheet Supports
External Interrupts? Yes As found in datasheet Required Programming
Hardware, Cost, URL USB-to-UART Bridge, approximately \$10, Example As
found in datasheet Module \# Available Needed Associated Pins (or \* for
any) UART 2 1 GPIO1 (TX), GPIO3 (RX) external SPI\* 2 1 GPIO18 (SCK),
GPIO23 (MOSI), GPIO19 (MISO), GPIO5 (CS) I2C 2 1 GPIO21 (SDA), GPIO22
(SCL) GPIO 36 10 \* ADC 20 1 GPIO34 LED PWM 16 1 \* Motor PWM 16 1 \*
USB Programmer 1 1 GPIO19 (D-), GPIO20 (D+)

Description on role in the team: I am working on the sensor. This
project was largely inspired by this working example of a weather
monitoring system: link. The system will use a 3.3V supply for my part
in the team and use I2C communication with the ESP32. I used the I2C
communication for a sensor last semester so I am somewhat familiar with
how it works, although I am not used to the ESP32 nor does the
worked-out example have it to be used. Another problem was that I could
not use the DHT11, however, after looking at the datasheet of the DHT11,
I found that the only major difference technically between my two
devices was that the DHT was more expensive and had a measuring supply
current of 980 µW instead of 220 µW. This will make me have to design
the voltage and current supply accordingly by using a low-dropout (LDO)
regulator or a buck converter to provide a stable 3.3V supply from the
main power source. Additionally, I will verify that the power rail can
supply at least the maximum operating current of the sensor, accounting
for any potential inrush currents. A current-limiting resistor or a
precision power supply with current regulation can help prevent
overcurrent damage. Finally, I will confirm proper voltage levels using
a multimeter and check signal integrity with an oscilloscope if
necessary.

Error Checking & Pin Availability \* Enough Pins? Yes, the ESP32 has
sufficient GPIOs to accommodate all necessary peripherals. \* Conflicts?
I2C and UART do not share pins, ensuring proper communication. \* Power
Requirements? The ESP32 provides 3.3V output, which matches the
HDC1010YPAR's voltage requirement.

Final Microcontroller Choice & Rationale Microcontroller Selected:
ESP32-S3-WROOM-1-N4 Rationale: \* Adequate I/O: Sufficient GPIOs to
handle all peripherals, including I2C, UART, ADC, PWM, and GPIO. \*
Wireless Capabilities: Includes Wi-Fi and Bluetooth, which could be
useful for future expansion. \* Low Power Consumption: Suitable for
battery-powered weather monitoring applications. \* Strong Software
Support: Compatible with ESP-IDF, Arduino, and MicroPython. \* Community
and Documentation: Extensive online resources for troubleshooting and
development. Next Steps \* Test I2C communication with the HDC1010YPAR
sensor using ESP-IDF or Arduino. \* Validate power supply stability
using a multimeter.

3\. Power Budget Calculation Component Voltage Range (V) Typical Voltage
(V) Max Current Power (mW) ESP32-S3-WROOM-1-N4 (LDO Regulator required)
3.0V - 3.6V 3.3V 200mA 660mW

HDC1010YPAR 2.7V - 5.5V 3.3V 20mA 66mW Total (maximum) Power Consumption
 - 3.3V 240mA 726mW

4\. Final Microcontroller Selection & Rationale The ESP32-S3-WROOM-1-N4
is optimal due to its low power consumption, integrated communication
(Wi-Fi/Bluetooth), and robust GPIO options. This selection ensures
reliable performance and efficient integration with all sensors and
peripherals. It is also highly compatible for the sensor part of the
team's circuit. Due to the I2C communication, it may communicate with
the ESP32 and carry the same voltage 3.3V. I would need to use pull-up
resistors around some parts of the sensor and ensure correct amperage
using these sensors as well. 5. Power Source & Voltage Regulator
Selection

I need to ensure that this part receives the correct amperage. Due to
the team planning to use 5V instead of 3.3V for this side of the circuit
we then have two choices. These choices are to either use 3.3V for the
whole board or to use an LDO, since it is a minimal change of 1.7V we
hope that this LDO regulator may work in reducing the voltage running
through my devices. I will have to construct a circuit that regualates
the voltage similar to the voltage regulator lab we finished in class.
Solution Pros Cons LDO Regulator AMS1117-3.3V (Selected) Simple, Readily
available, Low noise Higher heat dissipation Switching Regulator
LM2596-3.3V High efficiency, Low heat generation Bulkier, Requires
additional components Rationale: The AMS1117-3.3V was chosen for its
simplicity and ease of implementation in a low-power embedded system. 6.
Conclusion This component selection ensures an efficient, low-power, and
scalable design for a weather monitoring system using an
ESP32-S3-WROOM-1-N4 and HDC1010YPAR temperature and humidity sensor.

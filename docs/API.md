# API
This page discusses the sensor's message types

PIC18F47Q10T-I/PT with HDC2080DMBR Sensor - [Datasheet](https://www.ti.com/general/docs/suppproductinfo.tsp?distId=10&gotoUrl=https%3A%2F%2Fwww.ti.com%2Flit%2Fgpn%2Fhdc2080)

## Transmit Information: Temperature and Humidity
| **Variable Name**  | **Variable Type** | **Min Value** | **Max Value** | **Example**   | **Byte #** |
|---------------------|-------------------|---------------|---------------|---------------|------------|
| Send Temperature         | Float            | -40°C         | 85°C          | 25.5°C        | 2          |
| Send Humidity            | Float            | 0% RH         | 100% RH       | 38.9% RH      | 2          |
| Send Status/Error Code   | Integer          | 0.0           | 255.0         | 0 (No error)  | 1          |

## Process Information: Temperature and Humidity
| **Variable Name**  | **Variable Type** | **Min Value** | **Max Value** | **Example**   | **Byte #** |
|---------------------|-------------------|---------------|---------------|---------------|------------|
| Process Temperature Input   | Float            | -40°C         | 85°C          | 22.8°C        | 2          |
| Process Humidity Input      | Float            | 0% RH         | 100% RH       | 67.2% RH      | 2          |
| Process Processed Output    | Float            | -40°C         | 85°C          | 23.0°C        | 2          |

## Incoming Request: Temperature and Humidity
| **Variable Name**  | **Variable Type** | **Min Value** | **Max Value** | **Example**   | **Byte #** |
|---------------------|-------------------|---------------|---------------|---------------|------------|
| Receive Request Type        | Integer          | 0.0           | 255.0         | 1 (Request)   | 1          |
| Receive Temperature Request | Float            | -40°C         | 85°C          | 20.0°C        | 2          |
| Receive Humidity Request    | Float            | 0% RH         | 100% RH       | 60.0% RH      | 2          |

# These are the messages that were deemed necessary for the humidity and temperature sensor 
As seen below the teams communication sequence diagram, we may view the teams process for communicating in various different methods to reach our objective of allowing a user to read humidity, temperature, water flow rate and speed.

![image](https://github.com/user-attachments/assets/96821e97-3e54-4285-99f0-416ede6ef058)

# Humidity and temperature sensor responsibilities

  **RECEIVE - Incoming Request: Temperature and Humidity** - This is when a user initiates the system, asks temperature, humidity, or water speed or flow rate through the device. 

  **ACT ON - Process Information: Temperature and Humidity** - This is when the sensors go through their code to seek what they are capable of sensing. In my case the HDC2080 seeks out temperature and humidity through I2C data and clock capabilities. 
  
  **SEND -Transmit Information: Temperature and Humidity** - The final respocibility of the HDC2080 is to communicate the end process with the HMI so that it may be inserted into their code for processing and to be displayed to the user. 



 



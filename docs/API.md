# API
This page discusses the sensor's message types
## Team Member Roles

| **Team Member** | **Role**           | **Character ID** |
|-----------------|--------------------|------------------|
| Siddhant        | Motor Subsystem    | S                |
| Ethan           | Sensor Subsystem   | E                |
| Kevin           | HMI Subsystem      | K                |
| Sanjit          | Web Subsystem      | T                |


PIC18F47Q10T-I/PT with AHT21 Sensor - [Here](https://pdf.directindustry.com/pdf/aosong-electronics-co-ltd/data-sheet-aht21/121567-1002931.html)

## Messages

| **Message ID** | **Sender** | **Recipient** | **Description**                                |
|----------------|------------|----------------|------------------------------------------------|
| `FSEK00FS`     | Ethan      | Kevin          | Temperature message (`00` = temperature)       |
| `FSET00FS`     | Ethan      | Sanjit         | Temperature message (`00` = temperature)       |
| `FSES00FS`     | Ethan      | Siddhant       | Temperature message (`00` = temperature)       |


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



 



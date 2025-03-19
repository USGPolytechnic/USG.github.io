# Sensor Message Types for PIC18F47Q10T-I/PT with HDC2080 Sensor

## Transmit Information: Temperature and Humidity
| **Variable Name**  | **Variable Type** | **Min Value** | **Max Value** | **Example**   | **Byte #** |
|---------------------|-------------------|---------------|---------------|---------------|------------|
| Temperature         | Float            | -40°C         | 85°C          | 25.5°C        | 2          |
| Humidity            | Float            | 0% RH         | 100% RH       | 38.9% RH      | 2          |
| Status/Error Code   | Integer          | 0.0           | 255.0         | 0 (No error)  | 1          |

## Process Information: Temperature and Humidity
| **Variable Name**  | **Variable Type** | **Min Value** | **Max Value** | **Example**   | **Byte #** |
|---------------------|-------------------|---------------|---------------|---------------|------------|
| Temperature Input   | Float            | -40°C         | 85°C          | 22.8°C        | 2          |
| Humidity Input      | Float            | 0% RH         | 100% RH       | 67.2% RH      | 2          |
| Processed Output    | Float            | -40°C         | 85°C          | 23.0°C        | 2          |

## Incoming Request: Temperature and Humidity
| **Variable Name**  | **Variable Type** | **Min Value** | **Max Value** | **Example**   | **Byte #** |
|---------------------|-------------------|---------------|---------------|---------------|------------|
| Request Type        | Integer          | 0.0           | 255.0         | 1 (Request)   | 1          |
| Temperature Request | Float            | -40°C         | 85°C          | 20.0°C        | 2          |
| Humidity Request    | Float            | 0% RH         | 100% RH       | 60.0% RH      | 2          |

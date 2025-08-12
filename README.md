# NavIC + ESP32 GPS — Enhanced TinyGPS++ Sketch

## Overview
This sketch connects an ESP32 (via UART2) to a NavIC GPS module, using the TinyGPS++ library to capture location, speed, altitude, satellite data, HDOP, and computes distance and bearing to a predefined reference point. It also includes a GPS fix timeout for robust operation.

## Wiring
- NavIC TX → ESP32 GPIO16 (UART2 RX)
- NavIC RX ← ESP32 GPIO17 (UART2 TX)
- Use a clear-sky view for faster satellite acquisition
- Baud rate for both Serial Monitor and GPS: **115200**

## Data Output
Once a GPS fix is acquired, the Serial Monitor displays:

- **Latitude & Longitude** (high precision)
- **Speed** (knots)
- **Altitude** (meters)
- **Satellite Count** and **HDOP** (signal quality)
- **Distance to Target** (meters) and **Bearing** (degrees + cardinal direction using TinyGPSPlus::cardinal)
- **Time to Fix** (seconds after startup)

Should no fix be obtained within the specified timeout (e.g., 15 seconds), the program warns the user accordingly before retrying.

## Features & Advantages
- **GPS Fix Timeout**: Avoids indefinite waiting for lock—ideal for field or embedded usage.
- **Distance & Bearing Calculation**: Utilizes `TinyGPSPlus::distanceBetween()` and `TinyGPSPlus::courseTo()` to compute real-time navigation data :contentReference[oaicite:0]{index=0}.
- **Clean, Structured Output**: Designed for readability and usability in Serial Monitor logs.
- **Validation of Data**: Checks the recency (`.age()`) of GPS data to avoid stale outputs.

## Example Output
 Lat: 12.971599, Lon: 77.594567
Speed: 0.00 knots | Altitude: 920.50 m
Satellites: 7 | HDOP: 1.20
Distance to target: 0 m | Bearing: 0° (N)
Fix acquired in: 3.2 sec

if
❗ GPS fix timeout. Please check antenna and sky visibility.

Common Mistakes 
   -Swapping of RX/TX wires
   -Navic Requires constant 5V Connection from the microcontroller
   -Loose wires 
   




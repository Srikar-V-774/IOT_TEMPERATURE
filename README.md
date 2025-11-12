# IOT_TEMPERATURE

Project type: Mini embedded project (Temperature detector / Fever alert)
Authors: S. Joshuva Srikar Varma (URK24CS9017) + Team
Course: 23CS2022 — Internet of Things
Date: October 2025

Project summary

A simple, low-cost fever detector using an LM35 temperature sensor, Arduino, 16x2 LCD and buzzer. The device reads analog temperature from the LM35, converts it to °C, displays the value on the LCD, and triggers a buzzer when temperature exceeds a configurable threshold (default: 38.0°C). This is a prototype for quick fever screening — easy to build and test.
Note: This repository contains the original offline prototype code. Future features described below are conceptual and not part of the delivered prototype.

How it works (short)

LM35 outputs 10 mV per °C.
Arduino reads analog value (ADC) and converts to voltage.
Temperature (°C) = voltage * 100.
Arduino displays temperature on the 16x2 LCD.
If tempC > highTemp → buzzer sounds and LCD shows “ALERT! High Temp”.
Hysteresis: buzzer turns off only when temp drops below lowTemp to avoid flicker.
Hardware used
Arduino Uno (or compatible)
LM35 temperature sensor
16x2 LCD (HD44780)
Buzzer (active or passive)
Breadboard, jumper wires
10k potentiometer (optional — for adjustable threshold)
USB cable or 9V battery for power
Suggested wiring (brief)

LM35: VCC → 5V, GND → GND, OUT → A0
LCD: standard 4-bit wiring (RS, E, D4–D7) to Arduino digital pins
Buzzer: buzzer pin → D8 (use transistor or driver if using passive buzzer), GND → GND
Potentiometer (optional): middle pin → A1 (or any analog pin), ends → 5V & GND

Code (where to find)
Put the Arduino sketches in the code/ folder. Use the Arduino IDE to open the .ino files and upload to the board.
FeverDetector.ino is the main sketch to run the device with LCD display and buzzer alert.
FeverDetector_serial_log.ino prints readings to Serial Monitor (useful for logging or debugging).
Typical parameters used
Default highTemp = 38.0 °C
Default lowTemp = 37.5 °C (used to reset buzzer — hysteresis)
LCD refresh / loop delay = 500 ms (adjustable in code)
Testing and calibration
Compare LM35 readings with a trusted thermometer and apply a software offset if needed.
Ensure good thermal contact for repeatable measurements. Allow sensor warm-up time for stable readings.
Limitations

This prototype measures temperature only (contact sensor) — not a medical device.
Accuracy depends on sensor placement, ambient temperature, and ADC reference stability.
No built-in remote notification in the prototype (offline only).
Future scope (conceptual / not implemented)

Remote alerts: integrate ESP32/ESP8266 or GSM (SIM800) to send SMS or push notifications to the user and their emergency contacts when fever is detected.

Two-way communication: allow a trusted contact (e.g., daughter/relative) to receive alerts and send back a confirmation or voice/text message to the patient via an app/SMS or an MQTT chat channel.

Contactless sensing: switch to an IR sensor (e.g., MLX90614) for non-contact temperature measurement.

Data logging & analytics: store readings on SD card or cloud (ThingSpeak / Firebase) for history and trend analysis.

Mobile app / dashboard: build a simple mobile/web interface to view readings, acknowledge alerts, and chat (two-way commands).

Security: use encrypted channels (TLS) and authenticated access if connecting to the Internet.

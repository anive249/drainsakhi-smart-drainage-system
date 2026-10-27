# DrainSakhi Technical Design

## Architecture
Two ultrasonic sensors → ESP32 controller → threshold/persistence logic → LED and buzzer alert.

## Intended use
A tabletop demonstration to explore water-level monitoring. The system is not a certified safety device and is not validated for installation in real drains.

## Logic
- Measure distance from each sensor to the water surface.
- If either reading is invalid, print a diagnostic and do not trigger an alert from that sample.
- Check whether either distance is below the configured high-water threshold or the difference between readings exceeds a configured threshold.
- Trigger the alert only after the condition persists for the required number of samples.

## Limitations and risks
- Different water levels do not prove a blockage.
- Splashing, sensor angle, foam, debris, condensation, and sensor fouling can cause incorrect readings.
- Thresholds must be calibrated and false alerts/missed alerts documented.
- Sensors and electronics require appropriate protection before any outdoor use.

## Safety
HC-SR04 ECHO outputs commonly use 5 V. ESP32 GPIO is not 5 V tolerant; use a suitable voltage divider or logic-level shifter. Keep electronics dry.

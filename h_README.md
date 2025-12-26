# iiitH_iotBin
# Hardware Architecture – Smart Waste Bin Node

Each waste bin is equipped with a low-power sensing and communication unit that monitors the fill level and reports it to a central server.

## Main Components
- Ultrasonic Sensor: Measures the distance between the bin lid and waste surface.
- Microcontroller: ESP32 (low power, integrated communication support).
- Communication Module: LoRa (long-range, low power).
- Power Unit: Battery-powered with voltage regulation.

## Working Principle
1. The ultrasonic sensor measures the distance to the waste.
2. The ESP32 converts distance into fill percentage.
3. If the fill level crosses a threshold, data is transmitted.
4. The system enters deep sleep to conserve power.

This architecture enables scalability and energy-efficient deployment across multiple city zones.

## Power Strategy
- The ESP32 remains in deep sleep for most of the time so that current consumption is in microamps.
- Sensor readings are taken periodically (every 30–60 minutes).
- Data transmission occurs only when significant change is detected, transmission current burst will be high.

## Estimated Consumption
- Deep sleep current: ~10 µA
- Active current: ~120 mA for ~2 seconds per transmission

## Battery Life
With periodic sensing and deep sleep usage, the estimated battery life is approximately 6–12 months depending on transmission frequency.
Optional solar charging can further extend battery life.

# Hardware Fault Handling
## Sensor Errors
- Multiple ultrasonic readings are averaged to reduce noise.
- Sudden spikes or unrealistic values are ignored.

## Sensor Blockage
- If distance remains unchanged for long periods, the system flags a potential blockage.

## Power Faults
- Battery voltage is monitored.
- Low battery levels trigger maintenance alerts.

- ESP32 Datasheet: https://www.espressif.com
- HC-SR04 Ultrasonic Sensor Datasheet
- LoRa SX127x Datasheet

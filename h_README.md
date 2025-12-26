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
- Battery voltage is monitored and low battery levels trigger maintenance alerts.

# References
- [ESP32S3 Datasheet] (https://cdn-shop.adafruit.com/product-files/5477/esp32-s3_datasheet_en.pdf)
- [HC-SR04 Ultrasonic Sensor Datasheet] (https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf) 
- [LoRa SX127x Datasheet] (https://semtech.my.salesforce.com/sfc/p/#E0000000JelG/a/2R0000001Rbr/6EfVZUorrpoKFfvaF_Fkpgp5kzjiNyiAbqcpqh9qSjE)

# Cost
ESP32 S3 is [Rs 163] (https://www.digikey.in/en/products/detail/espressif-systems/ESP32-S3/15822445)
LoRa SX1278 is [Rs 258] (https://robokits.co.in/wireless-solutions/wireless-automation/433mhz-lora-sx1278-long-range-rf-wireless-module?srsltid=AfmBOooeR_Fk0S_jR67Tin0aKT3XEeGptbabyCAN1kSOIfCycvSDRbaqVNk)
HC-SR04 is [Rs 58] (https://shokitech.com/product/ultrasonic-sensor/?srsltid=AfmBOoqIjHFPvqD05Q4rkhDdOeaSh00jXH1uwqa-ZDxWAtISYLQCfgn57do)

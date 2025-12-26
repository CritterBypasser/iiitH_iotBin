# Overview
Each smart waste bin is equipped with a low-power sensing and communication unit that monitors the fill level and reports data to a central system.
An ultrasonic sensor mounted on the bin lid measures the distance to the waste surface. This data is processed by an ESP32 microcontroller, which calculates the fill percentage and manages communication. A LoRa communication module enables long-range, low-power data transmission to a nearby gateway.
The entire system is battery-powered, optimized using deep sleep modes and periodic sensing to ensure long operational life. This architecture supports scalable deployment of 100+ bins across multiple city zones.

# Why only 1 ultrasonic sensor
- Blockage is not a continuous failure
- Plastic or waste may block the sensor temporarily
- Adding a second sensor doubles cost, power, and complexity
- For 100 bins, redundancy must be cost-justified
- We do software mitigation first, hardware redundancy only if necessary

# When would multiple sensors be justified?
- Large industrial dumpsters
- Safety-critical systems
- Research deployments

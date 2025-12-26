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

# Why a Gateway is Required
In a large-scale IoT deployment (the 100 smart waste bins), individual sensor nodes are designed to be low-power, low-cost, and long-range, which limits their ability to directly connect to the internet.

A gateway is required to act as an intermediate aggregation point between the waste bins and the cloud backend.

## Key reasons for using a gateway:
- Enables long-range communication using low-power protocols such as LoRa
- Aggregates data from hundreds of bins
- Offloads internet connectivity from battery-powered nodes
- Improves scalability and network reliability
- Reduces power consumption at the bin level
- Each waste bin communicates only with the gateway, while the gateway handles all cloud communication.

# Components of the Gateway
The gateway is a fixed infrastructure device and is typically mains-powered.

## Core Gateway Components
1. LoRa Concentrator Module
   - Example: SX1302
   - Receives data from hundreds of LoRa nodes simultaneously
   - Supports multiple channels and spreading factors

2. Host Processor
   - Raspberry Pi
   - Runs packet forwarding and network management software
   - Handles data preprocessing and security

3. Internet Backhaul Interface
   - Wi-Fi, or 4G/LTE
   - Connects the gateway to the cloud server

4. High-Gain LoRa Antenna
   - Improves coverage and reliability
   - Typically mounted on poles or rooftops

5. Power Supply
   - Mains power with optional battery backup (UPS)

# Battery Pack Used in the Waste Bin Node
Each waste bin is a self-contained IoT node and must operate for long durations without frequent maintenance.

# Power Requirements
- Support ESP32 microcontroller and LoRa transmission peaks
- Enable long battery life (6–12 months)
- Compact and safe
- Cost-effective for large deployments

# Ideal Battery Pack for the Waste Bin
## Recommended Choice: Single 18650 Li-ion Battery
- Nominal Voltage 3.7 V 
- Capacity 2600–3400 mAh
- Rechargeable
- Compact

# Why 18650 Li-ion is Ideal
- Capable of handling high current bursts during LoRa transmission
- Widely available and cost-effective
- Suitable for compact enclosures
- Supports long operational life with proper power management

# Power Architecture of the Waste Bin
18650 Li-ion Battery (3.7 V)
       TO 
Low Quiescent Current Regulator
        TO
3.3 V Rail → ESP32 + Ultrasonic Sensor + LoRa Module

# Network Topology Choice
The smart waste bin monitoring system uses a star topology, where each waste bin node communicates directly with a central gateway using a long-range, low-power protocol (LoRa).

In this topology, waste bins act as end nodes, gateways act as aggregation points, and all data is forwarded from the gateway to the cloud backend.

# Why Star Topology is Preferred
1. Low Power Consumption
-Waste bins are battery-powered. In a star topology, each node only transmits its own data and does not forward data for other nodes, significantly reducing energy usage.

2. Simpler Node Design
- Nodes do not require routing logic or neighbor discovery, reducing firmware complexity and lowering the probability of software faults.

3. High Scalability
- A single LoRa gateway can support hundreds to thousands of nodes, making star topology suitable for city-wide deployments.

4. Ease of Maintenance
- Adding or removing bins does not affect other nodes. Failures are isolated and easier to diagnose.

# Why Mesh Topology is NOT Used
- Higher Power Consumption: Nodes must stay awake to relay packets for others
- Increased Complexity: Routing, synchronization, and link management increase firmware complexity
- Lower Reliability in Static Urban Environments: Node failure can disrupt routing paths
- Poor Fit for Low-Data-Rate Sensors: Mesh benefits are unnecessary for small periodic data packets

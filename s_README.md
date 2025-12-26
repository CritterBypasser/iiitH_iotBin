# Software Architecture – Smart Waste Bin Monitoring System (100 Nodes)

## Overview
- This software system manages a large-scale IoT deployment of 100 smart waste bins distributed across multiple city zones. The design emphasizes scalability, fault tolerance, low power consumption, and efficient route optimization.
- The system follows distributed sensing + centralized decision-making.

## System Scale Assumptions
- Total bins: 100
- Zones: 5–10 zones (≈10–20 bins per zone)
- Communication: MQTT over LoRa
- Update interval: 30–60 minutes per bin
- Cloud backend is stateless and horizontally scalable

## Software Components
1. Bin Node Firmware (×100 identical nodes)
2. Gateway / Network Server
3. Cloud Backend Services
4. Dashboard & Alerting System

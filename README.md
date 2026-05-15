# 🔐 MuleBot — Secure IoT Communication System Using ESP-NOW

> Autonomous Mobile Data-Mule Architecture for Distributed Sensor Networks

---

## 📌 Overview

**MuleBot** is a distributed cyber-physical IoT system designed to solve the problem of unreliable connectivity in remote or obstructed environments.  
The system uses a **mobile ESP32-based robotic platform** to autonomously travel to sensor nodes, collect environmental data using **ESP-NOW**, and securely transfer the collected information to a centralized base station.

Unlike traditional IoT architectures that depend on continuous Wi-Fi or cloud connectivity, MuleBot uses a **mobile data-mule approach**, significantly reducing power consumption while improving communication reliability.

---

## 🚀 Key Features

- 🔐 Secure peer-to-peer communication using ESP-NOW
- 🤖 Autonomous mobile robot for data collection
- 👁️ Computer-vision-based node detection
- ⚡ Low-power operation without cloud dependency
- 📡 TCP + Serial + ESP-NOW hybrid communication
- 📊 Automatic CSV-based data logging
- 🧩 Modular multi-controller architecture
- 🔋 Energy-efficient distributed sensing system

---

# 🧠 System Architecture

```text
                 ┌─────────────────────┐
                 │   PC Vision System  │
                 │ (Python + OpenCV)   │
                 └─────────┬───────────┘
                           │ TCP / Serial
                           ▼
                 ┌─────────────────────┐
                 │  Base Station ESP32 │
                 │ USB ↔ ESP-NOW Bridge│
                 └─────────┬───────────┘
                           │ ESP-NOW
                           ▼
                 ┌─────────────────────┐
                 │ Data Postman ESP32  │
                 │  (On MuleBot Car)   │
                 └──────┬──────┬───────┘
                        │      │
               ESP-NOW  │      │ ESP-NOW
                        ▼      ▼
              ┌────────────┐ ┌────────────┐
              │ DHT11 Node │ │ MQ-6 Node  │
              └────────────┘ └────────────┘
```

---

# 📂 Repository Structure

```text
secure-iot-communication-system-using-esp-now/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── firmware/
│   ├── README.md
│   │
│   ├── sensor_dht11/
│   │   └── dht11_sensor.ino
│   │
│   ├── sensor_mq6/
│   │   └── mq6_gas_sensor.ino
│   │
│   ├── data_postman/
│   │   └── data_postman.ino
│   │
│   ├── car_controller/
│   │   └── car_controller.ino
│   │
│   └── base_station_receiver/
│       └── base_station_receiver.ino
│
├── pc_software/
│   └── vision_control/
│       ├── README.md
│       ├── vision_controller.py
│       ├── requirements.txt
│       └── node_calibration.txt
│
├── hardware/
│   ├── components_list.md
│   ├── pin_connections.md
│   └── wiring_diagrams/
│
├── docs/
│   ├── system_architecture.md
│   ├── communication_flow.md
│   ├── security_design.md
│   └── diagrams/
│
├── setup/
│   ├── flashing_guide.md
│   ├── network_configuration.md
│   └── esp_now_pairing.md
│
├── testing/
│   ├── test_cases.md
│   ├── results.md
│   └── performance_analysis.md
│
└── demo/
    ├── demo_video_link.md
    └── images/
```

---

# 🔧 Hardware Components

| Component | Purpose |
|---|---|
| ESP32 | Main embedded controller |
| ESP32-CAM | Live vision streaming |
| DHT11 Sensor | Temperature & humidity sensing |
| MQ-6 Sensor | Gas concentration sensing |
| Ultrasonic Sensor | Obstacle & distance detection |
| Motor Driver | Robot movement control |
| DC Motors | Mobile robot actuation |
| Li-ion Battery Pack | Portable power supply |

---

# 🔗 Communication Design

| Layer | Protocol |
|---|---|
| Sensor Nodes ↔ MuleBot | ESP-NOW |
| PC ↔ Car Controller | TCP |
| PC ↔ Base Station | Serial |
| Base Station ↔ MuleBot | ESP-NOW |

---

# 👁️ Computer Vision Navigation

The PC-side OpenCV application performs:

- LED-based node detection
- Distance estimation
- Center alignment verification
- Autonomous robot guidance
- Mission orchestration

The robot rotates incrementally, scans for target nodes, aligns with the detected LED marker, and automatically initiates the data collection sequence.

---

# 🤖 MuleBot Workflow

```text
1. Vision system detects target node
2. Car controller navigates toward node
3. Data Postman triggers sensor sampling
4. Sensor node transmits readings via ESP-NOW
5. MuleBot returns to base station
6. Base station securely transfers data to PC
7. Data saved as CSV logs
```

---

# 📊 Data Logging

Sensor data is stored automatically in CSV format.

### DHT11 Example

```csv
Timestamp,Temperature,Humidity,Base_Station_Time
2025-11-11 22:24:46,25.3,72,2025-11-11 22:25:00
```

### MQ-6 Example

```csv
Timestamp,Gas_Concentration,Base_Station_Time
2025-11-11 22:28:25,1312,2025-11-11 22:28:39
```

---

# ⚙️ Setup Instructions

## 1️⃣ Flash ESP32 Firmware

Upload each firmware module to its respective ESP32:

| Firmware | ESP32 Role |
|---|---|
| `dht11_sensor.ino` | DHT11 Sensor Node |
| `mq6_gas_sensor.ino` | MQ-6 Sensor Node |
| `data_postman.ino` | MuleBot Coordinator |
| `car_controller.ino` | Mobile Robot Controller |
| `base_station_receiver.ino` | Base Station |

---

## 2️⃣ Install Python Dependencies

```bash
cd pc_software/vision_control
pip install -r requirements.txt
```

---

## 3️⃣ Start Vision Controller

```bash
python vision_controller.py
```

---

# 🎮 Controls

| Key | Action |
|---|---|
| `1` | Scan for DHT11 node |
| `2` | Scan for MQ-6 node |
| `g` | Start mission |
| `e` | Calibrate distance |
| `s` | Secure data transfer |
| `q` | Quit |

---

# 📈 Results

The system successfully demonstrated:

- ✔ Reliable node detection
- ✔ Stable autonomous movement
- ✔ Accurate sensor data collection
- ✔ Low-power communication
- ✔ Consistent ESP-NOW performance
- ✔ Successful CSV-based data transfer

---

# 🔮 Future Improvements

- GPS-assisted navigation
- LoRa integration
- ESP-NOW encryption
- Multi-MuleBot coordination
- Web dashboard visualization
- Advanced obstacle avoidance
- ML-based object detection

---

# 🎯 Applications

- Smart agriculture
- Industrial safety monitoring
- Environmental sensing
- Defence & restricted-area surveillance
- Remote wireless sensor networks
- Autonomous inspection systems

---

# 👨‍💻 Author

**Aditya Patil**  
Embedded Systems • IoT • Robotics • Computer Vision

---

# 📜 License

This project is made for educational purpose.

---

# ⭐ Final Note

MuleBot demonstrates how embedded systems, robotics, computer vision, and low-power wireless communication can be combined into a scalable and intelligent edge-IoT platform capable of operating in environments where traditional connectivity is unreliable.

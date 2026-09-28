# VOLT-VANGUARD-

# AI-Powered Underground Mine Safety Monitoring & Rescue System ⛏️🤖

> A low-cost, AI-powered ground rover that monitors hazardous gases, detects trapped survivors, and maps unknown underground tunnels — keeping rescue teams safe and informed.

**Problem Statement:** SIH26039 — AI-Powered Underground Mine Safety Monitoring and Rescue System (Smart Automation | Hardware)

**Status:** 🚧 Building for Smart India Hackathon 2026

---

## 🎯 The Problem

Underground mines in India face frequent, recurring accidents — toxic gas build-ups, floods, collapses, and trapped workers. When disaster strikes, rescue teams often have to enter smoke-filled, GPS-denied, low-visibility tunnels blind, risking their own lives. Industrial rescue robots exist, but they cost lakhs, so smaller mining setups can't afford them.

## 💡 Our Solution

An AI-powered ground rover that scouts hazardous zones **before** humans enter, and sends real-time data back to a base dashboard:

- ✅ **Gas monitoring & leak prediction** — MQ-2 / MQ-135 sensors with AI analysis give early warnings for hazardous gas levels
- ✅ **Survivor detection** — thermal (MLX90640) + night-vision camera with YOLO-based human detection works in dark, smoke-filled tunnels
- ✅ **SLAM-based live mapping** — builds a live map of unknown tunnels and tracks the rover's position to guide the rescue team
- ✅ **Structural crack identification** — image processing flags unstable tunnel sections to prevent collapse hazards
- ✅ **Long-range, low-power communication** — LoRa sends real-time photo alerts with location to the base dashboard, even where Wi-Fi/4G fail
- ✅ **Remote dashboard** — live map, gas levels, temperature & humidity, human-detection alerts with image and exact location

Built as a **force-multiplier for rescue teams** — scouting first, not replacing them.

---

## 🏗️ Architecture

```
[Sensors: Gas | Thermal | Camera | LiDAR | IMU | Encoder | DHT11/22 | Mic]
                        │
                        ▼
        [Raspberry Pi — Processing Unit]
                        │
     ┌──────────────────┼──────────────────────┐
     ▼                  ▼                      ▼
[Gas Leakage      [SLAM — Mapping &      [Human Detection
 Prediction]       Localisation]          (YOLO) + Crack
                                          Detection]
     └──────────────────┼──────────────────────┘
                        ▼
              [Motor Driver → Ground Rover]
                        │
                        ▼
        [LoRa Transmitter] ~~~ LoRa ~~~> [LoRa Receiver]
                                                │
                                                ▼
                               [Dashboard — Phone / PC]
                    Live Map | Gas | Temp/Humidity | Alerts | Human Detected

[Analog Camera] → [FPV Transmitter] ~~~> [FPV Receiver] → Live Video (separate link)
```

**Data flow:** Sensor data (Analog/Digital, I2C, UART) → Raspberry Pi runs AI/ML models → processed data + alerts sent over LoRa → base station dashboard. Live video runs on a separate analog FPV link.

---

## 🛠️ Tech Stack

| Layer | Tech |
|---|---|
| Processing Unit | Raspberry Pi (sensor fusion, AI/ML inference, motor control) |
| Gas Sensing | MQ-2 / MQ-135 (CO, CO₂, CH₄ detection) |
| Vision | Thermal camera (MLX90640), USB/CSI night-vision camera, analog camera (FPV) |
| Navigation | RPLIDAR A1 (360° scan), MPU6050 IMU, wheel encoder |
| Environment | DHT11 / DHT22 (temperature & humidity) |
| Mapping & Navigation | ROS 2 — SLAM Toolbox, Nav2 |
| AI / ML | YOLOv8 (Ultralytics) for human detection, OpenCV for crack detection, gas leakage prediction model |
| Communication | LoRa (data + photo alerts), 5.8 GHz analog FPV (live video) |
| Dashboard | Live map, gas/temperature/humidity display, human-detection alerts (phone / PC) |
| Power | Rechargeable Li-ion battery + 5V/12V voltage regulators |

---

## ✅ Feasibility & Viability

- **Technical:** Built entirely on low-cost, off-the-shelf components with proven open-source algorithms (ROS SLAM, YOLOv8). Modular design — gas, vision and mapping subsystems work independently, so one failure doesn't disable the rover.
- **Economic:** Estimated hardware cost **under ₹15,000 – ₹20,000 per unit** (vs. industrial rescue robots costing lakhs). Open-source software means zero licensing cost, and it scales to multiple units cheaply.
- **Operational:** Reduces risk to human rescuers, needs minimal training, and works in GPS-denied, low-visibility, toxic-gas environments.
- **Viability:** Directly addresses recurring mine accidents in India. Extensible to earthquakes, tunnel collapses and industrial disaster response. Aligns with Digital India / Make in India. Clear path to scale via pilots with mining companies (Coal India, SCCL).

### ⚠️ Challenges & Risks

| Challenge | Risk |
|---|---|
| Communication reliability — signal loss in deep tunnels | Loss of rover control or data |
| Environmental hazards — dust, smoke, heat | Sensor failure or overheating |
| Navigation complexity — GPS-denied mapping | Rover getting stuck or lost |

---

## 🌍 Impact & Benefits

- ❤️ **Direct life-saving impact** — faster rescue with thermal/night vision, rescuer protection by scouting toxic gas and collapse zones first, and explosion prevention via early gas alerts
- 🛡️ **Safety & risk reduction** — real-time crack detection, live SLAM mapping to replace outdated blueprints, data-driven decisions instead of risky manual guesses
- 💰 **Economic & social impact** — affordable for smaller mines, protects workers, builds public trust
- 🔁 **Versatile application** — earthquakes, building collapses, industrial accidents, petroleum refinery incidents

---

## 🔒 Safety & Design Principles

- **Rover scouts first** — humans enter only after hazard zones are assessed
- **Early warnings** — AI gas analysis alerts before levels turn dangerous
- **Photo alerts over live video on LoRa** — reliable, low-bandwidth, long-range data delivery
- **Modular subsystems** — failure in one module doesn't disable the rover
- **Human-in-the-loop** — assists rescue teams, does not replace them

---

## 📚 References

1. [NIOSH — Robotics Technology in Mine Disaster Reconnaissance, Rescue and Recovery](https://stacks.cdc.gov/view/cdc/227698)
2. [NIOSH — Guidelines for the Control and Monitoring of Methane Gas on Continuous Mining Operations](https://www.cdc.gov/niosh/publications/numbered/2010-141.html)
3. [NIOSH — Methane Monitoring](https://www.cdc.gov/niosh/engcontrols/ecd/detail161.html)
4. [ROS 2 — SLAM Toolbox Documentation](https://docs.ros.org/en/humble/p/slam_toolbox/)
5. [ROS 2 — Nav2 Navigation Concepts](https://docs.nav2.org/rolling/getting_started/navigation_concepts/)

## 🎥 Demo Video

[

![Watch Demo](https://img.shields.io/badge/▶_Watch-Demo_Video-red?style=for-the-badge)

](https://drive.google.com/file/d/1-2RmJU_kiQDHAJTdm3Bz9J0QpuEfmWQJ/view?usp=drivesdk)

Short walkthrough of our AI-powered mine safety rover: gas detection, survivor detection, live mapping and real-time alerts over LoRa.

🔗 **Link:** [Demo Video (Google Drive)](https://drive.google.com/file/d/1-2RmJU_kiQDHAJTdm3Bz9J0QpuEfmWQJ/view?usp=drivesdk)


---

## 📄 License

Apache-2.0

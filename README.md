# 🛡️ Aegis Vision — Safety Compliance Detector
### YOLOv8 · ByteTrack · OpenCV · Real-Time · Python · Self-Project

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Object_Detection-FF6F00?style=flat-square)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer_Vision-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![ByteTrack](https://img.shields.io/badge/ByteTrack-Object_Tracking-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Real--Time_Deployment-brightgreen?style=flat-square)

---

## 🧩 Problem Statement

Construction sites and factories require strict PPE (Personal Protective Equipment) compliance — but manual monitoring is expensive, error-prone, and unscalable. This project builds an **end-to-end real-time AI surveillance system** that automatically detects PPE violations and triggers intelligent alerts.

> *"Detect people in danger zones without helmets or vests → track them over time → trigger smart alerts — all in real-time on a live webcam feed."*

---

## 🎯 Key Features

| Feature | Detail |
|---|---|
| **Real-Time Detection** | YOLOv8 nano — optimized for speed + accuracy |
| **Object Tracking** | ByteTrack — assigns stable ID per person across frames |
| **Danger Zone** | User-defined polygon — alerts only where rules apply |
| **State Machine** | 4-state alert logic — prevents alert fatigue |
| **CSV Logging** | Every violation logged with timestamp and track ID |
| **Frame Saving** | Annotated violation frames saved automatically |
| **Cross-Platform** | Webcam + video file + static images supported |

---

## ⚙️ System Architecture

```
Live Webcam / Video Feed
        │
        ▼
YOLOv8 (CNN) — Object Detection
  ├── Detects: person, helmet, hardhat, vest
  └── Outputs: bounding boxes + class labels
        │
        ▼
ByteTrack — Object Tracking
  └── Assigns stable track_id per individual across frames
        │
        ▼
Danger Zone Check (OpenCV polygon test)
  └── Is person inside the restricted area?
        │
        ▼
PPE Compliance Check
  └── Is helmet/vest present in the same frame?
        │
        ▼
State Machine (per track_id)
  ├── PENDING   → violation detected, 30s grace period
  ├── ALARMING  → alarm triggered after 30s
  ├── REMINDING → reminder every 20s for 2 minutes
  └── TIMED_OUT → 30-min reminder if still in violation
        │
        ▼
Alert (alarm.wav) + CSV Log + Frame Saved
```

---

## 🧠 Three Core Components

### 1. YOLOv8 — The "Eyes"
Custom-trained YOLOv8 nano model on Roboflow PPE dataset. Chosen for optimal balance between **real-time inference speed** and **detection accuracy** on standard hardware.

### 2. ByteTrack — The "Memory"
Assigns a persistent `track_id` to each individual across consecutive frames. Without tracking, timing-based alerts are impossible — ByteTrack solves this by linking detections over time.

### 3. State Machine — The "Brain"
Custom Python state machine prevents **alert fatigue** — instead of constant alarms, each person's violation progresses through intelligent states based on precise timing rules.

```
pending → alarming → reminding → timed_out
  30s       10s        20s/2min     30min
```

---

## 📁 Repository Structure

```
📦 Aegis-Vision-Safety-Compliance-Detector/
├── main.py                  # Core detection + tracking + state machine
├── checkcamera.py           # Camera index finder utility
├── checkcameraloop.py       # Live camera stream test
├── start.bat                # Windows one-click launcher
├── requirements.txt         # Python dependencies
├── README.md
└── .gitignore
```

> **Note:** Model weights (`best.pt`) and output files not included. Download instructions below.

---

## 🚀 Getting Started

### Step 1 — Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 2 — Check Camera
```bash
python checkcamera.py
```

### Step 3 — Run Detector
```bash
python main.py
```

Or on Windows:
```bash
start.bat
```

---

## ⚙️ Configuration

Edit `main.py` to customize:

```python
INITIAL_DELAY_SECONDS = 30      # Grace period before first alarm
ALARM_DURATION_SECONDS = 10     # Duration of alarm sound
REMINDER_INTERVAL_SECONDS = 20  # Reminder frequency
REMINDER_WINDOW_SECONDS = 120   # Total reminder window
MAJOR_TIMEOUT_MINUTES = 30      # Long-term reminder interval
```

---

## 🧰 Tech Stack

| Component | Tool |
|---|---|
| Object Detection | YOLOv8 (Ultralytics) |
| Object Tracking | ByteTrack |
| Computer Vision | OpenCV |
| Numerical Computing | NumPy |
| Audio Alerts | Playsound |
| Logging | CSV + Python datetime |

---

## 🧠 Concepts Covered

`Computer Vision` · `Object Detection` · `Object Tracking` · `CNN` · `YOLOv8` · `ByteTrack` · `OpenCV` · `Real-Time Systems` · `State Machine` · `PPE Detection` · `Edge Deployment`

---

## 👤 Author

**Dhruv Kumar Sahu**
M.Tech, Industrial & Management Engineering — IIT Kanpur
GATE 2024 AIR 33 | [LinkedIn](https://www.linkedin.com/in/dhruv-kumar-sahu-157ab9193/) · [GitHub](https://github.com/dhruvkumar24-ai)

# People Flow Intelligence System  
### Real-Time Detection • Tracking • Counting • Heatmap Analytics (YOLOv11s + ByteTrack)

---

## 📌 Overview

This project is a computer vision pipeline that performs:

- Real-time people detection  
- Multi-object tracking  
- Directional IN/OUT counting  
- Movement heatmap generation  

It converts raw video into structured spatio-temporal intelligence.

---

## 🔄 System Pipeline

Video Input → YOLOv11s Detection → ByteTrack Tracking → Trajectory Analysis → Line Crossing Logic → Heatmap Generation → Output Video + CSV

---

## ✨ Key Features

- Real-time person detection using YOLOv11s  
- Multi-object tracking using ByteTrack  
- IN/OUT directional counting  
- Trajectory visualization  
- Heatmap generation of movement patterns  
- CSV logging of tracking data  

---

## 🎯 Detection Method

- Model: YOLOv11s (Ultralytics pretrained model)  
- Class: person (COCO dataset)  
- Confidence threshold: 0.3–0.5  

---

## 🧭 Tracking Method

- Algorithm: ByteTrack (Supervision library)  
- Maintains unique ID per person  
- Handles occlusion and re-identification  
- Ensures consistent tracking across frames  

---

## 🚦 Counting Logic (IN / OUT)

Two horizontal virtual lines:

- IN Line: `y = 69`  
- OUT Line: `y = 1008`  

### Rules:

- IN → Person moves downward crossing upper line  
- OUT → Person moves upward crossing lower line  
- Each ID is counted only once  

---

## 🔥 Heatmap Generation

- Extracts center points (cx, cy) of detections  
- Accumulates spatial movement density over time  
- Generates heatmap matrix and visualization video  

---

## 📤 Outputs

### Tracking Video
`people_yolov11s_tracked.mp4`

- Bounding boxes  
- Track IDs  
- Trajectories  
- IN/OUT counters  

### Heatmap Video
`heatmap_output.mp4`

- Movement density visualization  

### CSV File
`tracks.csv`

Includes:
- Frame number  
- Object ID  
- Center coordinates (cx, cy)  
- Confidence score  
- Bounding box coordinates  

---

## ▶️ How to Run

### Step 1: Download video

```bash
wget https://media.roboflow.com/supervision/video-examples/people-walking.mp4 -O people-walking.mp4

```

### Step 2: Run the Pipeline

```bash
python main.py

```

---

## Tech Stack

* **Core Language:** Python
* **Object Detection:** YOLOv11s (Ultralytics)
* **Tracking Framework:** ByteTrack (Supervision)
* **Image Processing:** OpenCV & NumPy
* **Data Logging:** Pandas

---

## Applications

* **Smart Surveillance Systems:** Enhanced security monitoring.
* **Crowd Analytics:** Density management at events or public spaces.
* **Retail Footfall Analysis:** Understanding customer movement trends.
* **Traffic Monitoring:** Pedestrian flow tracking at intersections.
* **Public Safety Systems:** Automated bottleneck and overcrowding detection.

---

## Future Improvements

* [ ] Multi-camera tracking system integration.
* [ ] Real-time web dashboard using Streamlit or FastAPI.
* [ ] Edge deployment support for NVIDIA Jetson Nano or Raspberry Pi.
* [ ] Behavior analysis algorithms (e.g., running, loitering detection).
* [ ] Advanced Feature Re-identification (ReID integration).

---

## Author

**Iqbal** *Mechanical Engineering | AI/ML Enthusiast* Focused on Deep Learning and Autonomous Systems.

---

## License

This project is licensed under the [MIT License](https://www.google.com/search?q=LICENSE).

```

```

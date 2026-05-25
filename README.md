👁️ People Flow Detection, Tracking & Heatmap System (YOLOv11 + ByteTrack)
📌 Overview

This project implements a real-time people detection, tracking, counting, and movement heatmap generation system using YOLOv8, ByteTrack, and Supervision.

It processes a video stream to:

Detect humans
Track unique individuals across frames
Count people crossing defined entry/exit lines
Generate trajectory visualization
Create a movement heatmap
Export annotated video + analytics data
🎯 Key Features
🔍 Real-time person detection using YOLO (Ultralytics)
🧠 Multi-object tracking using ByteTrack
🚶 IN/OUT counting using virtual boundary lines
🗺️ Movement heatmap generation
🎥 Annotated output video with overlays
📊 CSV logging of detection & tracking data
📍 Trajectory visualization per individual
🧠 Detection Method

We use the pre-trained YOLO (You Only Look Once) model from the ultralytics library.

Model used: yolo11s.pt (YOLO-based COCO pretrained weights)
Only the "person" class (class_id = 0) is considered
Confidence threshold: ≥ 0.3–0.5 (configurable)

YOLO performs single-stage object detection, enabling fast and accurate inference suitable for real-time video analysis.

🧾 Tracking Method (ByteTrack)

We use ByteTrack from the supervision library for multi-object tracking.

Why ByteTrack?
Maintains consistent identity IDs
Handles occlusion and re-appearance
Improves counting accuracy significantly

Each detected person is assigned a unique tracker_id across frames.

🚧 Counting Logic (IN / OUT System)

Two horizontal virtual lines are defined:

Upper Line (IN boundary): y = 69
Lower Line (OUT boundary): y = 1008
📥 IN Logic

A person is counted as IN when:

Their center point moves downward
Crosses from above to below the upper line
📤 OUT Logic

A person is counted as OUT when:

Their center point moves upward
Crosses from below to above the lower line
⚠️ Duplicate Prevention

Each tracker_id is counted only once using:

counted_ids_in
counted_ids_out
📍 Line Coordinates
Line Type	Coordinates
IN Line	(0, 69) → (1919, 69)
OUT Line	(0, 1008) → (1919, 1008)

Note: These are based on a 1920×1080 video and may need adjustment for other resolutions.

🗺️ Heatmap Generation

A heatmap is generated using accumulated center points of detected people.

Method:
Each detected person’s center (cx, cy) is recorded
A spatial intensity map is updated frame-by-frame
Final heatmap highlights high-density movement zones

Additionally, supervision.HeatMapAnnotator is used to create a visual overlay video.

📤 Output Files

The system generates:

🎥 1. Annotated Tracking Video
people_yolov11s_tracked.mp4

Includes:

Bounding boxes
Track IDs
Trajectories
IN/OUT counters
Counting lines
🗺️ 2. Heatmap Video
heatmap_output.mp4

Shows movement density visualization over time.

📊 3. Tracking Data (CSV)
tracks.csv

Contains:

Frame number
Object ID
Bounding box coordinates
Confidence scores
Center positions
🖼️ 4. Heatmap Image (Optional)
heatmap_raw.png / heatmap_overlay.png
⚙️ Installation

Install dependencies:

pip install ultralytics supervision opencv-python numpy matplotlib pandas

Enable GPU in Google Colab:

Runtime → Change Runtime Type → GPU
🚀 How to Run
1. Download video
wget https://media.roboflow.com/supervision/video-examples/people-walking.mp4 -O people-walking.mp4
2. Run detection pipeline

Execute the main script:

python main.py

or run in Colab notebook cell.

🧪 Model Workflow
Input Video
   ↓
YOLOv8 Detection (Person)
   ↓
ByteTrack Tracking (ID assignment)
   ↓
Trajectory + Line Crossing Logic
   ↓
Counting (IN / OUT)
   ↓
Heatmap Accumulation
   ↓
Output Video + CSV + Heatmap
📦 Tech Stack
🐍 Python
👁️ Ultralytics YOLO
🎯 ByteTrack (Supervision)
🎥 OpenCV
📊 NumPy, Pandas
📈 Matplotlib
📌 Applications
Smart surveillance systems
Crowd monitoring in public areas
Retail store analytics
Traffic and pedestrian flow analysis
Security automation systems
🔮 Future Improvements
Multi-camera tracking system
Real-time dashboard (Streamlit / FastAPI)
Re-identification (ReID) for long-term tracking
Edge deployment (Jetson Nano / Raspberry Pi)
Behavior classification (running, loitering, etc.)
👨‍💻 Author

Iqbal
Mechanical Engineering | AI/ML Enthusiast
Focus: Deep Learning, Autonomous Systems, Smart Surveillance

⭐ Acknowledgements
Ultralytics YOLO Team
Roboflow datasets
Supervision library contributors
OpenCV community
📜 License

This project is open-source and available under the MIT License.

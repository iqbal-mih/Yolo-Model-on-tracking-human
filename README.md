🧠 People Flow Intelligence System
Real-Time Detection • Tracking • Counting • Heatmap Analytics (YOLOv11 + ByteTrack)
🚀 Executive Summary

A production-style computer vision analytics pipeline that performs real-time people detection, multi-object tracking, directional flow counting, and spatial heatmap generation from video streams.

Built using YOLOv11 + ByteTrack, the system transforms raw video into structured intelligence:

Who is moving?
Where are they moving?
How many are entering/exiting?
Where are congestion hotspots?

This pipeline is designed for smart surveillance, crowd analytics, and autonomous monitoring systems.

🧩 System Architecture
Video Input
   ↓
YOLOv8 Object Detection
   ↓
ByteTrack Multi-Object Tracking
   ↓
Trajectory Reconstruction
   ↓
Line-Crossing Event Engine (IN / OUT)
   ↓
Spatio-Temporal Heatmap Engine
   ↓
Output Layer (Video + CSV + Heatmaps)
🎯 Key Capabilities
👁️ Detection
State-of-the-art YOLOv11s pretrained model
Focused on person class detection (COCO dataset)
Confidence-based filtering for robustness
🧭 Tracking
ByteTrack identity persistence
Handles occlusion, re-entry, and motion blur
Maintains consistent tracker_id per individual
🚶 Flow Intelligence (IN / OUT Engine)

Two virtual boundary lines define movement zones:

🔵 IN Line: y = 69
🟣 OUT Line: y = 1008
Event Logic:
IN Event: Downward crossing of upper boundary
OUT Event: Upward crossing of lower boundary

Each event is:

Timestamped
ID-locked (no double counting)
Direction-aware
🗺️ Spatio-Temporal Heatmap Engine

The system constructs a density field over time:

Extracts center points (cx, cy) of detections
Accumulates spatial frequency
Generates:
Raw heatmap matrix
Visual overlay heatmap video

This enables:

Identification of high-traffic zones and congestion hotspots.

📊 Outputs
🎥 1. Annotated Tracking Video

File: people_yolov8m_tracked.mp4

Includes:

Bounding boxes
Persistent IDs
Motion trajectories
IN/OUT counters
Virtual boundary visualization
🗺️ 2. Heatmap Video

File: heatmap_output.mp4

Displays:

Movement density visualization
Temporal crowd distribution patterns
📄 3. Structured Tracking Log

File: tracks.csv

Schema:

Field	Description
frame	Frame index
id	Unique tracker ID
cx, cy	Object center coordinates
conf	Detection confidence
x1,y1,x2,y2	Bounding box
🖼️ 4. Heatmap Images
heatmap_raw.png
heatmap_overlay.png
⚙️ Technical Stack
Layer	Technology
Detection	YOLOv8 (Ultralytics)
Tracking	ByteTrack (Supervision)
Video Processing	OpenCV
Analytics	NumPy, Pandas
Visualization	Supervision HeatMap + Matplotlib
🧠 Design Decisions
1. Why YOLOv11s?
Real-time inference capability
Strong small-object detection
Production-ready API (Ultralytics)
2. Why ByteTrack?
Robust identity preservation
Better than SORT/DeepSORT in crowded scenes
Minimal computational overhead
3. Why Center-Based Counting?
Reduces bounding box noise sensitivity
Stable trajectory representation
Improves line-crossing accuracy
4. Why Heatmap Accumulation?
Converts discrete detections → continuous spatial intelligence
Enables crowd density inference without re-training
📈 Performance Characteristics
⚡ Real-time capable (GPU-accelerated)
🎯 High tracking stability via ByteTrack
🧠 Robust against short occlusions
📉 Low false counting via ID filtering logic
📦 Installation
pip install ultralytics supervision opencv-python numpy pandas matplotlib
🚀 Execution Pipeline
Step 1 — Download Input Video
wget https://media.roboflow.com/supervision/video-examples/people-walking.mp4 -O people-walking.mp4
Step 2 — Run System
python main.py
🧪 Core Algorithm Flow
FOR each frame:
    Detect people (YOLOv8)
    Filter detections (person + confidence threshold)
    Assign tracking IDs (ByteTrack)
    
    FOR each tracked object:
        Compute center point
        Update trajectory buffer
        Check line-crossing events
        
        IF crossing detected AND not counted:
            Update IN/OUT counter
            
        Update heatmap accumulator
        Log to CSV

Write annotated frame to output video
📌 Real-World Applications
🏢 Smart surveillance systems
🛍️ Retail footfall analytics
🚦 Pedestrian traffic monitoring
🏟️ Stadium crowd analysis
🏙️ Urban planning intelligence systems
🔮 Future Enhancements
🔄 Multi-camera tracking fusion
🧠 Person re-identification (ReID integration)
📊 Real-time dashboard (Streamlit / FastAPI)
📡 Edge deployment (Jetson Nano / Raspberry Pi)
🤖 Behavioral analytics (loitering, running detection)
☁️ Cloud analytics pipeline (AWS/GCP)
👨‍💻 Author

Iqbal
Mechanical Engineering | AI & Computer Vision Engineer
Specialization: Deep Learning • Autonomous Systems • Intelligent Surveillance

🏁 License

This project is released under the MIT License.

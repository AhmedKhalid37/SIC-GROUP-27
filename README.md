# SIC-GROUP-27
Project Submission for Group 27 of the Samsung Innovation Campus

# AI-Powered Collision Avoidance System

### A Computer Vision Safety Controller for Autonomous Vehicles

## Overview
This project implements a **monocular vision-based collision avoidance system**. Using a single camera feed (simulated via dashcam images), the system detects vehicles, estimates their distance using geometric computer vision, and acts as a "Safety Logic Controller" to issue real-time driving commands (BRAKE, SLOW, SAFE).

The system addresses the challenge of depth perception in 2D images without expensive LiDAR hardware, providing a cost-effective safety solution for ADAS (Advanced Driver Assistance Systems).

## Key Features
* **Object Detection:** Utilizes **YOLOv8 Nano** for high-speed, accurate vehicle detection.
* **Distance Estimation:** Implements monocular distance calculation logic based on focal length and pixel width.
* **Safety Logic Controller:**
    * **VC (Very Close):** Triggers **BRAKE** (< 15m).
    * **C (Close):** Triggers **SLOW** (< 45m).
    * **N (Normal):** Status **SAFE** (> 45m).
* **Lane Filtering:** Intelligent logic to **IGNORE** vehicles in adjacent lanes (Code "O").
* **Enhanced Visualization:** Custom Pillow (PIL) rendering for clear, stacked text annotations ("O" on top, "IGNORE" below).

## Tech Stack
* **Language:** Python 3.x
* **Computer Vision:** OpenCV (cv2), Pillow (PIL)
* **AI/ML Model:** Ultralytics YOLOv8 (yolov8n.pt)
* **Visualization:** Matplotlib

## Installation

1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/yourusername/collision-avoidance-system.git](https://github.com/yourusername/collision-avoidance-system.git)
    cd collision-avoidance-system
    ```

2.  **Install Dependencies**
    Ensure you have Python installed, then run:
    ```bash
    pip install ultralytics opencv-python matplotlib pillow numpy
    ```

## Usage

1.  **Prepare your Data:**
    Place your dashcam images in a folder (e.g., images/) or ensure they are linked in your environment (e.g., Kaggle Input).

2.  **Run the Script:**
    Execute the main Python script (or run the Jupyter Notebook):
    ```bash
    python sic_27.py
    ```

3.  **View Results:**
    The script will process random frames from the dataset and display the annotated output with safety labels.

## How It Works

### 1. Object Detection
The system uses YOLOv8n to identify objects with class IDs [2, 3, 5, 7] (Car, Motorcycle, Bus, Truck).

### 2. Distance Calculation
We use the inverse relationship between object width in pixels and distance in meters:
D = (W * F) / P
* **D**: Distance (meters)
* **W**: Real Width of Vehicle (Standardized to 1.8m)
* **F**: Focal Length (Calibrated to 1200)
* **P**: Width in Pixels

### 3. Decision Logic
* **Lane Filter:** Objects outside the center 40% of the image frame are flagged as **IGNORE**.
* **Braking thresholds:**
    * **Red Zone (<15m):** Immediate Stop.
    * **Yellow Zone (15-45m):** De-accelerate/slowdown .
    * **Green Zone (>45m):** Safe, continue cruising.

## Future Improvements
* Integration with **Lane Line Detection** (Hough Transform) for curved roads.
* Implementation of **Object Tracking** (DeepSORT) for relative speed estimation.
* Deployment on edge devices like **Raspberry Pi** or **NVIDIA Jetson**.

## Team
* **Ahmed Khalid**
* **Mariam nidal abdullah**
* **Abdullah Moosa**
* **Sarah Ateeq**

## License
This project is for educational purposes as part of the Samsung Innovation Campus, Capestone Project.

AstroShield 🚀🛡️
AstroShield is a comprehensive computer vision application that leverages YOLOv8 Object Detection to identify and monitor critical safety equipment and hazards. Designed with a deep-space aesthetic, the web interface allows users to upload images or stream webcam footage to instantly detect objects like oxygen tanks, fire extinguishers, and first aid boxes.

Features
Real-Time Object Detection: Upload images or use webcam feed for instant predictions.
7 Critical Safety Classes: Detects OxygenTank, NitrogenTank, FirstAidBox, FireAlarm, SafetySwitchPanel, EmergencyPhone, and FireExtinguisher.
YOLOv8 Powered: Built on the state-of-the-art Ultralytics YOLOv8 architecture for fast and accurate inference.
Flask Backend & API: A robust Python backend handling model inference and serving RESTful APIs.
Interactive Web UI: A beautifully designed, highly interactive frontend featuring a space-themed UI with particle effects and smooth animations.
Integrated Retraining Pipeline: Built-in scripts and instructions to easily finetune or retrain the model on new data.
Advanced Post-Processing: Capable of filtering overlapping detection boxes for precise localized results.
Tech Stack
Backend: Python, Flask, Werkzeug, Gunicorn
Computer Vision: Ultralytics (YOLOv8), PyTorch, OpenCV
Frontend: HTML5, CSS3 (Custom animations, glassmorphism), Vanilla JavaScript, Chart.js
Environment Management: Conda / Pip
Project Structure
AstroShield_project/
├── app/                    # Flask Application
│   ├── templates/          # Contains index.html (Web UI)
│   ├── backend.py          # Flask app initialization and CORS setup
│   ├── routes.py           # API endpoints and route definitions
│   └── routes_training.py  # Training-specific API endpoints
├── src/                    # Core Logic
│   ├── detect.py           # YOLO inference and post-processing logic
│   └── train.py            # Model training utilities
├── models/                 # Saved models and training logs
├── data/                   # Dataset directory for training/validation
├── best.pt                 # Deployed YOLOv8 weights
├── start_server.py         # Entry point to run the web server
├── retrain_model.py        # Script to fine-tune the model
├── requirements.txt        # Python dependencies
├── environment.yaml        # Conda environment definition
└── ...                     # Evaluation and utility scripts
Setup & Installation
Follow these steps to set up AstroShield locally:

1. Clone or Download the Repository
Make sure you are in the project root directory.

2. Create the Environment
Using Conda (Recommended):

conda env create -f environment.yaml
conda activate observo
pip install -r requirements.txt
Using pip:

python -m venv venv
venv\Scripts\activate  # On Windows
pip install -r requirements.txt
Running the Application
To start the AstroShield backend server and Web UI:

# Ensure your environment is active
python start_server.py
The server will start on port 10000 (by default). Open your web browser and navigate to: http://localhost:10000

Retraining the Model
If you find that the model is misclassifying certain objects, or if you want to expand the dataset, you can initiate a retraining process:

Add Data: Ensure your new training images and labels are placed correctly within data/raw/train/images and data/raw/train/labels.
Run the Script:
conda activate observo
python retrain_model.py
Monitor Progress: Training logs are outputted to the console and saved inside models/logs/yolov8_astroshield/.
Deploy: Once complete, the updated model is automatically saved to models/weights/best.pt. Restart your server to load the new weights.
For full step-by-step instructions, see RUN_RETRAINING.md.

API Endpoints
The Flask backend exposes several endpoints for seamless frontend integration:

GET / - Serves the main SPA interface.
POST /predict - Primary detection endpoint. Accepts image uploads, runs inference, and returns bounded boxes with confidence scores.
POST /api/detect - Advanced detection endpoint offering filtered overlapping bounding boxes.
GET /api/health - Basic server health check.
GET /api/statistics - Provides dataset statistics and class distribution for rendering charts on the frontend.

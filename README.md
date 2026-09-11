
# Real-Time ISL Translator

A real-time Indian Sign Language (ISL) translator that uses a webcam to recognize sign language gestures and convert them into text and speech.

## About the Project

This project is designed to recognize Indian Sign Language gestures from a live webcam feed.

The system processes the video frames, detects the person, extracts hand, face, and body landmarks, and then uses a CNN-LSTM model to predict the sign.

The overall workflow is:

```text
Webcam
   ↓
YOLOv11
   ↓
MediaPipe Holistic
   ↓
Landmark Extraction
   ↓
CNN + LSTM
   ↓
Sign Prediction
   ↓
Text
   ↓
Speech
```

## Features

* Real-time sign recognition using a webcam
* Indian Sign Language gesture recognition
* YOLOv11 for person detection
* MediaPipe Holistic for landmark extraction
* CNN-LSTM based sign classification
* FastAPI backend
* WebSocket-based real-time communication
* Text-to-Speech output

## Technologies Used

| Technology          | Purpose                   |
| ------------------- | ------------------------- |
| Python              | Main programming language |
| PyTorch             | Deep learning             |
| YOLOv11             | Person detection          |
| MediaPipe Holistic  | Landmark extraction       |
| CNN                 | Feature extraction        |
| LSTM                | Sequence processing       |
| FastAPI             | Backend server            |
| WebSockets          | Real-time communication   |
| HTML/CSS/JavaScript | Frontend                  |
| Web Speech API      | Text-to-Speech            |

## How It Works

### 1. Webcam Input

The webcam captures the sign language performed by the user.

### 2. Person Detection

YOLOv11 is used to detect the person in the video frame and obtain the required region for further processing.

### 3. Landmark Extraction

MediaPipe Holistic extracts landmarks from the detected person.

The extracted landmarks include:

* Face landmarks
* Left-hand landmarks
* Right-hand landmarks
* Pose landmarks

### 4. Sequence Creation

Landmarks from consecutive frames are collected into a sequence.

Using a sequence instead of a single frame helps the model understand the movement involved in a sign.

### 5. CNN-LSTM Model

The landmark sequence is passed to the CNN-LSTM model.

The CNN extracts useful features from the landmark data, while the LSTM processes the sequence and captures temporal information.

### 6. Sign Prediction

After processing the required number of frames, the model predicts the corresponding sign.

The prediction is then sent to the web application.

### 7. Text and Speech

The predicted sign is displayed as text. The text can also be converted into speech using the browser's Text-to-Speech functionality.

## Project Structure

```text
Real-Time-ISL-Translator/
│
├── inference/
│
├── models/
│
├── notebooks/
│
├── scripts/
│
├── src/
│
├── web_app/
│   ├── static/
│   │   └── index.html
│   │
│   ├── app_ws.py
│   └── model_def.py
│
├── .gitignore
├── CHALLENGES_AND_FUTURE.md
├── README.md
├── WORKFLOW_DIAGRAM.md
├── requirements.txt
└── training_history.csv
```

## Requirements

Before running the project, make sure the following are installed:

* Python 3.9
* Conda
* Webcam
* Required Python packages

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Khushi-Keshari/Real-Time-ISL-Translator.git
```

### 2. Open the Project Directory

```bash
cd Real-Time-ISL-Translator
```

### 3. Create the Conda Environment

```bash
conda create -n isl-speech python=3.9
```

### 4. Activate the Environment

```bash
conda activate isl-speech
```

### 5. Install Dependencies

```bash
pip install -r requirements.txt
```

## Model Files

The required model files should be available in the `models` directory.

Example:

```text
models/
├── yolo11n.pt
└── best_web_model.pth
```

* `yolo11n.pt` - YOLOv11 model weights
* `best_web_model.pth` - trained CNN-LSTM model

## Running the Project

Start the FastAPI server:

```bash
uvicorn web_app.app_ws:app --reload
```

After starting the server, open the following address in your browser:

```text
http://localhost:8000
```

Allow the browser to access your webcam and start the camera.

## Controls

| Control           | Function                               |
| ----------------- | -------------------------------------- |
| `s`               | Start/reset the prediction sequence    |
| `r`               | Reset the sequence                     |
| Speak Translation | Convert the predicted text into speech |

## Model

The project uses a CNN-LSTM based architecture.

The CNN is used to extract features from the landmark data. The LSTM then processes the sequence of features and learns the temporal information from the sign.

This is useful for sign language recognition because the movement of the hands and body over a number of frames can be important for identifying a sign.

## Limitations

The current system has some limitations:

* Recognition may be affected by poor lighting.
* Hand or body occlusion can affect landmark extraction.
* Different users may perform the same sign differently.
* Recognition is limited to the signs available in the training data.
* Background and camera position can affect detection.
* The system does not cover the complete Indian Sign Language vocabulary.

## Future Improvements

The project can be further improved by:

* Increasing the number of supported ISL signs
* Using a larger and more diverse dataset
* Improving recognition accuracy
* Supporting continuous sentence recognition
* Improving real-time inference speed
* Supporting multiple languages for speech output
* Improving recognition under different lighting conditions
* Handling partially visible hands and body parts more effectively
* Deploying the application for easier access

## Applications

This project can be useful for:

* Sign language learning
* Accessibility applications
* Communication assistance
* Educational applications
* Human-computer interaction
* Sign language recognition research

## Author

[**Khushi Keshari**](https://github.com/Khushi-Keshari)

## Acknowledgements

This project uses the following open-source technologies:

* [PyTorch](https://pytorch.org/)
* [Ultralytics YOLO](https://www.ultralytics.com/)
* [MediaPipe](https://mediapipe.dev/)
* [FastAPI](https://fastapi.tiangolo.com/)


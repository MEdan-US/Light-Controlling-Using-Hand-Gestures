# Hand Gesture Light Control System

This project implements a **Real-time Hand Gesture Recognition** system using **Computer Vision** and **Deep Learning**. It detects hand landmarks via a webcam to control a simulated lighting interface and can be integrated with physical hardware via the Modbus protocol.

## 🚀 Key Features
* **Hand Landmark Detection:** Uses **MediaPipe** to extract 21 3D hand coordinates.
* **Gesture Classification:** A custom **PyTorch Neural Network** (MLP) classifies gestures based on landmark spatial data.
* **Interactive Simulation:** A visual interface built with **OpenCV** to show real-time light status (On/Off).
* **Industrial Integration:** Supports **Modbus Master** communication to control real-world actuators or PLCs.

## 📁 Project Structure
```text
.
├── model/                # Trained model weights (.pth files)
├── controller.py         # Modbus Master implementation for hardware control
├── detect_simulation.py  # Main execution script (Inference & UI)
├── hand_gesture.yaml     # Configuration file for gesture labels
└── README.md             # Project documentation

💻 How to Run
1. Model Configuration
Ensure your trained model is placed in the ./model/ directory. Open detect_simulation.py and verify the model_path at the bottom of the file:

Python
if __name__ == "__main__":
    model_path = "./model/model_06-04 03_10_NeuralNetwork_last"
    # ...
2. Execution
Run the main simulation script from your terminal:

PowerShell
python detect_simulation.py
3. Controls & Gestures
The system recognizes gestures based on the labels in hand_gesture.yaml. Show your hand to the webcam to trigger:

light1 / light2 / light3: Toggle specific individual virtual lights.

turn_on: Switches all 3 lights ON simultaneously.

turn_off: Switches all 3 lights OFF simultaneously.

undefined command: Triggered when a gesture is detected but doesn't match a command.

🧠 Technical Overview
Hand Landmark Detection
The system uses MediaPipe Hands to extract 21 landmarks (each with X, Y, Z coordinates). This 63-dimensional vector is then flattened and fed into the classifier.

Neural Network Architecture
A Multi-Layer Perceptron (MLP) built with PyTorch:

Input: 63 features.

Hidden Layers: Linear layers with 128 units, followed by ReLU activation, BatchNorm, and Dropout (0.4 - 0.6) to prevent overfitting.

Output: Multi-class classification based on your gesture set.

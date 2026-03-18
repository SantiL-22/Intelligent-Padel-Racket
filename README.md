# Smart Padel Racket

A system that classifies padel strokes in real-time using IMU sensors (accelerometer + gyroscope) mounted on the racket and machine learning.

## How it works

1. An **Arduino with an IMU sensor** captures movement data from the racket.
2. Models are trained using **TensorFlow** to classify the strokes.
3. The model is converted to **TFLite** and exported as a C header file (`model.h`) to run directly on the Arduino.
4. An **iOS app** connects to the Arduino via Bluetooth and displays real-time statistics.

### Classified Strokes

| Stroke | Description |
|--------|-------------|
| Forehand | Standard forehand stroke (Drive) |
| Backhand | Standard backhand stroke (Revés) |
| Smash | Powerful overhead shot |
| Bandeja | High defensive overhead shot |

## Repository Structure

```text
Smart-Padel-Racket/
├── training/
│   ├── Padel detection.ipynb      # Stroke detection notebook
│   ├── Arduino_Exercise.ipynb     # Pipeline: data → TensorFlow → TFLite → Arduino
│   ├── Padel_Data/                # Sensor CSV datasets
│   │   ├── drive.csv
│   │   ├── reves.csv
│   │   ├── smash.csv
│   │   ├── bandeja.csv
│   │   └── ruido.csv
│   └── Arduino_Code/
│       ├── Capture_Data/          # Arduino sketch to capture IMU data
│       └── IMU_Classifier/        # Arduino sketch for inference + model.h
├── images/                        # iOS app screenshots
└── README.md
```

## Model Training

The notebooks are located in `training/`:

- **`Padel detection.ipynb`** — Exploration and training of the stroke detection model.
- **`Arduino_Exercise.ipynb`** — Complete pipeline: loading CSVs → training with TensorFlow → conversion to TFLite → export to `model.h` for Arduino.

The training data (`training/Padel_Data/`) consists of accelerometer and gyroscope readings captured using the `Capture_Data.ino` sketch.

## iOS App

The app is developed in SwiftUI and connects to the Arduino via Bluetooth Low Energy (BLE). It has three screens: Dashboard, Statistics, and History.

If you would like to see the app's source code, feel free to contact me.

<p align="center">
  <img src="images/dashboard.png" width="250" />
  <img src="images/stats.png" width="250" />
  <img src="images/historial.png" width="250" />
</p>

## Requirements

- **Arduino:** Arduino Nano 33 BLE Sense (or compatible with IMU), Arduino IDE
- **Training:** Python 3.x, TensorFlow, pandas, numpy
- **App:** Xcode 16+, iOS 17+

## Author

Santi López

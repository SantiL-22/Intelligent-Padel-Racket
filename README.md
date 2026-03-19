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
  <img src="https://private-user-images.githubusercontent.com/235075880/565519779-4b352bc3-aa44-416d-af21-4f1706b65b27.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzM4MzM4NTUsIm5iZiI6MTc3MzgzMzU1NSwicGF0aCI6Ii8yMzUwNzU4ODAvNTY1NTE5Nzc5LTRiMzUyYmMzLWFhNDQtNDE2ZC1hZjIxLTRmMTcwNmI2NWIyNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMzE4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDMxOFQxMTMyMzVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jNGY0NzU2OWJmMzk4N2VlMTc1MTY4MWJlMDk3MDlhMzJjYzJiZmE4MGY0NDM1MWY5YTIxZGVkNWViYWFkMDAwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.lp1xhm8RJA7V1fLzf11oC2x4tOhiQeXvdaqkbsWnKVE" width="250" />
  <img src="https://private-user-images.githubusercontent.com/235075880/565519780-92593010-dd54-4360-bcd6-85e7f93688cd.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzM4MzM5NDAsIm5iZiI6MTc3MzgzMzY0MCwicGF0aCI6Ii8yMzUwNzU4ODAvNTY1NTE5NzgwLTkyNTkzMDEwLWRkNTQtNDM2MC1iY2Q2LTg1ZTdmOTM2ODhjZC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMzE4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDMxOFQxMTM0MDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hOGEzYzI0MDBjNjExMDdiYWRiNDQ0Mjk4MDVlMmVmNThiZWE0MGIwY2M3M2RkYzdlMjM2NDQzYWE0OTYwMmM1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.pTjhPwM-_2hFHrIT9EXSNC2LzHplUxOs3DDh2AUV8VM" width="250" />
  <img src="https://private-user-images.githubusercontent.com/235075880/565519778-02c9ea42-921d-4be2-bc69-f77e0563e7fe.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzM4MzM5NDAsIm5iZiI6MTc3MzgzMzY0MCwicGF0aCI6Ii8yMzUwNzU4ODAvNTY1NTE5Nzc4LTAyYzllYTQyLTkyMWQtNGJlMi1iYzY5LWY3N2UwNTYzZTdmZS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMzE4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDMxOFQxMTM0MDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03YTExMTdjMTI4N2E0N2U0MjRmMGJkNmEyZjk1YmU2Nzc0YjM4OWFhMzQ3MjJhMmU3MDJmMzg2ODU4OTNjNjBkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Pzwfewx7y_hKiUKWLAmc8fV3eEILcQpR0S1gaGqzxow" width="250" />
</p>

## Requirements

- **Arduino:** Arduino Nano 33 BLE Sense (or compatible with IMU), Arduino IDE
- **Training:** Python 3.x, TensorFlow, pandas, numpy
- **App:** Xcode 16+, iOS 17+

## Author

Santi López

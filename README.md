# Smart Padel Racket

Sistema que clasifica golpes de pádel en tiempo real usando sensores IMU (acelerómetro + giroscopio) montados en la pala y machine learning.

## Cómo funciona

1. Un **Arduino con sensor IMU** captura datos de movimiento de la pala
2. Se entrenan modelos con **TensorFlow** para clasificar los golpes
3. El modelo se convierte a **TFLite** y se exporta como header C (`model.h`) para ejecutarse directamente en el Arduino
4. Una **app iOS** se conecta por Bluetooth al Arduino y muestra estadísticas en tiempo real

### Golpes clasificados

| Golpe | Descripción |
|-------|-------------|
| Drive | Golpe de derecha |
| Revés | Golpe de revés |
| Smash | Remate |
| Bandeja | Golpe defensivo alto |

## Estructura del repo

```
Smart-Padel-Racket/
├── training/
│   ├── Padel detection.ipynb      # Notebook de detección de golpes
│   ├── Arduino_Exercise.ipynb     # Pipeline: datos → TensorFlow → TFLite → Arduino
│   ├── Padel_Data/                # Datasets CSV de sensores
│   │   ├── drive.csv
│   │   ├── reves.csv
│   │   ├── smash.csv
│   │   ├── bandeja.csv
│   │   └── ruido.csv
│   └── Arduino_Code/
│       ├── Capture_Data/          # Sketch Arduino para capturar datos del IMU
│       └── IMU_Classifier/        # Sketch Arduino para inferencia + model.h
├── images/                        # Capturas de la app iOS
└── README.md
```

## Entrenamiento del modelo

Los notebooks están en `training/`:

- **`Padel detection.ipynb`** — Exploración y entrenamiento del modelo de detección de golpes
- **`Arduino_Exercise.ipynb`** — Pipeline completo: carga de CSVs → entrenamiento con TensorFlow → conversión a TFLite → exportación a `model.h` para Arduino

Los datos de entrenamiento (`training/Padel_Data/`) son lecturas de acelerómetro y giroscopio capturadas con el sketch `Capture_Data.ino`.

## App iOS

La app está desarrollada en SwiftUI y se conecta al Arduino vía Bluetooth Low Energy (BLE). Tiene tres pantallas: Dashboard, Estadísticas e Historial.

Si quieres ver el código de la app, contáctame.

<p align="center">
  <img src="images/dashboard.png" width="250" />
  <img src="images/stats.png" width="250" />
  <img src="images/historial.png" width="250" />
</p>

## Requisitos

- **Arduino:** Arduino Nano 33 BLE Sense (o compatible con IMU), Arduino IDE
- **Entrenamiento:** Python 3.x, TensorFlow, pandas, numpy
- **App:** Xcode 16+, iOS 17+

## Autor

Santi López

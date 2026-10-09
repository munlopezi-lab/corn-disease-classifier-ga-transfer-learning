# Clasificación de Enfermedades en Cultivos de Maíz mediante Transfer Learning y Algoritmos Genéticos

## Descripción

Este proyecto aborda la clasificación automática de enfermedades en cultivos de maíz utilizando **Transfer Learning** con **EfficientNetB0** y la optimización de hiperparámetros mediante **algoritmos genéticos** con **PyGAD**.

El flujo de trabajo se divide en cinco etapas principales organizadas en notebooks de Jupyter:
1. Extracción y estructuración de imágenes del dataset PlantVillage.
2. Extracción de características de alta dimensión mediante un modelo preentrenado (EfficientNetB0).
3. Entrenamiento y evaluación de un modelo base (Baseline).
4. Optimización evolutiva de arquitectura e hiperparámetros de la red neuronal mediante algoritmos genéticos.
5. Construcción del clasificador final y funciones de inferencia para nuevas imágenes.

El objetivo es lograr un sistema robusto y altamente preciso para la detección temprana de patologías agrícolas.

---

## Objetivos

- Estructurar y preprocesar un conjunto de datos agrícola para clasificación de imágenes.
- Utilizar Transfer Learning con EfficientNetB0 como extractor de características avanzado.
- Implementar y evaluar un modelo base de referencia (Baseline).
- Aplicar algoritmos genéticos para optimizar hiperparámetros clave de la red neuronal.
- Comparar el rendimiento del modelo optimizado frente al baseline.
- Proveer una interfaz de inferencia para clasificar nuevas imágenes de cultivos de maíz.

---

## Dataset

Se utilizó el dataset **PlantVillage** enfocado en cultivos de maíz (*Corn / Maíz*), estructurado en conjuntos de entrenamiento, validación y prueba.

### Características

- Imágenes en formato RGB.
- Resolución normalizada para EfficientNetB0 (224 × 224 píxeles).
- 4 clases principales de diagnóstico fitosanitario.

### Clases

- **Cercospora**: Mancha foliar por Cercospora (*Cercospora leaf spot*).
- **Roya**: Roya común del maíz (*Common rust*).
- **Tizón**: Tizón foliar del norte (*Northern leaf blight*).
- **Sana**: Hojas sanas de maíz (*Healthy*).

---

# Extracción y Preparación de Imágenes

## Descripción

El primer paso del pipeline consiste en organizar y estructurar el conjunto de datos de origen (PlantVillage) en directorios limpios y particionados para entrenamiento, validación y prueba, asegurando una distribución adecuada para el aprendizaje automático.

---

# Extracción de Características

## Descripción

Se utilizó la arquitectura **EfficientNetB0** preentrenada en el dataset ImageNet (sin incluir las capas densas superiores, `include_top=False`) para transformar las imágenes en vectores densos de características de 1280 dimensiones.

Este enfoque reduce significativamente el costo computacional del entrenamiento posterior y aprovecha representaciones visuales altamente robustas aprendidas a gran escala.

---

# Modelo Base (Baseline)

## Descripción

Como punto de referencia inicial se implementó una red neuronal densa conectada a las características extraídas por EfficientNetB0.

La arquitectura base incluye:
- Capas densas con activación ReLU.
- Tasa de Dropout para regularización.
- Capa de salida con activación Softmax para clasificación multiclase.

Este modelo alcanzó una exactitud del **97.69%** en el conjunto de prueba.

---

# Optimización mediante Algoritmos Genéticos

## Descripción

Se implementó la biblioteca **PyGAD** para optimizar automáticamente los hiperparámetros de la red de clasificación (número de neuronas, tasa de aprendizaje, función de activación y tasa de dropout).

Cada individuo en la población representa una combinación de hiperparámetros evaluada mediante una función de aptitud basada en el accuracy de validación.

---

## Hiperparámetros Optimizados

Entre los parámetros ajustados evolutivamente se encuentran:
- Tasa de aprendizaje (*Learning Rate*).
- Número de neuronas en la capa densa.
- Función de activación.
- Tasa de Dropout.

---

## Resultados

El modelo optimizado y seleccionado mediante el algoritmo genético alcanzó los siguientes resultados en el conjunto de prueba:

| Métrica | Valor |
|----------|----------|
| Accuracy | 0.9831 |
| Loss | 0.0779 |

---

## Análisis de Resultados

Los resultados demuestran que la combinación de Transfer Learning con EfficientNetB0 y la optimización evolutiva de hiperparámetros permite superar el modelo de referencia, alcanzando una precisión superior al **98%** en la clasificación de patologías en hojas de maíz.

La matriz de confusión y las métricas por clase muestran un equilibrio excelente entre precisión y sensibilidad para todas las categorías evaluadas.

---

# Clasificador Final e Inferencia

## Descripción

El último módulo consolida el mejor modelo guardado (`mejor_modelo_maiz.keras`) y define funciones robustas de inferencia (`predict_image`) para cargar, preprocesar y clasificar nuevas imágenes aportadas por el usuario, retornando la clase estimada y el nivel de confianza.

---

## Tecnologías Utilizadas

- Python
- TensorFlow
- Keras
- PyGAD
- NumPy
- Matplotlib
- Scikit-Learn
- Seaborn

---

## Estructura del Proyecto

```text
.
├── Clasificador_final.ipynb
├── Evolucion_geneticaCNN.ipynb
├── LICENSE
├── Maiz_base_line.ipynb
├── README.md
├── extraer_imagenes.ipynb
└── extractor_caracteristicas.ipynb
```

---

## Aprendizajes

Durante este proyecto se aplicaron conceptos avanzados de:
- Transfer Learning con EfficientNet.
- Extracción y almacenamiento de características con NumPy.
- Redes Neuronales Profundas (DNN).
- Optimización evolutiva mediante Algoritmos Genéticos (PyGAD).
- Clasificación de imágenes agrícolas.
- Evaluación y métricas de rendimiento en Machine Learning.

---

## Trabajo Futuro

Posibles extensiones y mejoras para el proyecto:
- Ampliar el dataset con más categorías de enfermedades del maíz.
- Experimentar con arquitecturas base más potentes (EfficientNetB2, ResNet50).
- Aplicar técnicas de aumento de datos (*data augmentation*) en tiempo real.
- Desarrollar una aplicación web o móvil para diagnóstico en campo.

---

## Autor

Jairo Isaac Muñoz López

Estudiante de Licenciatura en Matemáticas Aplicadas.

GitHub: https://github.com/munlopezi-lab

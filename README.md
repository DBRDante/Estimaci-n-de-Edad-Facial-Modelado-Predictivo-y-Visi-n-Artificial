<img width="921" height="269" alt="image" src="https://github.com/user-attachments/assets/38e789a9-e7b1-43f6-89c5-bf452d374b52" />

# Estimación de Edad Facial para Cumplimiento Normativo en la Venta de Alcohol: Modelado Predictivo y Visión Artificial

## Problema
En la cadena de supermercados Good Seed, garantizar el cumplimiento estricto de las normativas de venta de alcohol mediante la prohibición a menores de edad es un desafío operativo crítico. Las tiendas están equipadas con cámaras en el área de pago que se activan automáticamente al registrar la compra de este producto.  
El objetivo de este proyecto es construir y evaluar un modelo de visión artificial capaz de predecir con precisión la edad cronológica de una persona a partir de su fotografía facial, sirviendo como una herramienta preventiva de apoyo para el personal de cajas.

---

## Datos
El análisis utilizó un conjunto de datos compuesto por metadatos y registros fotográficos procesados mediante las siguientes etapas:
- **Volumen del corpus:** 7,591 imágenes de rostros emparejadas con sus respectivas etiquetas de edad real (`real_age`) (5,693 para entrenamiento y 1,898 para validación/prueba).
- **Flujo de datos:** Implementación de generadores dinámicos (`ImageDataGenerator`) con aumentación estocástica (volteo horizontal, rotaciones y desplazamientos) para el entrenamiento y preprocesamiento estandarizado con la función de ResNet50.

---

## Enfoque
El proyecto siguió una metodología estructurada de Deep Learning y visión artificial:
- Análisis exploratorio de datos (EDA) para examinar la integridad del corpus, la distribución demográfica y los riesgos operativos en el umbral legal de los 18 años.
- Implementación de *Transfer Learning* utilizando la red **ResNet50** pre-entrenada en ImageNet como modelo base (*backbone*), aplicando *fine-tuning* selectivo en las últimas capas.
- Construcción de un cabezal de regresión personalizado con *Global Average Pooling*, una capa densa de 128 neuronas (activación ReLU), regularización *Dropout* (0.3) y una capa de salida lineal.
- Optimización mediante el algoritmo Adam, optimizando la función de pérdida de Error Absoluto Medio (MAE) y utilizando *callbacks* (`EarlyStopping` y `ModelCheckpoint`) para guardar el mejor artefacto (`best_model.h5`).

---

## Resultados Clave del Rendimiento
El modelo completó el ciclo de entrenamiento mostrando una convergencia sólida y estable desde la primera época hasta alcanzar su punto óptimo en la **Época 20**:
- **Mejor Error Absoluto Medio de Validación (Val MAE):** **7.54** (exactamente 7.5385 años)
- **Umbral de Éxito del Proyecto:** $\le 8.0$ años (Objetivo superado con éxito).
- **Estado de Finalización:** El algoritmo de *Early Stopping* restauró de manera óptima los pesos correspondientes al mejor rendimiento de la época 20.

### Evolución del Entrenamiento (Progreso por Épocas):
| Época | Pérdida de Entrenamiento (Loss) | MAE de Entrenamiento | Pérdida de Validación (Val Loss) | Val MAE (Métrica Principal) |
| :---: | :---: | :---: | :---: | :---: |
| **01 / 20** | 22.51 | 22.51 | 22.80 | 22.80 |
| **05 / 20** | 7.69 | 7.69 | 8.05 | 8.05 |
| **10 / 20** | 6.56 | 6.56 | 7.68 | 7.68 |
| **15 / 20** | 6.06 | 6.06 | 7.65 | 7.65 |
| **20 / 20 (Óptimo)** | **5.54** | **5.54** | **7.54** | **7.54** |

---

## Evaluación del Rendimiento y Análisis de Inferencia
La ejecución de la evaluación sobre el conjunto de validación utilizando el artefacto persistido (`best_model.h5`) permite verificar la estabilidad y generalización del modelo entrenado en un entorno de inferencia independiente.

* **Métrica Final Obtenida:** Se registró un Error Absoluto Medio (MAE) de **7.5385 años**, cumpliendo rigurosamente con el umbral de éxito establecido ($\le 8.0$ años).
* **Contraste Empírico:** Las predicciones generadas sobre muestras específicas del conjunto de validación permiten observar el comportamiento del estimador frente a diferentes perfiles:
  * Instancia 1 -> Edad Real: 50 | Edad Estimada: 40.2
  * Instancia 2 -> Edad Real: 41 | Edad Estimada: 22.7
  * Instancia 3 -> Edad Real: 46 | Edad Estimada: 34.1
  * Instancia 4 -> Edad Real: 85 | Edad Estimada: 90.6
  * Instancia 5 -> Edad Real: 14 | Edad Estimada: 21.0

---

## Conclusiones y Evaluación del Impacto de Negocio

### 1. Desempeño del Modelo y Resultados Obtenidos
Tras la ejecución de la fase de validación utilizando el artefacto optimizado (`best_model.h5`), el modelo de regresión basado en ResNet50 alcanzó un **Error Absoluto Medio (MAE) de 7.54 años**. Este resultado cumple satisfactoriamente con el umbral de éxito establecido ($\le 8.0$ años), demostrando una capacidad sólida de generalización a partir de las características faciales extraídas del corpus fotográfico.

### 2. Implicaciones Operativas para el Cliente (Good Seed)
* **Control y Cumplimiento Normativo:** El sistema de visión artificial implementado aporta una solución automatizable para la cadena de supermercados Good Seed, ayudando a verificar de forma preventiva la edad de los clientes en el área de pago durante la adquisición de alcohol.
* **Mitigación de Riesgos Legales:** Aunque el error promedio se mantiene en un margen razonable, la herramienta actúa como un valioso filtro de apoyo operativo para los cajeros, reduciendo significativamente la probabilidad de ventas accidentales a menores de edad y salvaguardando la conformidad legal de la compañía.

### 3. Oportunidades de Mejora y Trabajos Futuros
* **Densidad de Muestras en Edades Críticas:** Se recomienda enriquecer el corpus de datos con una mayor representación de imágenes en los rangos etarios extremos (menores de 10 años y mayores de 60), priorizando la recolección de muestras en la franja crítica cercana a la mayoría de edad (16 a 19 años) para refinar la precisión del estimador en el umbral legal.
* **Robustez ante Factores Ambientales:** Incorporar técnicas avanzadas de aumentación de datos orientadas a mitigar variaciones por condiciones de iluminación irregular, oclusiones parciales del rostro (como accesorios o mascarillas) y ángulos de inclinación de las cámaras instaladas en las cajas de cobro.

---

## Herramientas y Tecnologías
- Python  
- TensorFlow / Keras  
- Pandas  
- NumPy  
- Scikit-Learn  
- PIL / Matplotlib / Seaborn  

---

## Archivos Finales
La carpeta con los archivos finales (`final files`) se encuentra disponible en el siguiente enlace: [Carpeta de Archivos Finales](https://drive.google.com/uc?export=download&id=1qLEsMg4llT5Tz2CyrMH3xAudJPUKiypb)

---
---

<img width="921" height="269" alt="image" src="https://github.com/user-attachments/assets/38e789a9-e7b1-43f6-89c5-bf452d374b52" />

# Facial Age Estimation for Compliance in Alcohol Sales: Predictive Modeling and Computer Vision

## Problem
In the Good Seed supermarket chain, ensuring strict compliance with alcohol sales regulations by preventing sales to minors is a critical operational challenge. Stores are equipped with cameras in the checkout area that automatically activate when an alcohol purchase is registered.  
The goal of this project is to build and evaluate a computer vision model capable of accurately predicting a person's chronological age from a facial photograph, serving as a preventive support tool for checkout staff.

---

## Data
The analysis used a dataset composed of metadata and photographic records processed through the following stages:
- **Corpus volume:** 7,591 facial images paired with their respective real age labels (`real_age`) (5,693 for training and 1,898 for validation/testing).
- **Data flow:** Implementation of dynamic generators (`ImageDataGenerator`) with stochastic augmentation (horizontal flip, rotations, and shifts) for training and standardized preprocessing using ResNet50's function.

---

## Approach
The project followed a structured Deep Learning and computer vision methodology:
- Exploratory Data Analysis (EDA) to examine corpus integrity, demographic distribution, and operational risks at the 18-year legal threshold.
- Implementation of Transfer Learning using the **ResNet50** network pre-trained on ImageNet as a backbone, applying selective fine-tuning on the last layers.
- Construction of a custom regression head with Global Average Pooling, a 128-neuron dense layer (ReLU activation), Dropout regularization (0.3), and a linear output layer.
- Optimization via the Adam algorithm, optimizing the Mean Absolute Error (MAE) loss function and using callbacks (`EarlyStopping` and `ModelCheckpoint`) to save the best artifact (`best_model.h5`).

---

## Key Performance Results
The model completed the training cycle showing solid convergence until reaching its optimal point at **Epoch 20**:
- **Validation MAE (Val MAE):** **7.54** (exactly 7.5385 years)
- **Project Success Threshold:** $\le 8.0$ years (Successfully achieved).
- **Completion Status:** The *Early Stopping* callback optimally restored the weights corresponding to the best performance at epoch 20.

### Training Evolution (Progress by Epochs):
| Epoch | Training Loss | Training MAE | Validation Loss (Val Loss) | Val MAE (Primary Metric) |
| :---: | :---: | :---: | :---: | :---: |
| **01 / 20** | 22.51 | 22.51 | 22.80 | 22.80 |
| **05 / 20** | 7.69 | 7.69 | 8.05 | 8.05 |
| **10 / 20** | 6.56 | 6.56 | 7.68 | 7.68 |
| **15 / 20** | 6.06 | 6.06 | 7.65 | 7.65 |
| **20 / 20 (Optimal)** | **5.54** | **5.54** | **7.54** | **7.54** |

---

## Performance Evaluation and Inference Analysis
The evaluation executed on the validation set using the persisted artifact (`best_model.h5`) confirms the stability and generalization of the trained model in an independent inference environment.

* **Final Metric Obtained:** A Mean Absolute Error (MAE) of **7.5385 years** was recorded, rigorously meeting the established success threshold ($\le 8.0$ years).
* **Empirical Contrast:** Predictions generated on specific validation samples display the estimator's behavior across different profiles:
  * Instance 1 -> Real Age: 50 | Estimated Age: 40.2
  * Instance 2 -> Real Age: 41 | Estimated Age: 22.7
  * Instance 3 -> Real Age: 46 | Estimated Age: 34.1
  * Instance 4 -> Real Age: 85 | Estimated Age: 90.6
  * Instance 5 -> Real Age: 14 | Estimated Age: 21.0

---

## Conclusions and Business Impact Evaluation

### 1. Model Performance and Results
Following validation using the optimized artifact (`best_model.h5`), the ResNet50 regression model achieved a **Mean Absolute Error (MAE) of 7.54 years**. This result successfully satisfies the established success threshold ($\le 8.0$ years), proving robust generalization from the facial features extracted from the corpus.

### 2. Operational Implications for the Client (Good Seed)
* **Control and Regulatory Compliance:** The computer vision system provides an automated solution for Good Seed supermarkets, helping preventatively verify customer age at checkout when purchasing alcohol.
* **Legal Risk Mitigation:** Although the average error remains within reasonable bounds, the tool acts as a valuable operational support filter for cashiers, significantly reducing accidental sales to minors and safeguarding compliance.

### 3. Improvement Opportunities and Future Work
* **Sample Density in Critical Ages:** Enriching the dataset with higher image representation in extreme age ranges (under 10 and over 60) is recommended, prioritizing samples near the legal majority threshold (16 to 19 years) to refine precision.
* **Environmental Robustness:** Incorporating advanced data augmentation techniques to mitigate variations due to uneven lighting, partial facial occlusions (accessories or masks), and checkout camera angles.

---

## Tools and Technologies
- Python  
- TensorFlow / Keras  
- Pandas  
- NumPy  
- Scikit-Learn  
- PIL / Matplotlib / Seaborn  

---

## Final Files
The folder containing the final files (`final files`) is available at the following link: [Final Files Folder](https://drive.google.com/uc?export=download&id=1qLEsMg4llT5Tz2CyrMH3xAudJPUKiypb)

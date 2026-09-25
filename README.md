<img width="921" height="269" alt="image" src="https://github.com/user-attachments/assets/38e789a9-e7b1-43f6-89c5-bf452d374b52" />

# Estimación de Edad Facial para Cumplimiento Normativo en la Venta de Alcohol: Modelado Predictivo y Visión Artificial

## Problema
En la cadena de supermercados Good Seed, garantizar el cumplimiento estricto de las normativas de venta de alcohol mediante la prohibición a menores de edad es un desafío operativo crítico[cite: 1]. Las tiendas están equipadas con cámaras en el área de pago que se activan automáticamente al registrar la compra de este producto[cite: 1].  
El objetivo de este proyecto es construir y evaluar un modelo de visión artificial capaz de predecir con precisión la edad cronológica de una persona a partir de su fotografía facial, sirviendo como una herramienta preventiva de apoyo para el personal de cajas[cite: 1].

---

## Datos
El análisis utilizó un conjunto de datos compuesto por metadatos y registros fotográficos procesados mediante las siguientes etapas[cite: 1]:
- **Volumen del corpus:** 7,591 imágenes de rostros emparejadas con sus respectivas etiquetas de edad real (`real_age`)[cite: 1].
- **Flujo de datos:** Implementación de generadores dinámicos (`ImageDataGenerator`) con aumentación estocástica (volteo horizontal, rotaciones y desplazamientos) para el entrenamiento y preprocesamiento estandarizado con la función de ResNet50[cite: 1].

---

## Enfoque
El proyecto siguió una metodología estructurada de Deep Learning y visión artificial[cite: 1]:
- Análisis exploratorio de datos (EDA) para examinar la integridad del corpus, la distribución demográfica (con sesgo hacia adultos jóvenes) y los riesgos operativos en el umbral legal de los 18 años[cite: 1].
- Implementación de *Transfer Learning* utilizando la red **ResNet50** pre-entrenada en ImageNet como modelo base (*backbone*), aplicando *fine-tuning* selectivo en las últimas 30 capas[cite: 1].
- Construcción de un cabezal de regresión personalizado con *Global Average Pooling*, una capa densa de 128 neuronas (activación ReLU), regularización *Dropout* (0.3) y una capa de salida lineal[cite: 1].
- Optimización mediante el algoritmo Adam con una tasa de aprendizaje de $1e-5$, optimizando la función de pérdida de Error Absoluto Medio (MAE) y utilizando *callbacks* (`EarlyStopping` y `ModelCheckpoint`) para guardar el mejor artefacto (`best_model.h5`)[cite: 1].

---

## Resultados
El modelo cumplió y superó satisfactoriamente los criterios de éxito establecidos[cite: 1]:
- **MAE (Validación):** 7.5534 años (superando el umbral requerido de $\le 8.0$ años)[cite: 1].

### Otros resultados clave:
- **Generalización:** La validación sobre el conjunto de prueba independiente (1,898 imágenes) confirmó la estabilidad del artefacto optimizado en datos no observados[cite: 1].
- **Contraste empírico:** El modelo demostró estimaciones competitivas y una alta precisión en diferentes perfiles demográficos, validando su viabilidad práctica[cite: 1].

---

## Conclusión
El modelado predictivo basado en redes neuronales profundas demostró ser una solución técnica viable para automatizar la estimación de edad en entornos comerciales de gran escala. Implementar este flujo otorga a Good Seed una sólida base tecnológica para mitigar riesgos legales y asegurar el cumplimiento normativo en la venta de alcohol[cite: 1].

---

## Herramientas y Tecnologías
- Python[cite: 1]
- TensorFlow / Keras[cite: 1]
- Pandas[cite: 1]
- NumPy[cite: 1]
- Scikit-Learn[cite: 1]
- PIL / Matplotlib / Seaborn[cite: 1]

---

## Conclusión Clave
Este proyecto demuestra la aplicación práctica de técnicas de transferencia de aprendizaje (*Transfer Learning*) y redes convolucionales orientadas a resolver un desafío crítico de cumplimiento legal y seguridad en el sector de retail[cite: 1].

---
---


# Facial Age Estimation for Compliance in Alcohol Sales: Predictive Modeling and Computer Vision

## Problem
In the Good Seed supermarket chain, ensuring strict compliance with alcohol sales regulations by preventing sales to minors is a critical operational challenge[cite: 1]. Stores are equipped with cameras in the checkout area that automatically activate when an alcohol purchase is registered[cite: 1].
The goal of this project is to build and evaluate a computer vision model capable of accurately predicting a person's chronological age from a facial photograph, serving as a preventive support tool for checkout staff[cite: 1].

---

## Data
The analysis used a dataset composed of metadata and photographic records processed through the following stages[cite: 1]:
- **Corpus volume:** 7,591 facial images paired with their respective real age labels (`real_age`)[cite: 1].
- **Data flow:** Implementation of dynamic generators (`ImageDataGenerator`) with stochastic augmentation (horizontal flip, rotations, and shifts) for training and standardized preprocessing using ResNet50's function[cite: 1].

---

## Approach
The project followed a structured Deep Learning and computer vision methodology[cite: 1]:
- Exploratory Data Analysis (EDA) to examine corpus integrity, demographic distribution (skewed toward young adults), and operational risks at the 18-year legal threshold[cite: 1].
- Implementation of Transfer Learning using the **ResNet50** network pre-trained on ImageNet as a backbone, applying selective fine-tuning on the last 30 layers[cite: 1].
- Construction of a custom regression head with Global Average Pooling, a 128-neuron dense layer (ReLU activation), Dropout regularization (0.3), and a linear output layer[cite: 1].
- Optimization via the Adam algorithm with a learning rate of $1e-5$, optimizing the Mean Absolute Error (MAE) loss function and using callbacks (`EarlyStopping` and `ModelCheckpoint`) to save the best artifact (`best_model.h5`)[cite: 1].

---

## Results
The model successfully met and exceeded the established success criteria[cite: 1]:
- **MAE (Validation):** 7.5534 years (surpassing the required threshold of $\le 8.0$ years)[cite: 1].

### Other Key Results:
- **Generalization:** Validation on the independent test sample (1,898 images) confirmed the stability of the optimized artifact on unseen data[cite: 1].
- **Empirical Contrast:** The model demonstrated competitive estimations and high accuracy across different demographic profiles, validating its practical viability[cite: 1].

---

## Conclusion
Predictive modeling based on deep neural networks proved to be a technically viable solution to automate age estimation in large-scale retail environments. Implementing this workflow provides Good Seed with a solid technological foundation to mitigate legal risks and ensure regulatory compliance in alcohol sales[cite: 1].

---

## Tools and Technologies
- Python[cite: 1]
- TensorFlow / Keras[cite: 1]
- Pandas[cite: 1]
- NumPy[cite: 1]
- Scikit-Learn[cite: 1]
- PIL / Matplotlib / Seaborn[cite: 1]

---

## Key Takeaway
This project demonstrates the practical application of transfer learning techniques and convolutional networks aimed at solving a critical challenge of legal compliance and security in the retail sector[cite: 1].

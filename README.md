# Diagnóstico Automático de Neumonía mediante Deep Learning

El proyecto se centra en el desarrollo de redes neuronales convolucionales (CNN) para clasificar radiografías de tórax en dos categorías clínicas: **Normal** y **Neumonía**.

## Conjunto de Datos (Dataset)

Para este proyecto se ha utilizado el popular conjunto de datos **"Chest X-Ray Images (Pneumonia)"** de Kaggle. 

*   **Volumen total:** 5.856 radiografías de tórax en formato JPEG.
*   **Estructura:** Partición rigurosa en conjuntos de Entrenamiento, Validación y Test Ciego (624 imágenes reservadas para la evaluación final).

*(Nota: Por restricciones de peso, las imágenes originales no están subidas a este repositorio).*


## Estado Actual: Modelo Base (Baseline VGG16)

El cuaderno principal (`modelo_base_vgg16.ipynb`) implementa un *pipeline* médico robusto que incluye las siguientes técnicas:

*   **Ingeniería de Datos:** Preprocesamiento y *Data Augmentation* dinámico (rotación, zoom, desplazamientos) para evitar el sobreajuste.
*   **Mitigación de Sesgo de Clases:** Aplicación de pesos matemáticos (`class_weight`) durante el entrenamiento para contrarrestar el desequilibrio natural del dataset clínico.
*   **Estrategia de Entrenamiento en 2 Fases:** 
    1.  *Transfer Learning* utilizando la arquitectura **VGG16** (pesos de ImageNet) con las capas base congeladas.
    2.  *Fine-Tuning* progresivo descongelando el último bloque convolucional para adaptar los pesos al dominio médico.
*   **Monitorización:** Uso de *Early Stopping* y *Model Checkpoint* para preservar los mejores pesos en base al error de validación.

## Resultados Clínicos Obtenidos

Tras evaluar el modelo con un conjunto de prueba ciego compuesto por 624 radiografías[cite: 1], el modelo ha logrado un rendimiento equiparable al estándar de la industria:

*   **Precisión Global (Accuracy):** 90.87%
*   **Sensibilidad Neumonía (Recall):** 98.46% (Maximizando la reducción de falsos negativos)
*   **Área bajo la curva (ROC AUC):** 0.9686

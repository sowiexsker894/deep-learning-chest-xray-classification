# Procesamiento de Imágenes - Detección de Neumonía en Radiografías de Tórax

## 📋 Información del Curso y Equipo
- **Curso:** CC235 - Procesamiento de Imágenes
- **Carrera:** Ciencias de la Computación
- **Profesor:** Luis Canaval Sánchez
- **Integrantes:**
  - Mireya Nicole Sihuincha Schermuly
  - Carlos Alejandro Molina Huatuco
  - Joaquin Fernando Arèvalo Alcàntara
- **Fecha:** Mayo 2025

---

![Radiografía de Tórax](imagen_2025-05-07_161158968.png)  
*Ejemplo de radiografía de tórax procesada*

## 📌 Resumen

Este informe desarrolla un pipeline open-source de preprocesamiento de radiografías de tórax para mejorar la calidad visual y facilitar la detección de neumonía. Emplea el dataset Chest X-Ray Images (Pneumonia) de Kaggle, compuesto por aproximadamente 5,856 imágenes en escala de grises. Se plantean dos enfoques complementarios:

### 🔬 Enfoque Clásico
Aplica filtro Gaussiano (σ optimizado), filtro Mediano 3×3, ecualización de histograma, segmentación por umbral global y operaciones morfológicas para definir la región pulmonar. Sobre esta ROI se extraen histogramas de intensidad, descriptores LBP y estadísticas que alimentan un clasificador SVM lineal o regresión logística.

### 🧠 Enfoque de Deep Learning
Utiliza DenseNet-121 preentrenada en ImageNet, adaptada con redimensionado a 224×224 px, data augmentation (rotaciones, flips y ajustes de brillo) y fine-tuning con Adam para generar una probabilidad continua de neumonía.

**Palabras clave:** procesamiento de imágenes, radiografías de tórax, neumonía, filtro Gaussiano, DenseNet-121.

---

## 📚 Contenido

### 1. 📖 Introducción

El diagnóstico médico a través de imágenes radiográficas constituye un pilar fundamental en la detección temprana de diversas patologías. Entre estas, la neumonía destaca como una de las principales causas de mortalidad, especialmente en países en vías de desarrollo (Organización Mundial de la Salud [OMS], 2023). 

Las radiografías de tórax presentan limitaciones técnicas como ruido gaussiano, bajo contraste y artefactos que dificultan la visualización de tejidos pulmonares (Litjens et al., 2017). Estas fallas pueden eliminarse con un correcto tratamiento y procesado de cada imagen.

### 2. 🎯 Objetivos

- Desarrollar un pipeline de preprocesamiento de imágenes para mejorar la calidad visual de radiografías de tórax
- Combinar técnicas clásicas de procesamiento con redes neuronales profundas
- Optimizar la reducción de ruido, realce de bordes y contraste en las imágenes

### 3. ✳️ Logro del Curso

**Competencia General:** Manejo de la Información y Pensamiento Crítico (Nivel 2)  
Analizar un problema de computación complejo y aplicar principios de computación para identificar soluciones.

**Competencia Específica:** ABET 5 - Trabajo Multidisciplinario (Nivel 1)  
Capacidad de trabajar en proyectos de equipo multidisciplinares, aplicando principios científicos a soluciones prácticas e innovadoras.

### 4. 🗺️ Descripción del Caso de Uso

El diagnóstico de neumonía mediante radiografías se ve afectado por limitaciones técnicas. Este proyecto desarrolla una herramienta open-source de preprocesamiento que podría integrarse en plataformas de telemedicina, democratizando el acceso a diagnósticos precisos en contextos con recursos limitados.

**Preguntas clave:**
1. ¿Puede nuestro pipeline clasificar radiografías como normal/neumonía con precisión efectiva?
2. ¿Cuál es la probabilidad de neumonía dada una radiografía filtrada?
3. ¿Cuál es la sensibilidad de nuestro clasificador tras el preprocesamiento?

### 5. 🌐 Descripción del Conjunto de Datos

**Nombre:** Chest X-Ray Images (Pneumonia)  
**Fuente:** [Kaggle](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia)  
**Tamaño:** 5,856 imágenes (1.24GB)  
**Formato:** PNG  
**Estructura:**
- **Normal:** Imágenes de pulmones sanos
- **Pneumonia:** Imágenes con neumonía

### 6. ▶️ Modelización

#### 6.1 Modelo Clásico

**Preprocesamiento:**
1. Filtro Gaussiano para reducción de ruido
2. Filtro Mediano 3×3 para eliminar "ruido sal y pimienta"
3. Umbralización global para segmentación
4. Operaciones morfológicas para refinamiento

**Clasificación:** SVM lineal o Regresión Logística

#### 6.2 Modelo de Aprendizaje Profundo

**Arquitectura:** DenseNet-121 preentrenada  
**Preprocesamiento:**
- Redimensionado a 224×224 px
- Data augmentation (rotaciones, flips, ajustes de brillo)
- Normalización según ImageNet

**Entrenamiento:**
- Fine-tuning con Adam (lr=1×10⁻⁴)
- Binary cross-entropy como función de pérdida
- 20 epochs con batch size 16

#### 6.3 Respuesta a las Preguntas

1. **Precisión:** Calculada mediante matriz de confusión (TP+TN)/Total
2. **Probabilidad:** predict_proba() para modelo clásico, salida sigmoide para DenseNet
3. **Sensibilidad:** TP/(TP+FN) a partir de matriz de confusión

### 7. 📊 Publicación de Resultados

#### 7.1 Modelo Clásico

Esta sección detalla los resultados obtenidos de la implementación del primer enfoque para la clasificación de radiografías de tórax en "NORMAL" o "NEUMONÍA". Se evaluaron dos modelos de clasificación tradicionales, Support Vector Machine (SVM) lineal y Regresión Logística, después de un riguroso proceso de preprocesamiento y extracción de características de las imágenes.

**Métricas de Evaluación:**
- **Exactitud (Accuracy):** Proporción de predicciones correctas sobre el total
- **Precisión (Precision):** De todas las instancias predichas como positivas, cuántas fueron realmente positivas
- **Sensibilidad (Recall):** De todas las instancias realmente positivas, cuántas fueron correctamente identificadas
- **Puntuación F1 (F1-Score):** Media armónica de la precisión y la sensibilidad
- **Área bajo la curva ROC (AUC-ROC):** Capacidad del modelo para distinguir entre clases
- **Matriz de Confusión:** Tabla detallada de verdaderos positivos, negativos, falsos positivos y negativos

**Resultados:**
El modelo SVM obtuvo un rendimiento marginalmente superior en la mayoría de las métricas clave para la detección de neumonía, alcanzando una precisión del 69% comparado con el 68% de la regresión logística.

#### 7.2 Modelo de Aprendizaje Profundo

En este segundo enfoque, se implementó un modelo de aprendizaje profundo basado en la arquitectura DenseNet-121, utilizando la técnica de aprendizaje por transferencia. Para combatir el sesgo observado en los modelos clásicos, se aplicó una estrategia de pesos de clase en la función de pérdida, penalizando más duramente los errores en la clasificación de PNEUMONIA.

El modelo fue entrenado durante 30 épocas, demostrando un aprendizaje estable y una mejora significativa en el rendimiento. La evaluación final se realizó sobre el mismo conjunto de prueba de 624 imágenes para una comparación directa y justa.

**Resultados Destacados:**
- **Rendimiento General:** Exactitud del 86.5% y AUC-ROC de 0.9377
- **Detección de Neumonía:** Sensibilidad del 87.2% para la clase PNEUMONIA
- **Fiabilidad:** Precisión del 90.9% para PNEUMONIA con F1-Score de 0.89

#### 7.3 Respuesta de Nuestros Modelos a las Preguntas

**¿Puede nuestro pipeline clasificar una radiografía de tórax como normal o neumonía con una precisión efectiva?**

- **Modelo Clásico:** El modelo SVM alcanzó una precisión general del 69%
- **Modelo de Aprendizaje Profundo:** El modelo DenseNet-121 logró una precisión general del 86.5%

**¿Cuál es la probabilidad de que un paciente tenga neumonía dada su radiografía filtrada?**

- **Modelo Clásico:** AUC-ROC de 0.55, indicando capacidad de discriminación limitada
- **Modelo de Aprendizaje Profundo:** AUC-ROC de 0.9377, demostrando capacidad sobresaliente

**¿Cuál es la sensibilidad de nuestro clasificador normal o neumonía tras aplicar el preprocesamiento?**

- **Modelo Clásico:** Sensibilidad del 100% pero con alta tasa de falsos positivos
- **Modelo de Aprendizaje Profundo:** Sensibilidad del 87.2% con excelente balance

### 8. ⚜️ Conclusiones

El estudio demostró que, si bien las técnicas tradicionales ofrecen una base de clasificación, los modelos de aprendizaje profundo proporcionan una solución significativamente más robusta y precisa para la detección de neumonía. El modelo DenseNet-121 superó de manera concluyente al modelo clásico (SVM), aumentando la exactitud general del 69% al 86.5%.

Más importante aún, la sensibilidad para detectar casos de neumonía —la métrica más crítica en un contexto clínico— saltó de un nivel modesto a un excelente 87.2%, demostrando la clara superioridad del enfoque de deep learning para esta tarea.

La implementación de esta solución se realizó utilizando herramientas de código abierto y en un entorno Google Colab que simula condiciones de recursos accesibles. El alto rendimiento y la fiabilidad del modelo DenseNet-121 final, con un AUC-ROC de 0.9377, validan su gran potencial para ser integrado en plataformas de telemedicina reales.

El análisis comparativo de los modelos no mostró un rendimiento complementario, sino que reveló una mejor propuesta. El modelo DenseNet-121, tras ser optimizado con pesos de clase para corregir el sesgo de los datos, se consolidó como la herramienta definitiva. Su capacidad para identificar correctamente al 87.2% de los pacientes con neumonía, manteniendo al mismo tiempo una alta precisión del 90.9%, lo posiciona como un poderoso sistema de apoyo para el personal médico, capaz de agilizar el pre-diagnóstico y mejorar la atención en entornos clínicos.

### 9. 🔆 Referencias Bibliográficas

1. Mooney, P. (2018). Chest X-Ray Images (Pneumonia). Kaggle. https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia
2. Litjens, G., et al. (2017). A survey on deep learning in medical image analysis. Medical Image Analysis, 42, 60–88. https://doi.org/10.1016/j.media.2017.07.005
3. Organización Mundial de la Salud. (2023). Neumonía. https://www.who.int/es/news-room/fact-sheets/detail/pneumonia

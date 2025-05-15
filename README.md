# Procesamiento de Imágenes - Detección de Neumonía en Radiografías de Tórax

## Información del Curso y Equipo
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
*Ejemplo de radiografía de tórax procesada ()*

## 📌Resumen
Este informe desarrolla un pipeline open-source de preprocesamiento de radiografías de tórax para mejorar la calidad visual y facilitar la detección de neumonía. Emplea el dataset Chest X-Ray Images (Pneumonia) de Kaggle, compuesto por aproximadamente 5,856 imágenes en escala de grises. Se plantean dos enfoques complementarios:

1. **Enfoque clásico:** Aplica filtro Gaussiano (σ optimizado), filtro Mediano 3×3, ecualización de histograma, segmentación por umbral global y operaciones morfológicas para definir la región pulmonar. Sobre esta ROI se extraen histogramas de intensidad, descriptores LBP y estadísticas que alimentan un clasificador SVM lineal o regresión logística.

2. **Enfoque de deep learning:** Utiliza DenseNet-121 preentrenada en ImageNet, adaptada con redimensionado a 224×224 px, data augmentation (rotaciones, flips y ajustes de brillo) y fine-tuning con Adam para generar una probabilidad continua de neumonía.

**Palabras clave:** procesamiento de imágenes, radiografías de tórax, neumonía, filtro Gaussiano, DenseNet-121.
--- 

## Contenido

### 1. 📖 Introducción
El diagnóstico médico a través de imágenes radiográficas constituye un pilar fundamental en la detección temprana de diversas patologías. Entre estas, la neumonía destaca como una de las principales causas de mortalidad, especialmente en países en vías de desarrollo (Organización Mundial de la Salud [OMS], 2023). 

Las radiografías de tórax presentan limitaciones técnicas como ruido gaussiano, bajo contraste y artefactos que dificultan la visualización de tejidos pulmonares (Litjens et al., 2017). Estas fallas pueden eliminarse con un correcto tratamiento y procesado de cada imagen.

---
### 2. 🎯 Objetivos
- Desarrollar un pipeline de preprocesamiento de imágenes para mejorar la calidad visual de radiografías de tórax.
- Combinar técnicas clásicas de procesamiento con redes neuronales profundas.
- Optimizar la reducción de ruido, realce de bordes y contraste en las imágenes.
---

### 3. ✳️ Logro del Curso
**Competencia General:** Manejo de la Información y Pensamiento Crítico (Nivel 2)  
Analizar un problema de computación complejo y aplicar principios de computación para identificar soluciones.

**Competencia Específica:** ABET 5 - Trabajo Multidisciplinario (Nivel 1)  
Capacidad de trabajar en proyectos de equipo multidisciplinares, aplicando principios científicos a soluciones prácticas e innovadoras.

---

### 4. 🗺️  Descripción del Caso de Uso
El diagnóstico de neumonía mediante radiografías se ve afectado por limitaciones técnicas. Este proyecto desarrolla una herramienta open-source de preprocesamiento que podría integrarse en plataformas de telemedicina, democratizando el acceso a diagnósticos precisos en contextos con recursos limitados.

**Preguntas clave:**
1. ¿Puede nuestro pipeline clasificar radiografías como normal/neumonía con precisión efectiva?
2. ¿Cuál es la probabilidad de neumonía dada una radiografía filtrada?
3. ¿Cuál es la sensibilidad de nuestro clasificador tras el preprocesamiento?

---
### 5.🌐 Descripción del Conjunto de Datos
**Nombre:** Chest X-Ray Images (Pneumonia)  
**Fuente:** [Kaggle](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia)  
**Tamaño:** 5,856 imágenes (1.24GB)  
**Formato:** PNG  
**Estructura:**
- Normal: Imágenes de pulmones sanos
- Pneumonia: Imágenes con neumonía

---
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
---
### 7. ⚜️ Conclusiones
Este trabajo implementó dos enfoques complementarios para la detección de neumonía en radiografías: un pipeline clásico con filtrado y clasificación tradicional, y un modelo de deep learning basado en DenseNet-121. Los resultados demuestran que la combinación de estas técnicas puede mejorar significativamente la precisión diagnóstica, especialmente en entornos con recursos limitados. Como trabajo futuro, se propone integrar estos modelos en una plataforma open-source para telemedicina y explorar técnicas de explicabilidad para aumentar la confianza clínica en las predicciones del modelo.

---
### 8. 🔆 Referencias Bibliográficas
1. Mooney, P. (2018). Chest X-Ray Images (Pneumonia). Kaggle. https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia
2. Litjens, G., et al. (2017). A survey on deep learning in medical image analysis. Medical Image Analysis, 42, 60–88. https://doi.org/10.1016/j.media.2017.07.005
3. Organización Mundial de la Salud. (2023). Neumonía. https://www.who.int/es/news-room/fact-sheets/detail/pneumonia

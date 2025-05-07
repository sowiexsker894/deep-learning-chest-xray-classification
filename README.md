# CC235-TP-TF-2025-1
ANÁLISIS: MEJORA DE RADIOGRAFÍAS MÉDICAS 

Para realizar esta tarea hemos empleado el conjunto de datos desde kaggle "Chest X-Ray Images (Pneumonia)" https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia  Este dataset contiene imágenes de tórax que serán utilizadas para entrenar modelos de procesamiento de imágenes para la detección de neumonía

## Contenidos

1. [INTRODUCCIÓN](#data1)

2. [OBJETIVOS](#data2)

3. [lOGRO DEL CURSO](#data3)
        
4. [DESCRIPCIÓN DEL CASO DE USO](#data4)
    
5. [DESCRIPCIÓN DEL CONJUNTO DE DATOS](#data5)

6. [MODELIZACIÓN](#data6)

7. [PUBLICACIÓN DE LOS RESULTADOS](#data7)
   
8. [INTERFAZ GRÁFICA](#data8)
    
9. [CONCLUSIONES](#data9)

10. [REFERENCIAS BIBLIOGRÁFICAS](#data9)


## 1. Introducción <a name="data1"></a>

<center><p style="text-align: justify;">
  
El diagnóstico médico a través de imágenes radiográficas constituye un pilar fundamental en la detección temprana de diversas patologías. Entre estas, la neumonía destaca como una de las principales causas de mortalidad, especialmente en países en vías de desarrollo (Organización Mundial de la Salud [OMS], 2023). Las radiografías de tórax se consideran una de las herramientas más efectivas para identificar esta enfermedad; sin embargo, su interpretación suele verse afectada por limitaciones técnicas como el ruido gaussiano, el bajo contraste y la presencia de artefactos que dificultan la correcta visualización de los tejidos pulmonares (Litjens et al., 2017).

<img src="NEUMONIA .png" alt="NEUMONÍA" style="width: 700px;"/>
<center>Figura 1: NEUMONÍA</center>

<p></p>

## 2. Objetivos <a name="data2"></a>

Desarrollar un pipeline de preprocesamiento de imágenes orientado a la mejora de la calidad visual de las radiografías de tórax, facilitando así un diagnóstico más preciso y efectivo tanto para especialistas médicos como para sistemas de diagnóstico asistido por computadora (CAD).

Combina técnicas clásicas de procesamiento de imágenes junto con redes neuronales profundas, optimizando la reducción de ruido, el realce de bordes y el contraste en las imágenes.

## 3. Logro del curso <a name="data2"></a>

Competencia General: Manejo de la Información y Pensamiento Crítico
Nivel de logro: 2

Analizar un problema de computación complejo y aplicar principios de computación y otras disciplinas relevantes para identificar soluciones.

Competencia Específica: ABET 5 – Trabajo Multidisciplinario Nivel de logro: 1

Capacidad de trabajar en proyectos de equipo, que suelen ser multidisciplinares. Esta base brinda a los estudiantes una amplia base de comprensión que les permite aplicar su conocimiento de los principios científicos a las soluciones prácticas e innovadoras de problemas existentes y futuros.

## 4. Descripción del caso de uso <a name="data4"></a>

El diagnóstico médico basado en imágenes, como las radiografías de tórax, es esencial para la detección temprana de enfermedades respiratorias como la neumonía, una de las principales causas de mortalidad en países en desarrollo (Organización Mundial de la Salud [OMS], 2023). No obstante, dichas imágenes suelen representar limitaciones técnicas como ruido gaussiano y bajo contraste, lo cual complica su interpretación tanto para especialistas como para sistemas de diagnóstico asistido por computadora(CAD), disminuyendo así su eficacia (Litjens et al., 2017) . Frente a esta problemática, el desarrollo de una herramienta open-source de preprocesamiento de imágenes podría integrarse en plataformas de telemedicina, contribuyendo a democratizar el acceso a diagnósticos médicos precisos y oportunos, especialmente en contextos con recursos limitados.

A continuación, se formulan las preguntas que este proyecto atenderá mediante clasificación y/o predicción:

¿Puede nuestro pipeline preprocesado clasificar una radiografía de tórax como normal o neumonía con una precisión efectiva? (TP + TN) / Total
¿Cuál es la probabilidad de que un paciente tenga neumonía dada su radiografía filtrada?
¿Cuál es la sensibilidad de nuestro clasificador normal o neumonía tras aplicar el preprocesamiento? TP / (TP+FN)

Tenemos como objetivo general desarrollar un pipeline open-source de preprocesamiento que elimine el ruido y mejore el contraste en radiografías de tórax, con el fin de facilitar la lectura diagnóstica por radiólogos y la detección automática de neumonía mediante la integración de algoritmos de inteligencia artificial. 


## 4. Descripción del caso de uso <a name="data4"></a>

### Origen de los datos: 
- **Autores**: Paul Mooney
- **Fuente**: Kaggel
- **Nombre del Conjunto de Datos**: Chest X-Ray Images (Pneumonia)

-Tamaño del Conjunto de Datos: El dataset consta de aproximadamente 5,856 imágenes de radiografías de tórax.(1.24GB)

-Tipo de Datos: Las imágenes están en formato PNG y están divididas en dos carpetas: 
Normal: Presenta una serie de imágenes con pulmones sanos de pacientes atendidos.
Pneumonia: Presenta imágenes de pulmones que presentan cuadros de Neumonía.

-Detalles de las Columnas o Características

 Tipo de Imagen: Todas las imágenes son radiografías de tórax en formato PNG.
 Etiquetado: Cada imagen está etiquetada con una clase que indica si el paciente tiene neumonía (1) o no (0).

 






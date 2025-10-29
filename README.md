# Análisis de Sesgos en Noticias con Modelos de Embedding
## Modelo de IA simple en Python para el análisis de los sesgos en embeddings de palabras (Word Embeddings)

Este proyecto utiliza un modelo de *Word Embedding* simple implementado en **Python** para analizar y detectar posibles sesgos en un corpus de noticias en español. El objetivo es identificar asociaciones no deseadas o sesgadas en el tratamiento y la elección de palabras dentro de los textos periodísticos y reflexionar sobre su impacto ético.
---

<p align="center">
  ![Artificial Intelligence Dancing GIF](https://github.com/user-attachments/assets/46e2def6-6494-4007-a96b-16ce80e9a328)

---

## Descripción del Corpus Utilizado

El corpus utilizado es un subconjunto de datos del *dataset* **"Spanish News Classification"** de Kaggle (o similar corpus de noticias en español).

* **Contenido:** Noticias reales extraídas de periódicos.
* **Columna clave:** Se utilizó la columna que contiene los **títulos o el cuerpo de las noticias** (la columna **'news'** o equivalente) para construir el corpus de entrenamiento del modelo de *embedding*.
* **Procesamiento:** El texto fue preprocesado (conversión a minúsculas, eliminación de puntuación/símbolos y tokenización) antes de entrenar el modelo.

---

##  Lista de Palabras Seleccionadas y Justificación

Se seleccionó un conjunto de **10 palabras** con potencial de ser asociadas de manera sesgada, basándose en la consigna y la relevancia social en el contexto de noticias.

| Palabra | Categoría de Sesgo Potencial | Razón para la Selección |
| :--- | :--- | :--- |
| **mujer** | Género y Edad | Identificar posibles asociaciones con roles o características sesgadas (e.g., joven). |
| **hombre** | Género y Edad | Identificar posibles asociaciones con roles o características sesgadas (e.g., viejo). |
| **joven** | Edad | Analizar la asociación con género u otros grupos demográficos. |
| **viejo** | Edad | Analizar la asociación con género u otros grupos demográficos. |
| **trabajador** | Estereotipo de Rol | Rol profesional para ver su cercanía con género o estatus (e.g., inmigrante). |
| **nativo** | Origen/Estatus | Analizar el contraste y la asociación con "inmigrante" y "refugiado". |
| **inmigrante** | Origen/Estatus | Palabras sensibles en noticias; buscar asociaciones negativas o de conflicto. |
| **refugiado** | Origen/Estatus | Palabras sensibles en noticias; buscar asociaciones negativas o de conflicto. |
| **ángel** | Connotación Positiva | Término positivo para contrastar y medir la distancia semántica. |
| **malo** | Connotación Negativa | Término negativo para identificar qué palabras o grupos se asocian a esta connotación. |

---

## Visualización del Mapa 2D y Breve Interpretación

El gráfico muestra la representación de las palabras seleccionadas en un espacio **2D reducido** (utilizando técnica de PCA sobre el espacio de embedding). La cercanía entre los puntos indica **similitud semántica** en el contexto de las noticias del corpus.

<p align="center">

<img width="534" height="411" alt="Captura de pantalla 2025-10-28 225550" src="https://github.com/user-attachments/assets/34a7b48f-63f0-4357-9913-bcc75ccdedb0" />

</p>


**Interpretación del Gráfico:**

El mapa visualiza las relaciones que el modelo de *embedding* ha aprendido del corpus. Las palabras que aparecen **cercanas** entre sí son aquellas que tienden a aparecer en contextos similares dentro de las noticias, lo que sugiere una **asociación semántica** fuerte según el corpus.

---

##  Observaciones de Sesgo Detectadas

El análisis de la cercanía en el espacio de *embedding* revela las siguientes asociaciones que sugieren sesgos presentes en el corpus de noticias:

1.  **Sesgo de Edad y Género:**
    * **"hombre"** se agrupa con **"viejo"**.
    * **"mujer"** se agrupa con **"joven"**.
      
    * **Justificación:**
    
  El modelo asocia al hombre con la vejez y a la mujer con la juventud, lo que indica que, en este conjunto de datos, las noticias que hablan de hombres lo hacen más a menudo en contextos asociados a la edad avanzada, mientras que las noticias sobre mujeres se centran más en contextos de juventud. Este es un **sesgo de estereotipo de edad y género**.

2.  **Sesgo de Estatus y Connotación Negativa:**
    * **"refugiado"** y **"nativo"** se encuentran notablemente **cercanos a "malo"**.
    * **Justificación:**
      
   Esta proximidad sugiere que en el corpus de noticias, tanto la palabra **"refugiado"** como **"nativo"** aparecen con frecuencia en contextos negativos o asociados a problemas (delincuencia, conflictos, crisis, etc.), heredando cercanía semántica con el término **"malo"**. Esto revela un **sesgo de criminalización o negatividad**, afectando particularmente a la población de refugiados, pero también reflejando contextos negativos para los nativos.

3.  **Aislamiento de Roles Positivos/Neutros:**
    * Las palabras **"trabajador"** y **"ángel"** se encuentran **alejadas** de la mayoría de los demás términos.
    * **Justificación:**
    
    Su aislamiento sugiere que estas palabras tienen contextos de aparición muy diferentes en el corpus, sin una asociación semántica fuerte con los grupos demográficos y de estatus analizados.

---

##  Reflexión Ética

### **El Sesgo como Problema en Noticias y el Impacto en la Audiencia**

El sesgo en modelos de Procesamiento de Lenguaje Natural (PLN), especialmente cuando se entrena con un corpus de noticias, no es solo un problema técnico, sino **primordialmente ético**.

* **Amplificación de Estereotipos:** Un modelo de *embedding* simplemente refleja la realidad del texto con el que fue entrenado. Si las noticias sesgan la representación (ej. solo cubren a mujeres jóvenes o asocian a refugiados con problemas), el modelo **aprende y perpetúa** estos estereotipos.
  
* **Impacto en la Audiencia y la Sociedad:**
    * **Refuerzo de Estereotipos:** Si un sistema de recomendación o resumen basado en este modelo prioriza contenido de "hombres viejos" e ignora contenido relevante sobre "hombres jóvenes", se **limita** la visión del público sobre la diversidad de la realidad.
      
    * **Discriminación:** La asociación de términos como "refugiado" o "inmigrante" con connotaciones negativas (cercanía a "malo") puede influir en la forma en que los sistemas de IA procesan, resumen o clasifican noticias, llevando a la **perpetuación de prejuicios** y contribuyendo a la discriminación y la estigmatización social de estos grupos.

### **Propuestas para un Uso Más Responsable de PLN en Noticias**

Para mitigar los sesgos y promover un uso ético del PLN en este contexto, se proponen las siguientes acciones:

* **1. Balanceo y Diversificación del *Dataset*:**
    * **Intervención en Datos:** No solo recolectar más datos, sino balancear activamente el corpus. Por ejemplo, garantizar que haya una representación equitativa de **"hombre joven"** y **"mujer vieja"** en contextos positivos y neutros.
      
    * **Curación de Datos:** Incluir noticias de **diversas fuentes y líneas editoriales** para obtener una visión más amplia y menos polarizada.

* **2. Supervisión Humana y Auditoría:**
    * **Auditoría Constante:** Realizar auditorías de sesgos periódicas, similares a este ejercicio, para identificar y medir las asociaciones no deseadas.
    * **Validación Humana:** Incorporar expertos en ética y diversidad para validar las decisiones críticas de los modelos.

* **3. Transparencia y Explicabilidad:**
    * **Documentación Clara:** Documentar cómo se entrenó el modelo, las limitaciones del *dataset* y los sesgos que se sabe que contiene.
    * **Modelos Explicables:** Utilizar técnicas que permitan entender **por qué** el modelo tomó una decisión, facilitando la identificación de si el sesgo fue un factor determinante.

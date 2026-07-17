# 📊 Análisis de Comportamiento y Retención de Clientes - ConnectaTel 📡

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-Data_Manipulation-150458.svg)
![Seaborn](https://img.shields.io/badge/Seaborn-Data_Visualization-blueviolet.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626.svg)

## 📖 Descripción del Proyecto
Este proyecto de análisis de datos se enfoca en **ConnectaTel**, una empresa de telecomunicaciones operando en Latinoamérica. El objetivo principal es evaluar el comportamiento histórico de los clientes (hasta el año 2024) para perfilar usuarios, detectar patrones de consumo y construir una base sólida para el diseño de estrategias de retención (reducción de Churn) y la optimización de los planes ofrecidos.

## 🎯 Objetivos
* **Limpiar y estandarizar** múltiples fuentes de datos de uso y facturación.
* **Construir un perfil estadístico** unificado para cada cliente.
* **Identificar patrones atípicos** y segmentar a los usuarios según su consumo (Llamadas y Mensajes) y su tipo de plan (Básico vs. Premium).

## 🗂️ Diccionario de Datos
El análisis integra tres conjuntos de datos principales:
* `plans.csv`: Información maestra de los planes actuales (precio, minutos, GB incluidos, costos extra).
* `users_latam.csv`: Demografía y ciclo de vida del cliente (edad, ciudad, fecha de registro, tipo de plan, churn).
* `usage.csv`: Log detallado de la actividad real del usuario (duración de llamadas y cantidad de mensajes).

## 🛠️ Metodología y Pasos del Análisis

### 1. Data Wrangling y Control de Calidad
* **Detección y manejo de Sentinels:** Reemplazo de edades anómalas (`-999`) utilizando la imputación por la mediana para no sesgar la distribución. Tratamiento de ciudades no válidas (`?`) como valores nulos (`<NA>`).
* **Validación Temporal:** Corrección y eliminación de fechas lógicamente imposibles (ej. fechas de registro mayores a 2024).
* **Estandarización:** Unificación de categorías (corrección de errores tipográficos en los registros de SMS/Llamadas).

### 2. Feature Engineering (Agrupación)
Transformación de logs transaccionales a métricas de cliente. Se consolidó una tabla maestra `user_profile` sumandoizando:
* `cant_mensajes`: Total de SMS enviados por usuario.
* `cant_llamadas`: Frecuencia de llamadas realizadas.
* `cant_minutos_llamada`: Volumen total de minutos consumidos.

### 3. Análisis Exploratorio de Datos (EDA)
* Generación de estadísticas descriptivas.
* Creación de visualizaciones (Histogramas comparativos) segmentando las distribuciones de uso de acuerdo con el tipo de plan contratado (`Básico` vs `Premium`).

## 💡 Insights y Conclusiones Preliminares

### Análisis ejecutivo

⚠️ **Problemas detectados en los datos**

- Se detectaron valores atípicos de edad (-999) que fueron imputados con la mediana poblacional para no perder el registro de esos clientes.

- Había variables estructuralmente nulas en llamadas y mensajes debido a la exclusividad del servicio (mensajes sin duración y llamadas sin longitud de texto), lo cual es normal y no representa pérdida de datos.

🔍 **Segmentos por Edad**

- El grueso de nuestros usuarios se concentra en la categoría "Adulto" (30 a 59 años).

- Los segmentos "Jóvenes" tienden a preferir un uso mayor de texto sobre las llamadas tradicionales.

📊 **Segmentos por Nivel de Uso**

- Existe un gran bloque de usuarios clasificados como de "Alto uso" que consistentemente superan los límites base de los planes económicos.

- Los valores extremos (outliers) identificados en llamadas y mensajes no son errores, sino "Heavy Users" que posiblemente están pagando altas tarifas por excedentes.
➡️ Esto sugiere que existe una oportunidad para ofrecer planes ilimitados premium a este segmento de alto consumo.

💡 **Recomendaciones**

- Up-selling: Crear campañas dirigidas a los usuarios del segmento "Alto uso" que actualmente tienen planes básicos, ofreciéndoles un plan Premium que evite cobros sorpresa por excedentes, mejorando su retención.

- Retención: Monitorear a los clientes de "Bajo uso", ya que podrían sentir que están pagando de más por servicios que no consumen y son candidatos probables a churn (abandono). Se podría crear un plan "Lite" para retenerlos.

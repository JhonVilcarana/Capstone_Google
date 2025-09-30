# 🚲 Cyclistic Bike-Share Case Study  
*Google Data Analytics Capstone Project*  

## 📌 Descripción del Proyecto  
Este proyecto corresponde al **Capstone del Certificado de Google Data Analytics**.  
El reto consiste en analizar el comportamiento de los usuarios de **Cyclistic**, un sistema de bicicletas compartidas en Chicago, con el fin de **identificar las diferencias entre usuarios ocasionales (casual riders) y miembros anuales**, y proponer estrategias de marketing para **convertir más usuarios ocasionales en miembros**.  

La investigación sigue las etapas del proceso de análisis de datos:  
**Ask → Prepare → Process → Analyze → Share → Act**  

---

## 🎯 Objetivo de Negocio  
Cyclistic busca aumentar la rentabilidad mediante la **conversión de ciclistas ocasionales en miembros anuales**.  

Preguntas clave:  
1. ¿Cómo usan las bicicletas los miembros anuales vs. los ciclistas ocasionales?  
2. ¿Por qué los ciclistas ocasionales considerarían una membresía anual?  
3. ¿Cómo puede Cyclistic aprovechar los medios digitales para incentivar la conversión?  

---

## 📂 Datos Utilizados  
- **Fuente:** Datos públicos de Divvy/Cyclistic [Divvy Trip Data](https://divvy-tripdata.s3.amazonaws.com/index.html).  
- **Cobertura:** 12 meses (Julio 2024 – Junio 2025).  
- **Formato:** Archivos CSV (~15 GB en total).  
- **Contenido:** ID del viaje, tipo de usuario (`casual` / `member`), inicio y fin de viaje, estaciones, coordenadas GPS, tipo de bicicleta, entre otros.  

---

## 🛠️ Herramientas y Tecnologías  
- **SQL (MySQL):** Limpieza y análisis del dataset consolidado.  
- **Excel / Google Sheets:** Tablas dinámicas y análisis mensual.  
- **PowerPoint:** Presentación ejecutiva para stakeholders.  
- **Python/Pandas (opcional en pruebas):** Validación y exploración de datos.  

---

## 🔄 Proceso de Análisis  

### 1. Preguntar (Ask)  
- Convertir usuarios ocasionales en miembros es más rentable.  
- Entender diferencias de uso para diseñar campañas específicas.  

### 2. Preparar (Prepare)  
- Descarga de 12 archivos CSV.  
- Carga inicial en tabla `raw_trips` en MySQL.  
- Verificación de columnas, tipos de datos y duplicados.  

### 3. Procesar (Process)  
- Limpieza: eliminación de nulos, duplicados y viajes inválidos (<0s o >24h).  
- Normalización: formatos de fecha, categorías (`member` / `casual`).  
- Creación de campos derivados:  
  - `ride_length_sec` → duración en segundos.  
  - `day_of_week` → número de día (1=lunes, …, 7=domingo).  

### 4. Analizar (Analyze)  
- **Hallazgos clave:**  
  - Miembros → viajes cortos y frecuentes (~12 min), sobre todo entre semana.  
  - Ocasionales → viajes más largos (~27–28 min), principalmente fines de semana.  
  - Mayor número total de viajes en **miembros**, pero con menor duración que los casuals.  

### 5. Compartir (Share)  
📊 Visualizaciones clave:  
- **Cantidad de viajes por tipo de usuario y día de semana.**  
- **Duración promedio de viajes por tipo de usuario.**  
- **Patrones mensuales de uso (estacionalidad).**  

*(Puedes incluir aquí imágenes exportadas de tu PPT, por ejemplo en `/images` dentro del repo).*  

### 6. Actuar (Act)  
**Recomendaciones:**  
1. **Segmentación de usuarios**: identificar casuals frecuentes de fin de semana.  
2. **Campañas digitales personalizadas**:  
   - Emails/app notifications con ahorros estimados si fueran miembros.  
   - Publicidad geolocalizada cerca de estaciones concurridas en fines de semana.  
3. **Promociones & gamificación**:  
   - Descuentos progresivos por número de viajes.  
   - Retos y recompensas digitales vinculadas a membresías.  

---

## 📈 Resultados Clave  
- Los **miembros usan la bici como transporte diario**, con viajes cortos y regulares.  
- Los **ocasionales la usan para ocio**, con viajes más largos en fines de semana.  
- Existe un **alto potencial de conversión** de casuals a miembros mediante marketing digital y ofertas personalizadas.  

---

## 📑 Entregables  
- **Presentación ejecutiva (PPT)** con hallazgos visuales.  
- **README en GitHub (este archivo)** documentando el flujo del proyecto.  
- **SQL Scripts** de carga, limpieza y análisis (si deseas añadirlos al repo).  

---

## 👤 Autor  
**Jhon Vilcarana Tintaya**  
- Google Data Analytics Certified  
- Portafolio de Análisis de Datos  

---

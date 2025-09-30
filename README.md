# 🚲 Cyclistic Bike-Share Case Study  
*Google Data Analytics Capstone Project*  

<div align="center">

![SQL](https://img.shields.io/badge/SQL-MySQL-blue?logo=mysql&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-Data%20Cleaning-green?logo=microsoft-excel&logoColor=white)
![Sheets](https://img.shields.io/badge/Google%20Sheets-Analysis-yellow?logo=google-sheets&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-Visualization-orange?logo=tableau&logoColor=white)
![PowerPoint](https://img.shields.io/badge/PowerPoint-Presentation-red?logo=microsoft-powerpoint&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

**Análisis de usuarios para optimizar estrategias de membresía en un sistema de bicicletas compartidas.**

*Transformando datos masivos en insights para decisiones de negocio*

</div>

---

## 📋 Descripción

Este proyecto corresponde al **Capstone del Certificado de Google Data Analytics**.  
El reto consiste en analizar el comportamiento de los usuarios de **Cyclistic**, un sistema de bicicletas compartidas en Chicago, con el fin de **identificar diferencias entre usuarios ocasionales (casual riders) y miembros anuales**, y proponer estrategias de marketing para **convertir más usuarios ocasionales en miembros**.  

---

## 🎯 Objetivo de Negocio  

Cyclistic busca aumentar la rentabilidad mediante la **conversión de ciclistas ocasionales en miembros anuales**.  

Preguntas clave:  
1. ¿Cómo usan las bicicletas los miembros anuales vs. los ciclistas ocasionales?  
2. ¿Qué factores motivarían a los usuarios ocasionales a convertirse en miembros?  
3. ¿Cómo puede el marketing digital aprovechar estos hallazgos?  

---

## 📂 Datos Utilizados  

- **Fuente:** Datos públicos de Divvy/Cyclistic [Divvy Trip Data](https://divvy-tripdata.s3.amazonaws.com/index.html).  
- **Cobertura:** 12 meses (Julio 2024 – Junio 2025).  
- **Formato:** Archivos CSV (~15 GB).  
- **Contenido:** ID de viaje, tipo de usuario (`casual` / `member`), inicio y fin, estaciones, coordenadas GPS, tipo de bicicleta, duración, entre otros.  

---

## 🛠️ Herramientas Utilizadas  

- **SQL (MySQL)** → Integración y limpieza de datos (12M+ registros).  
- **Excel / Google Sheets** → Exploración, tablas dinámicas, métricas clave.  
- **Tableau / Data Studio** → Visualización de patrones de uso.  
- **PowerPoint** → Presentación ejecutiva de hallazgos y recomendaciones.  

---

## 🔄 Proceso de Análisis  

### 1. Preguntar (Ask)  
Definir el objetivo: aumentar la conversión de usuarios ocasionales a miembros.  

### 2. Preparar (Prepare)  
- Descarga y consolidación de 12 meses de datos.  
- Creación de una base unificada en MySQL.  

### 3. Procesar (Process)  
- Eliminación de nulos, duplicados y viajes inválidos (<0s o >24h).  
- Normalización de categorías (`casual` / `member`).  
- Cálculo de campos derivados: duración (`ride_length`), día de la semana, mes.  

### 4. Analizar (Analyze)  
- Miembros → viajes cortos (~12 min) y frecuentes, sobre todo entre semana.  
- Ocasionales → viajes largos (~27 min), principalmente fines de semana.  
- Miembros generan mayor número de viajes totales, pero de menor duración.  

### 5. Compartir (Share)  
📊 Visualizaciones clave:  
- Número de viajes por tipo de usuario y día de semana.  
- Duración promedio de viajes.  
- Estacionalidad mensual del uso.  

### 6. Actuar (Act)  
**Recomendaciones estratégicas:**  
1. Campañas digitales segmentadas para usuarios ocasionales frecuentes de fin de semana.  
2. Promociones que destaquen el ahorro económico de una membresía.  
3. Programas de fidelización y recompensas digitales.  

---

## 📊 Resultados Clave  

- Los **miembros usan la bici como transporte diario** (patrón utilitario).  
- Los **ocasionales la usan como ocio** (patrón recreativo).  
- Se identificó un **alto potencial de conversión** de usuarios casuales a miembros mediante campañas personalizadas.  

---

## 🎥 Presentación Ejecutiva  

La presentación final resume el análisis y las recomendaciones de negocio:  

📑 [Descargar Presentación PDF](./Negro%20y%20Verde%20Bicicleta%20Ilustrada%20Producto%20Presentación.pdf)  

---

## 📁 Estructura del Repositorio  

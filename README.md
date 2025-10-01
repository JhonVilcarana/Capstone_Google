# 🚲 Cyclistic Bike-Share Case Study  
*Google Data Analytics Capstone Project*  

<div align="center">

![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?logo=microsoft-excel&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?logo=tableau&logoColor=white)
![PowerPoint](https://img.shields.io/badge/PowerPoint-FF6F00?logo=microsoft-powerpoint&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

**Análisis de usuarios para optimizar estrategias de membresía en un sistema de bicicletas compartidas.**

*De datos crudos a insights estratégicos con SQL, Excel y Tableau.*

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
2. ¿Qué factores motivan a los usuarios casuales a convertirse en miembros?  
3. ¿Qué estrategias de marketing pueden apoyar esta conversión?  

---

## 🗂️ Dataset  

- **Fuente:** [Divvy Trip Data](https://divvy-tripdata.s3.amazonaws.com/index.html)  
- **Cobertura:** 12 meses (enero – diciembre 2020)  
- **Tamaño:** ~1 GB (CSV cargado en MySQL)  
- **Principales variables:**  
  - `ride_id` → ID único del viaje  
  - `rideable_type` → Tipo de bicicleta  
  - `started_at` y `ended_at` → Tiempos de inicio y fin  
  - `start_station_name`, `end_station_name` → Estaciones  
  - `member_casual` → Tipo de usuario (casual / member)  

---

## 🛠️ Herramientas Utilizadas  

- **MySQL** → Limpieza y transformación de datos masivos (1M+ registros).  
- **Excel** → Validaciones y métricas rápidas.  
- **Tableau** → Visualización interactiva de patrones de uso.  
- **PowerPoint** → Presentación ejecutiva del análisis y recomendaciones.  

---

## 🔄 Proceso de Análisis  

1. **Preguntar (Ask)** → Definir la meta: aumentar la conversión de usuarios casuales en miembros.  
2. **Preparar (Prepare)** → Consolidar 12 meses de datos y cargarlos en MySQL.  
3. **Procesar (Process)** → Limpieza de nulos, duplicados y viajes inválidos. Cálculo de duración y día de la semana.  
4. **Analizar (Analyze)** → Comparación entre usuarios casuales y miembros: frecuencia, duración, patrones semanales y estacionales.  
5. **Compartir (Share)** → Creación de dashboard en Tableau.  
6. **Actuar (Act)** → Recomendaciones estratégicas para marketing.  

---

## 📊 Dashboard Tableau  

![Dashboard Cyclistic](./dashboard_cyclistic.png)  

Componentes principales:  
- 📌 **Comparación anual de uso** (miembros vs. casuales)  
- 📌 **Patrones semanales** (mayor uso entre semana para miembros, fines de semana para casuales)  
- 📌 **Duración promedio de viajes** (casual ~24 min, miembros ~12 min)  
- 📌 **Top 10 estaciones más concurridas**  
- 📌 **Mapa interactivo** de estaciones con más viajes  
- 📌 **Uso mensual** (estacionalidad clara en verano)  

---

## 🔑 Hallazgos Clave  

- 🚲 **Miembros** → viajes más cortos, frecuentes, principalmente entre semana (uso utilitario).  
- 🏖️ **Casuals** → viajes más largos, principalmente en fines de semana (uso recreativo).  
- 📍 Las estaciones más concurridas se ubican en zonas turísticas y céntricas.  
- 💡 Existe un **alto potencial de conversión** de usuarios casuales a miembros mediante campañas segmentadas.  

---

## 🚀 Recomendaciones de Negocio  

1. **Campañas digitales** enfocadas en usuarios casuales frecuentes de fines de semana.  
2. **Promociones de membresía flexible** para turistas y visitantes de corto plazo.  
3. **Destacar beneficios exclusivos** de membresía: viajes ilimitados, disponibilidad prioritaria.  
4. **Optimizar estaciones más concurridas** para mejorar la experiencia del usuario.  

---

## 📁 Estructura del Repositorio  
Capstone_Cyclistic/
├── 📄 SQL/                   # Consultas SQL de limpieza y análisis
├── 📊 Tableau_Dashboard/     # Visualizaciones y dashboard
├── 📑 Case_Study.pdf         # Documento del caso de estudio
├── 📑 Presentation.pdf       # Presentación ejecutiva
└── 📖 README.md              # Este archivo

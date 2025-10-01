# 🚲 Cyclistic Bike-Share Case Study  
*Google Data Analytics Capstone Project*  

<div align="center">

![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?logo=microsoft-excel&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?logo=tableau&logoColor=white)
![PowerPoint](https://img.shields.io/badge/PowerPoint-FF6F00?logo=microsoft-powerpoint&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

**Análisis de usuarios para optimizar estrategias de membresía en un sistema de bicicletas compartidas.**

*De datos crudos a insights estratégicos con MySQL, Excel y Tableau.*

</div>

---

## 📋 Descripción  

Proyecto Capstone del Certificado de Google Data Analytics.  
Se analizó el comportamiento de usuarios de **Cyclistic** (sistema de bicicletas compartidas) para identificar diferencias entre usuarios ocasionales (`casual`) y miembros (`member`), con el objetivo de proponer estrategias que aumenten la conversión de usuarios ocasionales en miembros anuales.

---

## 🎯 Objetivo de negocio  

Desarrollar análisis y recomendaciones que permitan a Cyclistic aumentar la conversión de usuarios casuales a miembros, optimizando campañas de marketing y la operación de estaciones.

Preguntas clave:  
1. ¿Cómo usan las bicicletas los miembros vs. los ocasionales?  
2. ¿Qué factores aumentan la probabilidad de conversión?  
3. ¿Qué acciones de marketing priorizar para lograr mayor conversión?

---

## 🗂️ Datos utilizados  

- **Fuente:** Divvy / Cyclistic (archivos públicos).  
- **Cobertura:** 12 meses (ej.: enero–diciembre 2020).  
- **Tamaño bruto:** ~1 GB (CSV) — cargado y procesado en MySQL.  
- **Variables principales (ejemplos):**
  - `ride_id` (ID viaje)
  - `rideable_type`
  - `started_at`, `ended_at`
  - `start_station_name`, `start_lat`, `start_lng`
  - `end_station_name`, `end_lat`, `end_lng`
  - `member_casual` (casual / member)

---

## 🛠️ Herramientas utilizadas

- **MySQL** — ingestión, limpieza y agregación de datos (tablas y vistas).  
- **Microsoft Excel** — validación rápida, muestreos y exportes puntuales.  
- **Tableau Public** — dashboard interactivo y mapa de estaciones.  
- **PowerPoint** — presentación ejecutiva del caso.  

---

## 🔗 Recursos públicos / Archivos incluidos

- Dashboard en Tableau Public:  
  https://public.tableau.com/views/Libro1_17510448553710/Dashboard1?:language=es-ES&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

- Archivos en este repositorio (añadir los archivos al repo):
  - `Case Study 1_How does a bike-share navigate speedy success.pdf`
  - `Negro y Verde Bicicleta Ilustrada Producto Presentación.pdf`
  - `SQL/` (consultas y scripts)
  - `Tableau_Dashboard/dashboard_cyclistic.twbx` (opcional - si no quieres subir .twbx, dejar enlace a Tableau Public)
  - `README.md` (este archivo)

---

## 🔄 Proceso de análisis (resumen)

1. **Prepare**: Consolidación de CSVs y carga en MySQL (tabla `trips_raw`).  
2. **Process**: Limpieza (viajes inválidos, nulos, duplicados) y creación de variables derivadas (`ride_length_min`, `dia_semana`, `mes`).  
3. **Analyze**: Agregados por tipo de usuario, día de la semana, mes, top estaciones, mapas.  
4. **Visualize**: Dashboard en Tableau con mapas y comparativas (anual, semanal y mensual).  
5. **Act**: Recomendaciones de marketing y operación.

---

## ✅ Consultas SQL clave (ejemplos listos para usar)

> Asuma que los datos crudos están en la tabla `trips_raw`. Ajustar nombres según tu esquema.

### 1) Crear tabla limpia con duración en minutos y eliminar viajes inválidos
```sql
CREATE TABLE trips_clean AS
SELECT
  ride_id,
  rideable_type,
  started_at,
  ended_at,
  start_station_name,
  start_station_id,
  end_station_name,
  end_station_id,
  start_lat,
  start_lng,
  end_lat,
  end_lng,
  member_casual,
  TIMESTAMPDIFF(SECOND, started_at, ended_at)/60.0 AS ride_length_min,
  DAYNAME(started_at) AS dia_semana,
  MONTH(started_at) AS mes,
  YEAR(started_at) AS anio
FROM trips_raw
WHERE started_at IS NOT NULL
  AND ended_at IS NOT NULL
  AND TIMESTAMPDIFF(SECOND, started_at, ended_at) BETWEEN 30 AND 86400; -- entre 30s y 24h

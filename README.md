# 🚲 Cyclistic Bike-Share Case Study  
*Google Data Analytics Capstone Project*  

<div align="center">

![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white)
![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?logo=microsoft-excel&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?logo=tableau&logoColor=white)
![PowerPoint](https://img.shields.io/badge/Microsoft_PowerPoint-B7472A?logo=microsoft-powerpoint&logoColor=white)

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

- **Fuente:** Divvy / Cyclistic (https://divvy-tripdata.s3.amazonaws.com/index.html).  
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

## 🔄 Proceso de análisis


1. **Ask**: Consolidación de CSVs y carga en MySQL (Identificar las diferencias en patrones de uso entre ciclistas casuales y miembros anuales, para diseñar estrategias que conviertan a los usuarios ocasionales en socios anuales).  
1. **Prepare**: Consolidación de CSVs y carga en MySQL (tabla `trips_raw`).  
2. **Process**: Limpieza (viajes inválidos, nulos, duplicados) y creación de variables derivadas (`ride_length_min`, `dia_semana`, `mes`).  
3. **Analyze**: Agregados por tipo de usuario, día de la semana, mes, top estaciones, mapas.  
4. **Visualize**: Dashboard en Tableau con mapas y comparativas (anual, semanal y mensual).  
5. **Act**: Recomendaciones de marketing y operación.

---

## 📊 Consultas SQL principales

El análisis se apoyó en **MySQL** para limpiar, transformar y explorar más de 12 millones de registros.  
A continuación, se listan las consultas más relevantes utilizadas:

---

### 1. Carga de datos y limpieza inicial
Se cargaron los CSV en la base de datos, transformando fechas y duraciones de viaje a segundos.
```sql
LOAD DATA LOCAL INFILE '/ruta/dataset.csv'
INTO TABLE trips
CHARACTER SET utf8mb4
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(@ride_id,@rideable_type,@started_at_txt,@ended_at_txt,
 @start_station_name,@start_station_id,
 @end_station_name,@end_station_id,
 @start_lat,@start_lng,@end_lat,@end_lng,
 @member_casual,@ride_length_txt,@day_of_week_txt)
SET
  ride_id            = @ride_id,
  rideable_type      = @rideable_type,
  started_at         = STR_TO_DATE(@started_at_txt, '%e/%m/%y %H:%i'),
  start_station_name = NULLIF(@start_station_name,''),
  end_station_name   = NULLIF(@end_station_name,''),
  member_casual      = @member_casual,
  @rl := REPLACE(@ride_length_txt, ',', '.'),
  ride_length_sec    = CASE
                         WHEN @rl REGEXP '^[0-9]{1,2}:[0-9]{2}:[0-9]{2}(\.[0-9]+)?$'
                           THEN TIME_TO_SEC(@rl)
                         WHEN @rl REGEXP '^[0-9]{1,2}:[0-9]{2}(\.[0-9]+)?$'
                           THEN CAST(SUBSTRING_INDEX(@rl,':',1) AS DECIMAL(10,3))*60
                              + CAST(SUBSTRING_INDEX(@rl,':',-1) AS DECIMAL(10,3))
                         ELSE NULL
                       END,
  ended_at           = DATE_ADD(STR_TO_DATE(@started_at_txt, '%e/%m/%y %H:%i'),
                                INTERVAL ride_length_sec SECOND),
  day_of_week        = CASE LOWER(@day_of_week_txt)
                         WHEN 'monday' THEN 1
                         WHEN 'tuesday' THEN 2
                         WHEN 'wednesday' THEN 3
                         WHEN 'thursday' THEN 4
                         WHEN 'friday' THEN 5
                         WHEN 'saturday' THEN 6
                         WHEN 'sunday' THEN 7
                         WHEN 'lunes' THEN 1
                         WHEN 'martes' THEN 2
                         WHEN 'miércoles' THEN 3
                         WHEN 'miercoles' THEN 3
                         WHEN 'jueves' THEN 4
                         WHEN 'viernes' THEN 5
                         WHEN 'sábado' THEN 6
                         WHEN 'sabado' THEN 6
                         WHEN 'domingo' THEN 7
                         ELSE NULL
                       END;
```
### 2. Duración promedio por día de la semana y tipo de usuario
```sql
SELECT
  member_casual,
  ROUND(AVG(CASE WHEN day_of_week = 1 THEN ride_length_sec END)/60, 2) AS Lunes,
  ROUND(AVG(CASE WHEN day_of_week = 2 THEN ride_length_sec END)/60, 2) AS Martes,
  ROUND(AVG(CASE WHEN day_of_week = 3 THEN ride_length_sec END)/60, 2) AS Miercoles,
  ROUND(AVG(CASE WHEN day_of_week = 4 THEN ride_length_sec END)/60, 2) AS Jueves,
  ROUND(AVG(CASE WHEN day_of_week = 5 THEN ride_length_sec END)/60, 2) AS Viernes,
  ROUND(AVG(CASE WHEN day_of_week = 6 THEN ride_length_sec END)/60, 2) AS Sabado,
  ROUND(AVG(CASE WHEN day_of_week = 7 THEN ride_length_sec END)/60, 2) AS Domingo
FROM trips
WHERE ride_length_sec IS NOT NULL
GROUP BY member_casual;
```
### 3. Número de viajes por día de la semana
```sql
SELECT
  member_casual,
  SUM(CASE WHEN day_of_week = 1 THEN 1 ELSE 0 END) AS Lunes,
  SUM(CASE WHEN day_of_week = 2 THEN 1 ELSE 0 END) AS Martes,
  SUM(CASE WHEN day_of_week = 3 THEN 1 ELSE 0 END) AS Miercoles,
  SUM(CASE WHEN day_of_week = 4 THEN 1 ELSE 0 END) AS Jueves,
  SUM(CASE WHEN day_of_week = 5 THEN 1 ELSE 0 END) AS Viernes,
  SUM(CASE WHEN day_of_week = 6 THEN 1 ELSE 0 END) AS Sabado,
  SUM(CASE WHEN day_of_week = 7 THEN 1 ELSE 0 END) AS Domingo
FROM trips
GROUP BY member_casual;
```
### 4. Duración promedio por tipo de usuario
```sql
SELECT 
  member_casual,
  SEC_TO_TIME(AVG(ride_length_sec)) AS promedio_duracion
FROM trips
WHERE ride_length_sec IS NOT NULL
GROUP BY member_casual;
```
### 5. Viajes mensuales
```sql
SELECT DATE_FORMAT(started_at, '%Y-%m') AS periodo,
       COUNT(*) AS total_viajes
FROM trips
GROUP BY periodo
ORDER BY periodo;
```
### 6. Top 10 estaciones más usadas
```sql
SELECT start_station_name,
       COUNT(*) AS total_viajes
FROM trips
WHERE start_station_name IS NOT NULL
GROUP BY start_station_name
ORDER BY total_viajes DESC
LIMIT 10;
```

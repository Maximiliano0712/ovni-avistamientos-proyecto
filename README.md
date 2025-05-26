# Proyecto GSP823: Análisis de Avistamientos OVNI

Este proyecto corresponde al laboratorio GSP823 de Google Skill Boosts. Utilizamos Google Cloud para cargar, procesar, consultar y visualizar datos de avistamientos OVNI en EE.UU.

---

## 📂 Estructura del proyecto

| Carpeta        | Descripción                                 |
|----------------|---------------------------------------------|
| `/data`        | Archivo CSV original                        |
| `/sql`         | Consultas en BigQuery                       |
| `/images`      | Capturas de Looker Studio y la consola GCP |
| `/site`        | Código fuente del sitio del proyecto        |

---

## 🧪 Herramientas utilizadas

- Google Cloud Storage
- Cloud Dataprep
- BigQuery
- Looker Studio
- GitHub Pages

---

## 🚀 Flujo del Proyecto

### 1. Subida del archivo
- Se creó el bucket `maximiliano-herrera`
- Se subió el archivo `ufo_sighting.csv` a Cloud Storage

### 2. Preparación del archivo
- Se usó Cloud Dataprep para:
  - Eliminar nulos
  - Normalizar columnas
  - Confirmar tipos de datos

### 3. Creación del dataset
- Dataset: `ovni`
- Tabla: `avistamientos`

### 4. Consultas SQL en BigQuery

#### 📌 Top 5 formas de objetos más vistos:
```sql
SELECT 
  UFO_shape,
  COUNT(*) AS Sightings
FROM 
  `ovni.avistamientos`
WHERE 
  country = 'us'
GROUP BY 
  UFO_shape
ORDER BY 
  Sightings DESC
LIMIT 5;
#### 📌 avistamientos por año:
SELECT 
  EXTRACT(YEAR FROM DATETIME(Date_time)) AS Year,
  COUNT(*) AS Sightings
FROM 
  `ovni.avistamientos`
WHERE 
  country = 'us'
GROUP BY 
  Year
ORDER BY 
  Sightings DESC;
#### 📌 avistyamientos por estado:
SELECT 
  `state/province` AS State,
  COUNT(*) AS Sightings
FROM 
  `ovni.avistamientos`
WHERE 
  country = 'us'
GROUP BY 
  State
ORDER BY 
  Sightings DESC;


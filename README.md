# Análisis de Eventos Lunares 🌕

Análisis de eventos astronómicos diseñado para procesar y analizar grandes volúmenes de datos sobre eventos astronómicos utilizando PySpark y Databricks.

## 📋 Tabla de Contenidos
- [Descripción General](#descripción-general)
- [Arquitectura](#arquitectura)
- [Requisitos](#requisitos)
- [Instalación](#instalación)
- [Uso](#uso)
- [Diseño del Modelo de Datos](#diseño-del-modelo-de-datos)
- [Flujo de Trabajo Git](#flujo-de-trabajo-git)
- [Stack Tecnológico](#stack-tecnológico)

## 🎯 Descripción General

Este proyecto implementa un pipeline de datos completo para el procesamiento y análisis de eventos astronómicos, con enfoque particular en eventos lunares. El sistema maneja:
- Generación de datos simulados (50GB+)
- Procesamiento ETL con PySpark
- Modelado dimensional para análisis
- Almacenamiento optimizado en formato Parquet

## 🏗 Arquitectura

```
astronomical_events/
├── src/
│   ├── data_simulation.ipynb  # Scripts de generación de datos
│   ├── data_process.ipynb     # Scripts de procesamiento ETL
│   └── analysis.ipynb         # Notebooks y scripts de análisis
│
│   - opcional usando un bucket especifico de databricks, gcp, aws, azure│
├── data/
│   ├── raw/               # Datos simulados sin procesar
│   └── processed/         # Datos intermedios procesados
│
│   - en nuestro caso usamos el Unity Catalog de  databricks, que se almacena en su propio metastore 
├── default.astronomical_events # Datos simulados sin procesar
├── default.lunar_events        # Datos lunares por año
├
├── datamart/              # Datos finales en formato Parquet
├── docs/                  # Documentación y diagramas
└── tests/                 # Tests unitarios y de integración
```

## 📋 Requisitos

- Python 3.9.19
- Apache Spark 3.3.2
- Scala 2.12
- Databricks Runtime 12.2 LTS
- Git

## 🚀 Instalación

1. Clonar el repositorio:
```bash
git clone https://github.com/erlinares/astronomical_events.git
```


## 💻 Uso

### Generación de Datos
```python
python src/data_simulation.ipynb --size 50GB
```

### Procesamiento ETL
```python
python data_process.ipynb

```

## 📊 Diseño del Modelo de Datos

### Esquema Dimensional
```
FACT_LUNAR_EVENTS
├── event_id (PK)
├── event_type (FK)
├── time_key (FK)
├── location_key (FK)
└── details

DIM_EVENT_TYPE
├── event_type_key (PK)
├── type_name
├── category
└── description

DIM_TIME
├── time_key (PK)
├── timestamp
├── year
├── month
├── day
├── quarter
└── season

DIM_LOCATION
├── location_key (PK)
├── region
├── country
├── continent
├── hemisphere
├── latitude
├── longitude
└── timezone
```


### Justificación del Diseño
- **Modelo Estrella**: Optimizado para consultas analíticas
- **Particionamiento**: Por año para mejorar el rendimiento
- **Formato Parquet**: Compresión eficiente y lectura columnar

## 🌿 Flujo de Trabajo Git

### Branches Principales
- `main`: Código en producción
- `develop`: Rama de desarrollo principal

### Feature Branches
1. `feature/simulate-data`: Generación de datos
2. `feature/process-data`: Procesamiento ETL
3. `feature/datamart-design`: Diseño dimensional



## 🛠 Stack Tecnológico

- **Procesamiento**: Apache Spark, PySpark
- **Almacenamiento**: Parquet, Delta Lake
- **Orquestación**: Workflows(databricks) ** No se realizó por la versionéis comunnity
- **Desarrollo**: Python, Git
- **Plataforma**: Databricks
- **Testing**: no aplica

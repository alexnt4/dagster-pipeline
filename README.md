# Pipeline de Datos NYC Taxi con Dagster

Este repositorio contiene un pipeline ELT desarrollado con Dagster utilizando el dataset de NYC Taxi, implementando las funcionalidades principales de orquestación de datos incluyendo:

1. Orquestación declarativa basada en Assets
2. Procesamiento ELT con DuckDB
3. Backfill de datos usando Particiones
4. Configuración de Schedules y Jobs
5. Políticas de Auto Materialización
6. Visualización de métricas y análisis

## Instalación

Clona el repositorio e instala las dependencias usando uv:

```bash
git clone https://github.com/alexnt4/dagster-pipeline
cd dagster-pipeline
uv sync
```

Esto creará automáticamente el entorno virtual e instalará todas las dependencias necesarias.

Luego, inicia el servidor web de Dagster:

```bash
dg dev
```

Abre http://localhost:3000 en tu navegador para acceder a la interfaz de Dagster.

## Arquitectura del Sistema

<div align="center">
  <img src="img/archi.png" alt="Arquitectura del pipeline" width="500">
</div>


El pipeline procesa datos de taxis de NYC siguiendo un patrón ELT (Extract, Load, Transform):

- **Extracción**: Datos de viajes de taxi desde archivos fuente
- **Carga**: Almacenamiento en DuckDB como data warehouse
- **Transformación**: Agregaciones y métricas calculadas
- **Visualización**: Dashboards y gráficos para análisis

### Assets Principales

- `taxi_zones_file` / `taxi_zones`: Datos de zonas de taxi de NYC
- `taxi_trips_file` / `taxi_trips`: Registros de viajes individuales
- `manhattan_stats`: Estadísticas específicas de Manhattan
- `manhattan_map`: Visualización geográfica de datos
- `trips_by_week`: Análisis temporal agregado por semana

## Características Implementadas

### 📊 **Assets y Materialización**
Los assets representan objetos en almacenamiento persistente que capturan el estado de los datos en diferentes etapas del pipeline.


<div align="center">
  <img src="img/dags.png" alt="Assets y dependencias" width="800">
</div>


### 🔄 **Particiones**
Implementación de particionado temporal para procesar datos históricos de manera eficiente y permitir backfills selectivos.

### ⏰ **Schedules y Jobs**
Configuración de ejecuciones automáticas y programadas para mantener los datos actualizados.

### 🎯 **Auto Materialización**
Políticas automáticas que determinan cuándo regenerar assets basándose en dependencias y cambios upstream.

### 📈 **Visualización**

<div align="center">
  <img src="img/map.png" alt="Mapa de Manhattan con datos de taxi" width="400">
</div>


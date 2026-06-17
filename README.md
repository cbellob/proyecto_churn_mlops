# Proyecto Churn MLOps

Este proyecto corresponde a una práctica del módulo de ML-Ops y Puesta en Producción.

El objetivo es construir una estructura básica de trabajo para un proyecto de Machine Learning que permita:

* Preparar datos.
* Entrenar un modelo.
* Evaluar métricas.
* Guardar el modelo entrenado.
* Exponer el modelo mediante una API.
* Ejecutar pruebas básicas.
* Desplegar el servicio utilizando Docker.

## Problema del proyecto

Se trabajará con un caso simplificado de predicción de abandono de clientes, conocido como churn.

El modelo intentará predecir si un cliente podría abandonar un servicio, utilizando variables como edad, antigüedad, saldo promedio, reclamos y uso de aplicación móvil.

## Estructura del proyecto

```text
proyecto_churn_mlops
├── data
├── notebooks
├── src
├── models
├── api
├── tests
├── docs
├── README.md
├── Dockerfile
├── .dockerignore
└── requirements.txt
```

## Carpetas principales

* `data`: contiene los datos del proyecto.
* `notebooks`: contiene análisis exploratorios.
* `src`: contiene los scripts principales del modelo.
* `models`: contiene el modelo entrenado.
* `api`: contiene la API del modelo.
* `tests`: contiene pruebas automáticas.
* `docs`: contiene documentación y métricas.

## Flujo del proyecto

El flujo básico implementado es:

1. Preparar los datos.
2. Entrenar el modelo.
3. Evaluar el modelo.
4. Guardar el modelo entrenado.
5. Crear una API con FastAPI.
6. Contenerizar la aplicación con Docker.
7. Ejecutar y probar el servicio.

## Requisitos previos

Para ejecutar este proyecto es necesario contar con:

* Python 3.11 o superior.
* Docker Desktop instalado.
* Git.
* Las dependencias especificadas en `requirements.txt`.

## Ejecución local

1. Clonar el repositorio:

```bash
git clone <url-del-repositorio>
cd proyecto_churn_mlops
```

2. Instalar las dependencias:

```bash
pip install -r requirements.txt
```

3. Ejecutar la API:

```bash
uvicorn api.main:app --reload
```

4. Abrir la documentación interactiva:

```text
http://127.0.0.1:8000/docs
```

## Despliegue con Docker

Construir la imagen:

```bash
docker build -t churn-api-bello .
```

Ejecutar el contenedor:

```bash
docker run -d -p 8000:8000 --name churn-api-bello churn-api-bello
```

Verificar que el contenedor esté activo:

```bash
docker ps
```

## Endpoints disponibles

- `GET /` : confirma que el servicio está activo.
- `GET /health` : verifica el estado de la API y del monitoreo.
- `GET /metrics` : muestra métricas acumuladas del servicio.
- `GET /info` : devuelve información general de la API y del modelo.
- `POST /predict` : realiza la predicción de churn.

### Ejemplo de respuesta de `/info`

```json
{
    "nombre_api": "API predictiva de churn",
    "autor": "Carolina Bello Banzer",
    "version_modelo": "modelo_churn_v1",
    "version_api": "2.0.0",
    "mejora_tecnica": "Endpoint informativo agregado como personalización técnica"
}
```

## Pipeline del proyecto

```text
Datos CSV
    ↓
Preparación de datos
(src/preparar_datos.py)
    ↓
Entrenamiento del modelo
(src/entrenar_modelo.py)
    ↓
Modelo entrenado
(models/modelo_churn_v1.joblib)
    ↓
API FastAPI
(api/main.py)
    ├── GET /
    ├── GET /health
    ├── GET /metrics
    ├── GET /info
    └── POST /predict
    ↓
Monitoreo básico
    ├── Logging
    ├── Métricas
    ├── Latencia
    └── Detección de anomalías
    ↓
Docker
(Dockerfile + Contenedor)
    ↓
Cliente / Usuario
```

## Control de versiones

Este proyecto utiliza Git para registrar cambios y GitHub para respaldar el repositorio en la nube.

El uso de commits permite mantener trazabilidad sobre los cambios realizados en el código, la documentación y la estructura del proyecto.

## Mejora técnica implementada

Como mejora técnica diferenciadora respecto al proyecto base trabajado en aula, se incorporó una primera capa de observabilidad y monitoreo mediante logging a archivo y consola, medición de latencia con middleware, métricas acumuladas del servicio, detección de valores fuera del rango histórico y endpoints adicionales (`/metrics` y `/info`) para consultar información del modelo y del comportamiento de la API.

## Monitoreo

El endpoint `/metrics` permite consultar información acumulada del servicio, incluyendo:

- Número total de solicitudes.
- Errores de validación.
- Errores internos.
- Predicciones válidas.
- Predicciones de alto y bajo riesgo.
- Latencia promedio y máxima.
- Códigos HTTP devueltos por la API.

## Autor

Carolina Bello Banzer

Maestría en Ciencia de Datos e Inteligencia Artificial

Módulo: ML-Ops y Puesta en Producción

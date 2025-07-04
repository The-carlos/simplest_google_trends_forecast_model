# simplest_google_trends_forecast_model
A simple google trends monthly forecast model for Mexico and USA countries focused in MLOps results.

# 🧭 Etapas del Proyecto
## 1. Extracción de datos desde BigQuery
Usarás el cliente Python de BigQuery.

Consulta al dataset público de Google Trends filtrando:

Término: `MLOps`

Ubicación: `MX` y `US`

Frecuencia: mensual (puede que tengas que agregar esto vía agregación).

Validaremos que haya suficiente historia temporal para poder hacer un forecast sencillo.

## 2. Procesamiento de los datos
Agrupación mensual.

Transformación a formato compatible con modelos de serie de tiempo (ej. ds, y para Prophet).

Separación de series: México y USA.

## 3. Entrenamiento del modelo
Puedes usar un modelo sencillo:

`Prophet` (rápido y enfocado en tiempos).

Entrenamiento por país.

Guardado de los modelos con joblib.

## 4. Construcción de la API con FastAPI
Endpoint: `POST /predict`

Input: país y horizonte de tiempo (ej. próximos 3 meses).

Output: predicciones en JSON.

Carga del modelo entrenado desde disco.

## 5. Dockerización
`Dockerfile` que incluya FastAPI, modelos, dependencias.

Exponer el puerto 8080 (requerido por Cloud Run).

## 6. Despliegue en GCP
Subida de la imagen a Artifact Registry.

Despliegue en Cloud Run:

Configuración pública (sin autenticación).

Uso de variables de entorno si es necesario.

Test del endpoint en producción.

## 7. Pruebas y monitoreo
Probar con curl o Postman.

Validar respuestas.

(Opcional) Integrar logs o monitoreo básico.

## 📁 Estructura del Proyecto

Este repositorio sigue una estructura modular para facilitar el desarrollo, entrenamiento y despliegue de un modelo de forecasting basado en datos de Google Trends.

simplest_google_trends_forecast_model/
├── data/        `Archivos de datos descargados o procesados`

├── notebooks/   `Notebooks de exploración y prototipado`

│ └── eda.ipynb

├── model/        `Código para entrenamiento y serialización del modelo`

│ └── train_model.py

├── api/          `Servicio FastAPI para servir el modelo`

│ └── main.py

├── docker/       `Archivos relacionados a la construcción del contenedor`

│ └── Dockerfile

├── gcp/          `Scripts de despliegue e infraestructura en GCP`

│ └── cloudrun_deploy.sh

├── requirements.txt `Dependencias del proyecto`

├── .gitignore    `Exclusiones de Git`

└── README.md     `Documentación principal del proyecto`


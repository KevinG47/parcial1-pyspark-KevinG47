# Parcial 1 - Análisis Exploratorio COVID-19 Colombia 🇨🇴
**Curso:** Machine Learning con PySpark y Docker | 2026-I  
**Estudiante:** Kevin G  
**Universidad:** Universidad Santo Tomás

## ¿De qué trata este proyecto?
Este repositorio contiene el análisis exploratorio del dataset de casos 
de COVID-19 en Colombia. Se trabajó con PySpark dentro de un contenedor 
Docker para garantizar que el entorno sea reproducible.

## Dataset
El archivo CSV no está incluido porque pesa 1.09 GB y GitHub no permite 
archivos tan grandes. Para reproducir el análisis hay que descargarlo manualmente:

1. Ir a este enlace de Kaggle:  
   https://www.kaggle.com/datasets/josetroyatoscano/covid19-colombia-complete-dataset-dec-2023
2. Renombrarlo a: `dataset.csv`
3. Pegarlo en la carpeta: `data/`

## Estructura del repositorio
```
parcial1-pyspark-KevinG47/
├── docker-compose.yml
├── data/dataset.csv
├── notebooks/analisis_exploratorio.ipynb
└── README.md
```

## ¿Cómo correr el proyecto?
```bash
docker-compose up
```
Después de ejecutar ese comando, abrir el navegador en http://localhost:8888

## Explicación del docker-compose.yml

**`version: '3.8'`**  
Le dice a Docker qué versión de la sintaxis estamos usando para escribir el archivo.

**`services`**  
Acá se definen los contenedores que va a levantar Docker. En este caso solo necesitamos uno que tenga Jupyter con PySpark.

**`image: jupyter/pyspark-notebook:latest`**  
Es la imagen que usamos, ya viene con todo instalado (Python, PySpark, Jupyter), entonces no toca instalar nada manualmente.

**`ports: "8888:8888"`**  
Esto conecta el puerto del contenedor con el de nuestro computador, básicamente es lo que nos permite abrir Jupyter en el navegador.

**`volumes`**  
Sirven para que los archivos que creamos dentro del contenedor no se pierdan cuando lo apaguemos. Conectan las carpetas locales con las del contenedor.

**`JUPYTER_ENABLE_LAB=yes`**  
Le indica al contenedor que abra JupyterLab en vez de la versión clásica de Jupyter.
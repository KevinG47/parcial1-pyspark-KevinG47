# Parcial 1 - Análisis Exploratorio COVID-19 Colombia
**Curso:** Machine Learning con PySpark y Docker | 2026-I  
**Estudiante:** Kevin Leonardo Chaparro Reyes  
**Universidad:** Universidad Santo Tomás

## ¿De qué trata este proyecto?
Este repositorio contiene el análisis exploratorio del dataset de casos 
de COVID-19 en Colombia. Se trabajó con PySpark dentro de un contenedor 
Docker para garantizar que el entorno sea reproducible.

El análisis incluye estadística descriptiva, pruebas de hipótesis, 
correlaciones, visualizaciones y análisis de evolución temporal de 
la pandemia en Colombia.

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

## Cómo ejecutar el proyecto paso a paso

Sigue estos pasos en orden para correr el proyecto sin problemas:

### Requisitos previos
Antes de empezar asegúrate de tener instalado:
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) 
- [Git](https://git-scm.com/downloads)

### Paso 1 - Clonar el repositorio
Abre una terminal y ejecuta:
```bash
git clone https://github.com/KevinG47/parcial1-pyspark-KevinG47.git
cd parcial1-pyspark-KevinG47
```

### Paso 2 - Descargar el dataset
1. Ir a: https://www.kaggle.com/datasets/josetroyatoscano/covid19-colombia-complete-dataset-dec-2023
2. Crear una cuenta en Kaggle si no tienes una (es gratis)
3. Descargar el archivo CSV
4. Renombrarlo a `dataset.csv`
5. Copiarlo dentro de la carpeta `data/`

### Paso 3 - Abrir Docker Desktop
Abre Docker Desktop y espera a que esté corriendo 
(el ícono de la ballena debe estar estable, no animado)

### Paso 4 - Levantar el contenedor
En la terminal, estando dentro de la carpeta del proyecto ejecuta:
```bash
docker-compose up
```
La primera vez puede tardar varios minutos porque descarga la imagen. 
Es normal, hay que esperar.

### Paso 5 - Abrir JupyterLab
Cuando en la terminal aparezca un mensaje con una URL como esta:
```
http://127.0.0.1:8888/lab?token=...
```
Copia esa URL completa (con el token) y pégala en el navegador.

### Paso 6 - Abrir el notebook
1. En el panel izquierdo de JupyterLab hacer doble clic en la carpeta `work`
2. Luego doble clic en `notebooks`
3. Abrir el archivo `analisis_exploratorio.ipynb`
4. Ejecutar todas las celdas con: `Kernel` → `Restart Kernel and Run All Cells`

### Para detener el contenedor
Cuando termines, en la terminal presiona `Ctrl + C` y luego ejecuta:
```bash
docker-compose down
```

## Contenido del notebook
1. Introducción y contexto del dataset
2. Carga y exploración inicial
3. Estadística descriptiva (variables numéricas y categóricas)
4. Consultas con Spark SQL
5. Correlaciones y pruebas estadísticas
6. Análisis de evolución temporal
7. Conclusiones

## Principales hallazgos
- El dataset contiene 6.387.145 casos registrados entre marzo 2020 
  y diciembre 2023 en Colombia.
- El 97.11% de los casos fueron leves, confirmando que el COVID-19 
  fue altamente contagioso pero con baja mortalidad.
- Los hombres tuvieron una tasa de fallecimiento del 2.92% frente 
  al 1.65% de las mujeres (Chi-cuadrado p≈0).
- La edad promedio de los fallecidos fue de 68.63 años vs 39.21 años 
  en recuperados (Mann-Whitney p≈0).
- Se identificaron claramente 4 olas del COVID en Colombia, siendo 
  mayo-junio 2021 la más letal.

## Explicación del docker-compose.yml

**`version: '3.8'`**  
Le dice a Docker qué versión de la sintaxis estamos usando para escribir el archivo.

**`services`**  
Acá se definen los contenedores que va a levantar Docker. En este caso 
solo necesitamos uno que tenga Jupyter con PySpark.

**`image: jupyter/pyspark-notebook:latest`**  
Es la imagen que usamos, ya viene con todo instalado (Python, PySpark, Jupyter), 
entonces no toca instalar nada manualmente.

**`ports: "8888:8888"`**  
Esto conecta el puerto del contenedor con el de nuestro computador, 
básicamente es lo que nos permite abrir Jupyter en el navegador.

**`volumes`**  
Sirven para que los archivos que creamos dentro del contenedor no se pierdan 
cuando lo apaguemos. Conectan las carpetas locales con las del contenedor.

**`JUPYTER_ENABLE_LAB=yes`**  
Le indica al contenedor que abra JupyterLab en vez de la versión clásica 
de Jupyter.
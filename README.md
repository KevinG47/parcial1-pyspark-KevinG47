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

### Requisitos previos
Antes de empezar asegúrate de tener instalado:
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Git](https://git-scm.com/downloads)
- [Visual Studio Code](https://code.visualstudio.com/) (recomendado)

---

### Paso 1 - Clonar el repositorio

1. Abre **Visual Studio Code**
2. En el menú superior haz clic en **Terminal** → **New Terminal**  
   (se abrirá una ventana negra en la parte inferior de la pantalla)
3. En esa terminal escribe el siguiente comando y presiona Enter:
```bash
git clone https://github.com/KevinG47/parcial1-pyspark-KevinG47.git
```
4. Esto creará una carpeta llamada `parcial1-pyspark-KevinG47` en tu computador
5. Ahora entra a esa carpeta con este comando:
```bash
cd parcial1-pyspark-KevinG47
```

---

### Paso 2 - Descargar el dataset
1. Entra a este enlace:  
   https://www.kaggle.com/datasets/josetroyatoscano/covid19-colombia-complete-dataset-dec-2023
2. Si no tienes cuenta en Kaggle, créala gratis con tu correo
3. Haz clic en el botón **Download** (arriba a la derecha)
4. Se descargará un archivo comprimido, descomprímelo
5. Busca el archivo `.csv` que salió al descomprimir
6. **Renómbralo** a `dataset.csv` (clic derecho → Cambiar nombre)
7. **Muévelo** a la carpeta `data/` que está dentro del proyecto  
   La ruta debe quedar así: `parcial1-pyspark-KevinG47/data/dataset.csv`

---

### Paso 3 - Abrir Docker Desktop
1. Busca **Docker Desktop** en tu computador y ábrelo
2. Espera hasta que el ícono de la ballena en la barra de tareas 
   esté quieto (no animado) — eso significa que Docker está listo
3. No cierres Docker Desktop mientras trabajas

---

### Paso 4 - Levantar el contenedor
1. Vuelve a la terminal de VS Code que abriste en el Paso 1
2. Asegúrate de estar dentro de la carpeta del proyecto  
   (la terminal debe mostrar algo como `parcial1-pyspark-KevinG47>`)
3. Escribe este comando y presiona Enter:
```bash
docker-compose up
```
4. La **primera vez** puede tardar entre 5 y 15 minutos porque 
   descarga todo lo necesario. Es completamente normal, hay que esperar.
5. Sabrás que está listo cuando veas un mensaje así en la terminal:
```
http://127.0.0.1:8888/lab?token=...
```

---

### Paso 5 - Abrir JupyterLab en el navegador
1. En la terminal busca la línea que dice:  
   `http://127.0.0.1:8888/lab?token=...`
2. Copia esa línea completa (incluyendo el token)
3. Abre tu navegador (Chrome, Firefox, Edge)
4. Pega la URL en la barra de direcciones y presiona Enter
5. Se abrirá JupyterLab — una interfaz parecida a un bloc de notas 
   pero para código

---

### Paso 6 - Abrir y ejecutar el notebook
1. En el panel izquierdo de JupyterLab verás una carpeta llamada `work`
2. Haz doble clic en `work`
3. Luego doble clic en `notebooks`
4. Haz doble clic en el archivo `analisis_exploratorio.ipynb`
5. Para ejecutar todo el análisis ve al menú superior:  
   **Kernel** → **Restart Kernel and Run All Cells**
6. Confirma haciendo clic en **Restart** cuando te lo pida
7. Espera unos minutos mientras corre todo el análisis

---

### Para detener el proyecto cuando termines
1. Vuelve a la terminal de VS Code
2. Presiona `Ctrl + C` para detener el contenedor
3. Luego ejecuta:
```bash
docker-compose down
```
Esto apaga el contenedor correctamente y libera recursos de tu computador.

---

## Informe
El informe completo del análisis está disponible en:
`docs/Informe_COVID19_Colombia_KevinChaparro.pdf`


### Problemas frecuentes

**Docker no arranca:**  
Asegúrate de que Docker Desktop esté abierto y corriendo antes de 
ejecutar `docker-compose up`

**La URL no abre en el navegador:**  
Copia la URL completa desde la terminal, incluyendo el token 
(la parte que dice `?token=...`)

**El dataset no carga:**  
Verifica que el archivo se llame exactamente `dataset.csv` y esté 
dentro de la carpeta `data/`


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
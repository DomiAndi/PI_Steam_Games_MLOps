# 🎮 Machine Learning - Modelo de Recomendación de Juegos en Steam

Proyecto MLOps - SteamGames


## 📝 Descripción del Proyecto
Este proyecto simula el trabajo de un ingeniero MLOps, que fusiona habilidades de ingeniería de datos y ciencia de datos, en el contexto de la plataforma de juegos Steam. 
El objetivo es crear un Producto Mínimo Viable (MVP) que incluya una API desplegada y un modelo de Machine Learning para realizar consultas útiles sobre la plataforma. 
También se implementará un sistema de recomendación basado en la similitud de los juegos.

## 📊 Datos

El proyecto se basa en tres archivos comprimidos en formato JSON (GZIP):

output_steam_games.json: Contiene datos sobre los juegos, como nombres, editores, desarrolladores, precios y etiquetas.
australian_users_items.json: Ofrece información sobre cómo los usuarios interactúan con los juegos, incluyendo el tiempo de juego.
australian_users_reviews.json: Contiene comentarios y reseñas de usuarios sobre los juegos, así como recomendaciones y otros detalles como URLs e IDs de usuario.

## 🛠️ Tareas Realizadas

### ETL (Extracción, Transformación y Carga)

En esta fase del proyecto, se llevaron a cabo las siguientes actividades utilizando los Notebooks ETL_steam_games, ETL_user_reviews y ETL_user_items:

1. Extracción de datos desde los archivos JSON iniciales para familiarizarse con ellos y comenzar la limpieza de datos.
2. Limpieza de los datos para eliminar información innecesaria y asegurar una comprensión adecuada.
3. Conversión de los datos a formato Parquet para su uso posterior.

### Feature Engineering
En esta etapa del proyecto, analizamos los sentimientos de los comentarios utilizando la librería TextBlob, que forma parte de una biblioteca de procesamiento de lenguaje natural (NLP). 
Esta librería evalúa la polaridad del sentimiento de un comentario y lo clasifica como negativo, neutral o positivo.

Además de esta metodología, preparamos los conjuntos de datos necesarios para procesar cada función específica, 
lo que optimiza y mejora los tiempos de funcionamiento del servicio en la nube para implementar la API y resolver consultas (Funciones_API.ipynb).

### Análisis Exploratorio de Datos (EDA)

Se llevó a cabo un análisis exploratorio de los tres conjuntos de datos después del proceso ETL. 
Esto permitió visualizar las variables categóricas y numéricas, identificando las que son esenciales para el modelo de recomendación final del Machine Learning.

### Modelado (Desarrollo de Modelos de Machine Learning)
En este proyecto, utilizando el conjunto de datos steam_games, creamos una función llamada recommend_games para sugerir juegos similares basados en su género. 
Esta función utiliza un modelo de recomendación de elemento-elemento, que se ejecuta con la técnica de similitud del coseno. 
Esta técnica es comúnmente utilizada para comparar la similitud entre documentos, palabras o cualquier cosa representada como vectores en un espacio multidimensional.

#### Desarrollo de API

Se creó una API utilizando el framework FastAPI, que ofrece las siguientes funciones:

* *userdata*: Proporciona información sobre el gasto de un usuario, su porcentaje de recomendaciones y la cantidad de elementos que consume.
* *userforgenre*: Identifica al usuario que acumula más horas jugadas para el género dado y otorga una lista de la acumulación de horas jugadas por año de lanzamiento.
* *developer*: Ofrece detalles sobre el contenido desarrollado por una empresa y su porcentaje de contenido gratuito por año.
* *best_developer_year*: Devuelve el top 3 de desarrolladores con juegos más recomendados por usuarios para el año dado.
* *sentiment_analysis*: Según el desarrollador, devuelve un diccionario con el nombre del desarrollador como llave y una lista con la cantidad total de registros de reseñas de usuarios que se encuentren categorizados con un análisis de sentimiento como valor positivo o negativo.
* *recommend_games*: Recomienda 5 juegos similares a uno ingresado.

### FastAPI

El código para la generación de la API se encuentra en el archivo `Main`. Para ejecutar la API localmente, siga estos pasos:

1. Clonar el proyecto con `git clone https://github.com/sebastianr92/PI_MLOps_SteamGames.git`
2. Levantar un entorno virtual con `python -m venv env`.
3. Activar el entorno virtual con `env\Scripts\activate`.
4. Instalar las dependencias con `pip install -r requirements.txt`.
5. Ejecutar el archivo `main.py` usando Uvicorn con `uvicorn main:app --reload`.
6. Acceder a la documentación de la API en su navegador usando la dirección `http://XXX.X.X.X:XXXX/docs`.
7. Utilizar las funciones proporcionadas.

### Deploy

El despliegue de la API se realizó en la plataforma Render. 
Se generó un servicio en Render conectado a este repositorio y se puede acceder a la API

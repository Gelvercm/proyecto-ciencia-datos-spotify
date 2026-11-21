# ¿Qué hace popular a una canción? Análisis de datos de Spotify

Proyecto final del curso de Ciencia de Datos.

## Integrantes
- Miguel Ángel Malagón Villarreal
- Gelver Cifuentes Mendoza
- Nicoll Oyola

## Video de presentación
(Aquí va el enlace al video de 2 a 5 minutos, o se indica que está en la carpeta `video/`.)

## Descripción del proyecto
En este proyecto trabajamos con un conjunto de datos públicos de cerca de 33 mil canciones de Spotify ([TidyTuesday, enero de 2020](https://github.com/rfordatascience/tidytuesday/tree/master/data/2020/2020-01-21)). Los datos incluyen características de audio (danceability, energy, valence, tempo, etc.), la popularidad de cada canción y su género.

La pregunta que guía el trabajo es: **¿qué características de audio se relacionan con la popularidad de una canción y cómo varían según el género?**

El proyecto se desarrolla en tres etapas, una por cada módulo del curso.

## Estructura del repositorio
```
├── README.md
├── datos/            datos originales y datos limpios (.csv)
├── notebook/         cuaderno de Google Colab (.ipynb)
├── presentacion/     presentación de apoyo (.pptx) e imágenes
└── video/            video de presentación o enlace
```

## Avance por etapas
| Etapa | Módulo | Estado |
|---|---|---|
| 1 | Fundamentos y preparación de datos | Terminada |
| 2 | Etapa 2: Análisis Exploratorio de Datos (EDA) | Terminado |
| 3 | Etapa 3: Modelado Matemático, Storytelling y Conclusiones | Terminado |

### Etapa 1: Fundamentos y preparación de datos
Seleccionamos el dataset, exploramos sus variables y distribuciones, y lo limpiamos. Pasó de 32 833 filas y 23 columnas a 28 352 filas y 24 columnas. Estos fueron los principales problemas y lo que hicimos:

- **Nulos:** 5 filas sin nombre, artista ni álbum. Las eliminamos.
- **Duplicados:** una misma canción aparecía en varias playlists. Dejamos un registro por `track_id`.
- **Fechas:** había tres formatos distintos. Las pasamos a tipo fecha y creamos la columna `anio`.
- **Tipos de datos:** `key` y `mode` eran números; los convertimos a notas musicales y modo (mayor/menor). El género quedó como categoría.
- **Valores no válidos:** `tempo = 0` lo dejamos como nulo y la duración la pasamos a minutos.

### Etapa 2: Análisis Exploratorio de Datos (EDA)
Exploramos las distribuciones, correlaciones y diferencias por género y época sobre las 28 352 canciones limpias para entender qué patrones se relacionan con `track_popularity`. Estos fueron los principales hallazgos:

- **Distribución de popularidad:** media de `39.34` y mediana de `42.0` (rango `0` a `100`); el `9.23%` de las canciones (`2 616`) tiene popularidad `0`.
- **Correlaciones con el audio:** relaciones lineales suaves; destacan en negativo `instrumentalness` ($\rho = -0.166$), `duracion_min` ($\rho = -0.121$) y `energy` ($\rho = -0.110$), y en positivo `anio` ($\rho = +0.150$) y `acousticness` ($\rho = +0.125$).
- **Géneros y décadas:** `pop` (`43.50`) y `latin` (`42.62`) lideran en popularidad promedio, mientras `edm` registra la más baja (`32.01`). El catálogo se concentra en la década de `2010` (`19 830` canciones).

### Etapa 3: Modelado Matemático, Storytelling y Conclusiones
Entrenamos modelos supervisados (partición `80%` entrenamiento / `20%` prueba con `Pipeline` sin fuga de datos) usando 12 variables numéricas y 4 categóricas para evaluar tanto la predicción de puntaje continuo como la detección de canciones de alta popularidad (`track_popularity >= 60`):

- **Regresión (puntaje `0–100`):** el modelo lineal base (**Regresión Ridge**) obtuvo $\text{MAE} = 18.08$, $\text{RMSE} = 21.83$ y $R^2 = 0.140$, mientras que **Gradient Boosting** mejoró a $\text{MAE} = 17.18$, $\text{RMSE} = 20.76$ y $R^2 = 0.222$, evidenciando interacciones no lineales.
- **Clasificación (*Hit* $\ge 60$, top `22.63%`):** **Gradient Boosting** alcanzó un $\text{ROC-AUC} = 0.772$ y $\text{Accuracy} = 78.35\%$, y **Random Forest Balanceado** logró el mejor equilibrio detección/precisión ($\text{F1} = 0.501$, $\text{Recall} = 65.11\%$).
- **Variables más influyentes:** año de lanzamiento (`24.33%`), baja instrumentalidad (`9.68%`), subgénero/género, volumen (`loudness`, `5.24%`) y duración acotada (`4.15%`).
  
- **Conclusión y efectividad del modelo:** el modelo es moderadamente efectivo para detectar patrones generales y hacer un filtrado inicial (*pre-screening*), pero no basta por sí solo para predecir el éxito exacto, ya que las características acústicas explican ~`22%` de la variabilidad y el ~`78%` restante depende de factores externos (marketing, redes sociales, base de fans y playlists).

El detalle con el código está en el notebook.

## Cómo reproducir el análisis
[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/miguelmalgon-sys/proyecto-ciencia-datos-spotify/blob/main/notebook/proyecto_ciencia_datos.ipynb)

## Cómo reproducir el análisis
[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/Gelvercm/proyecto-ciencia-datos-spotify/blob/main/notebook/proyecto_ciencia_datos.ipynb)


Abrir `notebook/proyecto_ciencia_datos.ipynb` en [Google Colab](https://colab.research.google.com/) y ejecutar las celdas en orden. Si el repositorio no está clonado, el notebook descarga los datos directamente desde la fuente original.

# Proyecto de Ciencia de Datos: ¿Qué hace popular a una canción?

Proyecto final del curso de Ciencia de Datos (3 etapas, una por módulo).

## Integrantes
- _Nombre 1_ — _usuario GitHub_
- _Nombre 2_ — _usuario GitHub_
- _Nombre 3 (opcional)_

## 🎥 Video de presentación
_(Pegar aquí el enlace público al video de 2 a 5 minutos, o ubicarlo en `video/`)_

## Contexto
Dataset público de ~33 mil canciones de Spotify ([TidyTuesday 2020-01-21](https://github.com/rfordatascience/tidytuesday/tree/master/data/2020/2020-01-21)) con atributos de audio, popularidad y género. Pregunta guía: *¿qué características de audio se asocian con la popularidad y cómo varían por género?*

## Estructura
```
├── README.md
├── datos/          spotify_songs_raw.csv (original) · spotify_songs_limpio.csv (depurado)
├── notebook/       proyecto_ciencia_datos.ipynb (abrir en Google Colab)
├── presentacion/   presentacion_proyecto.pptx (Etapa 1 lista; añadir Etapas 2 y 3) + img/
└── video/          video o enlace
```

## Etapas
| Etapa | Módulo | Estado |
|---|---|---|
| 1 | Fundamentos y preparación de datos: selección, exploración, limpieza | ✅ Completa (Miguel) |
| 2 | _(según Módulo 2)_ | ⏳ A cargo de los compañeros |
| 3 | _(según Módulo 3)_ | ⏳ A cargo de los compañeros |

### Etapa 1 — Resumen de limpieza
32 833 filas × 23 columnas → 28 352 filas × 24 columnas tras la limpieza (detalle en el notebook).
- 5 filas con nulos en nombre/artista/álbum → eliminadas.
- `track_id` repetidos (misma canción en varias playlists) → 1 registro por canción.
- Fechas en 3 formatos → unificadas a `datetime` + columna `anio`.
- `key`/`mode` numéricos → notas y modo (mayor/menor); géneros como `category`.
- `tempo = 0` inválido → nulo; duración a minutos.

## Cómo ejecutar
Abrir `notebook/proyecto_ciencia_datos.ipynb` en [Google Colab](https://colab.research.google.com/) (si no se clona el repo, el notebook descarga los datos desde la URL original).

# Gremio de Aventureros

Aplicación web en PHP para digitalizar el tablón de misiones del Gremio de Aventureros de Villa Roble. Reto evaluable de 0613 DWES (2.º DAW).

## Estado

| Parte | Contenido | Estado |
|---|---|---|
| Parte 1 · El tablón | Funciones de presentación con `match` y tablón de misiones con `foreach` | Hecha |
| Parte 2 · Filtros y zurrón | Filtros por GET, aceptar y abandonar misiones por POST, zurrón | Pendiente |
| Parte 3 · Miembros del gremio | Login, sesión y cookies | Pendiente (Entrega 2) |

## Qué hay hecho en la Parte 1

- `src/inc/funciones.php`
  - `etiquetaRango()`: devuelve el nombre del rango (E Novato, D Aprendiz, C Veterano, B Experto, A Élite, S Leyenda) con `match`.
  - `claseRango()`: devuelve la clase CSS según la dificultad con `match` de varios valores por brazo (E y D `facil`, C y B `media`, A y S `dificil`).
  - `formatearOro()`: formatea las monedas con `number_format` (5000 → 5.000 mo).
- `src/tablon.php`: recorre las misiones con `foreach` y pinta una tarjeta por misión con el rango, el título, la zona, los días (en singular o plural), la descripción y la recompensa. Todo el texto que sale de los datos pasa por `e()`.

## Estructura

```
gremio/
├── MEMORIA.md
├── sql/gremio.sql
└── src/
    ├── css/estilo.css
    ├── inc/
    │   ├── cabecera.php
    │   ├── conexion.php
    │   ├── datos_misiones.php
    │   ├── funciones.php
    │   ├── pie.php
    │   └── sesion.php
    ├── index.php
    ├── login.php
    ├── logout.php
    ├── preferencias.php
    ├── tablon.php
    └── zurron.php
```

## Cómo probarlo

1. Copiar la carpeta `gremio/` dentro de la carpeta que sirve el contenedor web (en mi entorno, `src/`).
2. Levantar los contenedores con `docker compose up -d`.
3. Abrir `http://localhost:8080/gremio/src/tablon.php`.

Tienen que salir las 10 misiones, cada una con el borde verde, naranja o rojo según su rango.

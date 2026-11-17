# Gremio de Aventureros

Tablón de misiones del Gremio de Aventureros de Villa Roble hecho en PHP. Muestra las misiones del gremio en tarjetas, cada una con su rango, la zona, los días que dura, la descripción y la recompensa en monedas de oro.

El borde de cada tarjeta cambia de color según la dificultad:

- **Verde:** rangos E (Novato) y D (Aprendiz)
- **Naranja:** rangos C (Veterano) y B (Experto)
- **Rojo:** rangos A (Élite) y S (Leyenda)

## Tecnologías

- PHP 8.3 con ***declare(strict_types=1)***
- Docker con Nginx, PHP-FPM y MySQL
- HTML y CSS

## Cómo ejecutarlo

1. Copiar la carpeta ***gremio*** dentro de la carpeta que sirve el contenedor web.
2. Levantar los contenedores con ***docker compose up -d***.
3. Abrir ***http://localhost:8080/gremio/src/tablon.php***.

## Archivos principales

- ***src/inc/funciones.php***: funciones para mostrar el nombre del rango, la clase de color y el formato del oro.
- ***src/tablon.php***: página del tablón que recorre las misiones y pinta una tarjeta por cada una.
- ***src/inc/datos_misiones.php***: array con las 10 misiones.
- ***MEMORIA.md***: explicación de lo que he hecho, pruebas y dificultades.

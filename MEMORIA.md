# Memoria · Gremio de Aventureros

**Alumno:** Adrián Hermida Moreno

## 1. Parte 1 · El tablón

En esta parte he completado las funciones de presentación de ***inc/funciones.php*** y he hecho que ***tablon.php*** pinte todas las misiones del array.

### etiquetaRango()

Devuelve el nombre de cada rango usando ***match***: E es Novato, D Aprendiz, C Veterano, B Experto, A Élite y S Leyenda.

He puesto ***default => 'Desconocido'***. Si no lo pongo y llega un rango que no está en ningún brazo, por ejemplo ***'Z'***, ***match*** lanza un ***UnhandledMatchError*** y la página se para con un error fatal. Con el ***default*** la función siempre devuelve algo y el tablón sigue funcionando aunque llegue un dato raro.

Lo prefiero así porque ahora las misiones vienen de un array que controlamos nosotros, pero más adelante vendrán de la base de datos y no puedo asegurar que el rango siempre sea correcto. Es mejor que en una tarjeta salga "Desconocido" que romper la página entera.

### claseRango()

Devuelve la clase CSS que pinta el borde de la tarjeta. Aquí he usado ***match*** con varios valores en el mismo brazo:

- ***'E', 'D' => 'facil'*** (borde verde)
- ***'C', 'B' => 'media'*** (borde naranja)
- ***'A', 'S' => 'dificil'*** (borde rojo)

También tiene ***default => ''***, así que si llega un rango raro la tarjeta sale sin color pero no da error.

Una diferencia con ***switch*** que he visto es que ***match*** compara con ***===***, así que una ***'b'*** en minúscula no entraría en el brazo de la ***'B'***.

### formatearOro()

Uso ***number_format($oro, 0, ',', '.')*** y le añado ***' mo'*** al final. El 0 es para que no saque decimales, la coma es el separador decimal y el punto el de miles, que es como se escribe en España. Así 5000 sale como "5.000 mo" y 1200 como "1.200 mo".

### Tablón con foreach

En ***tablon.php*** recorro ***$visibles*** con ***foreach*** y por cada misión pinto un ***article*** con:

- la clase ***mision*** más la que devuelve ***claseRango()***, que es la que da el color del borde
- el rango y su nombre con ***etiquetaRango()***
- el título, la zona y la descripción
- los días, con el singular bien puesto: ***$mision['dias'] === 1 ? 'día' : 'días'***
- la recompensa con ***formatearOro()***

Todo el texto que sale del array pasa por ***e()***, que usa ***htmlspecialchars***. Así, si algún dato tuviera etiquetas HTML, se mostrarían como texto y no se ejecutarían.

Si el filtro deja la lista vacía, se muestra "Ninguna misión cumple el filtro.".

## 2. Pruebas que he hecho

| Prueba | Resultado esperado | Resultado obtenido |
|---|---|---|
| Abrir tablon.php | 10 tarjetas con borde de color según el rango | Salen las 10: 4 verdes (E/D), 4 naranjas (C/B) y 2 rojas (A/S) |
| Misiones de 1 día | Sale "1 día" en singular | Ratas en la bodega, Hierbas de luna y Cartas perdidas salen con "1 día" |
| Formato del oro | 5000 → 5.000 mo | El dragón de Obsidiana sale con 5.000 mo y Huevo de grifo con 1.200 mo |
| tablon.php?rango=Z&oro=hola | La página no da errores | Salen las 10 misiones sin avisos |

## 3. Dificultades y cómo las he resuelto

- **Singular y plural de los días:** al principio todas las misiones salían con "días", también las de 1. Lo arreglé con un operador ternario.
- **Formato del oro:** con ***number_format($oro)*** sin más parámetros salía "5,000", con coma, que es el formato inglés. Tuve que pasarle el separador decimal y el de miles.
- **El default del match:** sin ***default***, si probaba a cambiar un rango a mano en el array por una letra que no existe, la página daba un error fatal. Con el ***default*** se soluciona.

## 4. Conocimientos adquiridos

- ***match*** devuelve un valor y se puede asignar o devolver directamente, cosa que ***switch*** no hace.
- ***match*** compara de forma estricta (***===***) y no necesita ***break***.
- En un mismo brazo de ***match*** se pueden poner varios valores separados por comas.
- Si ningún brazo coincide y no hay ***default***, ***match*** lanza ***UnhandledMatchError***.
- ***number_format()*** recibe el número, los decimales, el separador decimal y el separador de miles.
- ***foreach ($array as $elemento)*** recorre un array sin preocuparse de los índices.
- Con la sintaxis alternativa (***foreach (...):*** y ***endforeach;***) el PHP mezclado con HTML se lee mucho mejor.
- Todo dato que se pinta en HTML hay que escaparlo con ***htmlspecialchars*** para evitar XSS.

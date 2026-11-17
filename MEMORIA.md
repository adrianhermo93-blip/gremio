# Memoria · Gremio de Aventureros

**Alumno:** Adrián Hermida Moreno

## 1. Mi aventurero
- Usuario que he añadido a la tabla: ______
- Comando o pasos que he usado para generar el hash:

## 2. Parte 1 · match
¿Has puesto `default` en `etiquetaRango()`? ¿Qué pasa si llega el rango `'Z'`? ¿Por qué lo prefieres así?

Sí, he puesto `default => 'Desconocido'`. Si no lo pongo y llega un rango que no está en los brazos, por ejemplo `'Z'`, `match` lanza un `UnhandledMatchError` y la página se para con un error fatal. Con el `default` la función siempre devuelve un texto y la página sigue funcionando aunque llegue un dato raro.

Lo prefiero así porque las misiones ahora vienen de un array, pero en la UD9 vendrán de la base de datos y no puedo estar seguro al 100% de que el rango siempre sea correcto. Es mejor que salga "Desconocido" en una tarjeta que romper el tablón entero. En `claseRango()` he hecho lo mismo con `default => ''`, así esa tarjeta sale sin color pero no da error.

Otra cosa que he visto es que `match` compara con `===`, a diferencia de `switch`, así que `'b'` en minúscula no entraría en el brazo `'B'`.

## 3. Parte 2 · Validación de la URL
Escribe a mano en la barra `tablon.php?rango=Z&oro=hola`. ¿Qué ocurre y qué línea de tu código lo evita?

## 4. Parte 3 · Sesión frente a cookie
Explica con tus palabras qué guardas en `$_SESSION` y qué guardas en cookies, y por qué no al revés.

## 5. Parte 3 · Seguridad del login
- ¿Qué pasa si en el usuario escribes `' OR '1'='1`? ¿Por qué?
- ¿Para qué sirve `session_regenerate_id(true)`?
- ¿Por qué el mensaje de error es el mismo si falla el usuario o la contraseña?

## 6. Pruebas que he hecho
| Prueba | Resultado esperado | Resultado obtenido |
|---|---|---|
| Entrar en tablon.php sin login | | |
| Login con contraseña mala | | |
| Aceptar la misma misión dos veces | | |
| Cerrar sesión y volver al zurrón | | |
| Cambiar el tema y cerrar sesión | | |

## 7. Dificultades y cómo las he resuelto

# Mi Jardín

Catálogo de cuidado de mi colección de plantas de interior, en Coyoacán, Ciudad
de México. Se consulta desde el celular, a la hora de regar.

**https://jorgeliber28.github.io/mi-jardin/**

## Qué es

Un solo archivo, `index.html`, sin dependencias, sin build y sin instalación.
Se abre en cualquier navegador y funciona sin conexión salvo por las fotografías.

## Qué contiene

26 ejemplares repartidos en cinco zonas según la luz que reciben y cada cuándo
se riegan, más una pestaña **Recientes** con la colección entera en orden de
llegada.

Cada ficha muestra de entrada el nombre común, el binomio, el rincón donde está
y los tres datos que se consultan con la regadera en la mano: riego, luz y
manejo. Al abrirla aparecen sustrato, humedad, temperatura, poda, reproducción,
nivel de exigencia, problemas comunes, cuidado especial y la procedencia del
ejemplar.

Las especies tóxicas llevan marca visible. La clasificación se verifica contra
la base de plantas tóxicas y no tóxicas de la ASPCA; cuando una especie no
figura ahí, la ficha lo dice en lugar de suponerlo.

| Zona | Luz | Riego |
|---|---|---|
| 1 | Baja | 5–7 días |
| 2 | Media | 5–7 días |
| 3 | Media a alta | 7–10 días |
| 4 | Baja a media | 10–14 días |
| 5 | Alta | 10–14 días |

## Las láminas

Cada especie tiene su ilustración vectorial dibujada dentro del archivo: no
depende de internet ni de URLs que caduquen. Cuando el ejemplar tiene fotografía
propia, la fotografía sustituye a la lámina.

Al tocar la lámina se abren fotografías de referencia. El archivo consulta la
Action API de Wikipedia (`/w/api.php` con `origin=*`) agrupando las variantes
del nombre en una sola petición por wiki, primero en inglés y luego en español,
y recurre a búsqueda si el título directo no devuelve imagen. Si todo falla, se
queda la lámina dibujada. Para diagnosticar qué especie encontró fotografía,
abrir la consola del navegador y escribir `diagFotos()`.

## Diseño

Pliego de herbario: papel, tinta y un solo acento verde, con el carmín reservado
a las advertencias. Tipografías EB Garamond para los nombres, Archivo para el
cuerpo y Courier Prime para las etiquetas. Tema claro y oscuro. La iconografía
es de trazo, dibujada en el archivo.

## Mantenimiento

El repositorio guarda los archivos con saltos de línea LF. Los cambios se
confirman y publican desde GitHub Desktop, nunca por la interfaz web de GitHub:
mezclar las dos cosas ya produjo una vez dos historias paralelas.

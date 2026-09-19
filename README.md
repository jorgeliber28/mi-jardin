# Mi Jardín

Inventario de las plantas de interior de la casa, en Coyoacán, Ciudad de México.
Se consulta desde el celular, a la hora de regar.

**https://jorgeliber28.github.io/mi-jardin/**

## Qué es

Un solo archivo, `index.html`, sin dependencias, sin build y sin instalación.
Se abre en cualquier navegador y funciona sin conexión salvo por las
fotografías y las tipografías.

## El modelo

El sistema distingue dos cosas que antes iban revueltas:

- **Especie** — lo que es cierto de la planta: luz, riego, cuánta agua,
  sustrato, humedad, temperatura, poda, reproducción, exigencia, problemas
  comunes, cuidados especiales y toxicidad.
- **Ejemplar** — lo que es cierto de *esta* planta: fecha de llegada a casa,
  dónde se compró, en qué rincón está, su fotografía y sus notas.

Dos ejemplares de la misma especie comparten una sola ficha de cuidados y
conservan cada uno su fecha y su procedencia. Corregir un cuidado se hace en
un solo lugar.

## Los grupos

Las plantas se agrupan por la luz que necesitan, que es la decisión que manda
al elegir dónde ponerlas. La pestaña **Recientes** muestra la colección
completa en orden de llegada.

| Grupo | Qué significa |
|---|---|
| Muy poca luz | Rincones sin ventana cerca |
| Luz baja | Lejos de la ventana o con ella tapada |
| Luz media | Ventana norte o este, o detrás de cortina |
| Luz brillante | Junto a la ventana, sin sol encima |
| Sol directo | Ventana sur u oeste, con horas de sol sobre la hoja |

## Toxicidad

Cada especie lleva uno de tres valores, y la ficha dice contra qué se
verificó: **tóxica**, **no tóxica** o **sin dato**.

El tercero no es relleno. *Pachypodium lamerei*, *Cotyledon pendens* y
*Pilea peperomioides* no aparecen en la base de la ASPCA, y sin ese valor el
sistema obligaría a mentir en una de las dos direcciones. Cuando la ASPCA
clasifica otra especie del mismo género, la ficha lo dice con ese nombre.

## Las láminas

Cada especie tiene su ilustración vectorial dibujada dentro del archivo: no
depende de internet ni de URLs que caduquen. Cuando el ejemplar tiene
fotografía propia, la fotografía sustituye a la lámina.

Al tocar la lámina se abren fotografías de referencia. El archivo consulta la
Action API de Wikipedia (`/w/api.php` con `origin=*`, porque la API REST
ignora ese parámetro y falla por CORS), agrupando las variantes del nombre en
una sola petición por wiki, primero en inglés y luego en español, con búsqueda
como último recurso. Si todo falla, se queda la lámina dibujada.

Para diagnosticar qué especie encontró fotografía, abrir la consola del
navegador y escribir `diagFotos()`.

## Mantenimiento

El repositorio guarda los archivos con saltos de línea **LF**. Los cambios se
confirman y publican desde GitHub Desktop, nunca por la interfaz web de
GitHub: mezclar las dos cosas ya produjo una vez dos historias paralelas.

`ARQUITECTURA.md` explica dónde vive cada cosa dentro del archivo y qué tocar
para cambiar cada cosa.

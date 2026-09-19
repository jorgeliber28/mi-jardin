# Arquitectura de Mi Jardín

Este documento existe para que nadie —ni tú dentro de seis meses, ni quien te
ayude— tenga que leer 1,300 líneas para saber dónde tocar. Si cambias la
estructura del archivo, actualiza también este mapa.

## El archivo

`index.html` es todo el sistema: marcado, estilo y lógica en un archivo, sin
dependencias, sin build y sin servidor. Lo único que pide a internet son las
tipografías de Google Fonts y las fotografías de Wikipedia; sin ninguna de las
dos, el sitio sigue funcionando.

Tres secciones en este orden: `<style>`, el marcado del `<body>`, y un
`<script>` envuelto en una función anónima para no dejar nada en el ámbito
global salvo `diagFotos()`.

## Dónde vive cada cosa

| Quieres cambiar… | Está en |
|---|---|
| Colores, tipografías, tamaños, medidas | `1. TOKENS`, bloque `:root` |
| El tema oscuro | El mismo bloque, en `@media (prefers-color-scheme: dark)` |
| Cómo se ve la ficha | `4.3 Ficha` |
| La marca de tóxica / no tóxica | `4.4 Marca de toxicidad` |
| Los tres datos del vistazo | `4.5 Vistazo` |
| Qué plantas hay y sus cuidados | `DATOS`, la constante `DATOS` |
| Los grupos de luz y sus descripciones | `DATOS`, la constante `LUZ` |
| Qué campos salen en la ficha y en qué orden | `PINTADO`, función `fichaHTML` |
| Cómo se redacta la toxicidad | `PINTADO`, función `campoToxicidad` |
| Los iconos | `ICONOGRAFÍA`, objeto `ICONOS` |
| Las ilustraciones de cada especie | `LÁMINAS VECTORIALES` |
| Cómo se buscan las fotografías | `FOTOS REALES` |
| Pestañas, orden y búsqueda | `ESTADO` |

## El modelo de datos

```
DATOS = {
  especies:   { "clave-de-especie": { …cuidados… }, … },
  ejemplares: [ { clave, n, fechaIngreso, aprox, procedencia, rincon, foto, notas }, … ]
}
```

La **clave de especie** se deriva del binomio en minúsculas y sin acentos:
`Alocasia longiloba` → `alocasia-longiloba`. Es lo que liga las dos tablas.

El **número de acceso** (`n`) identifica al ejemplar y es estable: no es su
orden de lectura, y no se reordena aunque cambie de grupo.

`aprox: true` marca una fecha estimada. Se muestra al mes —"hacia agosto de
2026"— en vez de fingir un día exacto; el ordenamiento sí usa la fecha
completa.

### Catálogos

Valores cerrados. Cambiar uno obliga a revisar los tres lugares donde se usa:
el dato, la constante que lo traduce y el estilo que lo pinta.

- **luz**: `muy-baja` · `baja` · `media` · `brillante` · `sol-directo`
- **manejo**: `facil` · `medio` · `medio-alto` · `alto`
- **toxicidad**: `toxica` · `no-toxica` · `sin-dato`

## Cómo se da de alta una planta

1. Si la especie es nueva, agregar una entrada a `DATOS.especies` con su clave.
2. Agregar su lámina: una entrada `svg` en la especie y, si ninguna forma
   existente le queda, una función `dibujoX` en `LÁMINAS VECTORIALES`
   registrada en el objeto `DIBUJOS`.
3. Agregar el ejemplar a `DATOS.ejemplares` con el siguiente número de acceso.
4. Verificar la toxicidad contra la ASPCA **antes** de escribirla. Si la
   especie no figura, el valor es `sin-dato` y la nota lo explica.
5. Actualizar el conteo en `<meta name="description">`.

La skill `alta-planta-mi-jardin` automatiza este procedimiento.

## Reglas del archivo que no se rompen

- **El CSS va en bloques y en orden**: tokens, base, estructura, componentes,
  estados, utilidades, consultas de medios. Una regla nueva va en su bloque,
  **nunca al final del archivo**. Añadir al final es lo que encima el código.
- **Ningún color, tamaño ni tipografía fuera de `:root`**, con una excepción
  deliberada y comentada: la lámina y su lupa, cuyo fondo es papel en los dos
  temas porque las caladuras de la monstera se recortan con ese tono.
- **Ningún `!important`** salvo el bloque de `prefers-reduced-motion`.
- **Cero emojis.** La iconografía son SVG de trazo dibujados en el archivo.
- **Saltos de línea LF.** El repositorio los usa; en CRLF el diff sale de
  archivo completo y es imposible de revisar.
- **El push lo hace Liber desde GitHub Desktop**, nunca por la web de GitHub.

## Qué revisar y cada cuándo

| Cuándo | Qué |
|---|---|
| Tras agregar o editar una planta | Sintaxis, conteo por grupo, y que la ficha abra sin error en consola |
| Tras cambiar la paleta | Contraste de cada tono sobre cada fondo real, en los dos temas |
| Tras cambiar estilos | Selectores repetidos, clases sin uso, colores fuera de `:root` |
| Al cerrar un bloque | Código sin uso, y que ningún texto o comentario diga algo que ya no es cierto |
| Cada tanto | `diagFotos()` en la consola, para ver qué especie dejó de encontrar fotografía |

## Registro de decisiones

**19 de septiembre de 2026 — Se separa especie de ejemplar.**
Antes cada renglón era a la vez especie y ejemplar. Eso repetía los cuidados
entre cultivares —tres Potos, dos Rhipsalis— y hacía imposible registrar dos
ejemplares de la misma especie con fechas distintas. Se sacrifica algo de
simplicidad al leer el archivo a cambio de una sola fuente de verdad.

**19 de septiembre de 2026 — La toxicidad pasa a tres valores.**
Antes se deducía del texto libre con una expresión regular, y ocho especies no
decían nada, lo que se leía igual que "no es tóxica". Ahora es un campo
explícito con su fundamento citado. Se verificaron las 26 contra la ASPCA.

**19 de septiembre de 2026 — Se agrega "cuánta agua".**
La frecuencia en días no dice cuánta agua. El campo da volumen en referencia
al tamaño de maceta, que es como se riega de verdad.

**19 de septiembre de 2026 — Los grupos pasan a ser el catálogo de luz.**
Antes eran cinco zonas con nombres mixtos de luz y riego. Ahora el grupo es
únicamente el nivel de luz, que es la decisión que manda al elegir sitio.

**19 de septiembre de 2026 — Las fechas de las 24 plantas heredadas son estimadas.**
No había registro real. Se fijaron en agosto de 2026 y se marcaron con
`aprox`, que las muestra al mes. Se reemplazan por fechas reales conforme
aparezcan.

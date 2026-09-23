# AGENTS.md

Instrucciones de trabajo para agentes de IA que operen sobre este repositorio.

---

## Índice

1. [Qué es este proyecto](#1-qué-es-este-proyecto)
2. [Stack](#2-stack) — 2.1 [Recomendar sí, modificar no](#21-recomendar-sí-modificar-no)
3. [Qué hace y qué no hace el agente](#3-qué-hace-y-qué-no-hace-el-agente) — 3.1 [Alcance por archivo](#31-alcance-por-archivo)
4. [Las once reglas, en detalle](#4-las-once-reglas-en-detalle)
5. [Plantillas disponibles](#5-plantillas-disponibles)
6. [De bloque a HTML](#6-de-bloque-a-html)
7. [El índice](#7-el-índice)
8. [Vocabulario de CSS](#8-vocabulario-de-css)
9. [Qué actualizar cuando algo cambia](#9-qué-actualizar-cuando-algo-cambia)

---

## 1. Qué es este proyecto

Un reservorio de material de estudio sobre temas técnicos. Cada tema se documenta en
una página HTML autónoma que comparte una hoja de estilos común.

**El contenido no se genera acá.** Llega escrito, en archivos `.txt` dentro de
`contenidos/`. Este proyecto los convierte en HTML usando plantillas.

Eso define el trabajo del agente: **traducir contenido a estructura**. No investigar el
tema, no completar lo que falte, no decidir qué debería decir una ficha.

El contexto completo — para qué existe, cómo está organizado, qué formatos hay — está
en `README.md`. Este archivo asume que ya se leyó.

`FORMATOS.md` es la guía para escribir los `.txt`. No es material de trabajo del
agente: se usa afuera del proyecto, al volcar un tema estudiado. Se lo menciona acá
porque hay cambios que obligan a actualizarlo (punto 9).

---

## 2. Stack

El proyecto es **HTML y CSS**. Nada más.

Sin JavaScript, sin frameworks, sin preprocesadores, sin gestores de paquetes, sin
proceso de compilación, sin dependencias externas en tiempo de ejecución.

Eso es deliberado y sostiene tres cosas: el material se abre con doble clic sin
levantar nada, sigue funcionando dentro de diez años sin pelearse con versiones, y su
fuente se lee sin herramientas.

**Cualquier tecnología nueva se valida antes de incorporarse.** Una librería, un script
de build, un generador estático, JavaScript propio: todo eso se propone y se espera la
decisión del autor. No se agrega como efecto colateral de otra tarea.

Hay dos casos ya previstos — un buscador y un generador de índice — que van a necesitar
JavaScript o Python. Están contemplados, pero se implementan cuando el autor los
defina, no antes.

### 2.1 Recomendar sí, modificar no

El agente **puede y debe** señalar mejoras: una refactorización que convendría, un
componente que se repite, una tarea manual que un script resolvería, una decisión de
diseño que envejeció mal.

Lo que no puede es **aplicarlas sin aviso**. La propuesta puede venir de cualquiera; la
decisión es del autor.

Esto vale para todo el proyecto, no sólo para el stack.

---

## 3. Qué hace y qué no hace el agente

**Hace:** toma un `.txt` de `contenidos/`, lo traduce a HTML usando la plantilla que
corresponde según su `TIPO:`, guarda el resultado en `publicado/`, y agrega la tarjeta
al índice.

**No hace, por iniciativa propia:**

- No investiga el tema ni aporta información propia, aunque la sepa
- No completa un bloque que el `.txt` dejó incompleto
- No escribe la versión de divulgación a partir de la técnica, ni al revés
- No decide qué recortar si el contenido no entra
- No agrega ni modifica componentes de `estilo.css`
- No modifica las plantillas
- No incorpora tecnología nueva
- No edita archivos de `contenidos/`

Todo lo que aparece en una ficha tiene que poder rastrearse a una línea del `.txt`. Si
algo no está ahí, no va.

### 3.1 Alcance por archivo

Ningún archivo está fuera de alcance. Lo que cambia es **cuándo puede tocarlo**: hay
archivos que el agente escribe como parte normal de su trabajo, y otros que sólo
modifica cuando el autor lo pide o lo aprueba.

| Archivo | Cuándo lo modifica |
|---|---|
| `publicado/**/*.html` | Libremente — es su salida |
| `publicado/index.html` | Libremente — agrega la tarjeta del tema nuevo |
| `contenidos/**/*.txt` | Sólo si el autor lo pide explícitamente |
| `plantillas/*.html` | Sólo con aprobación previa |
| `estilo.css` | Sólo con aprobación previa |
| `README.md`, `AGENTS.md`, `FORMATOS.md` | Cuando cambia algo del sistema, avisando qué actualizó |
| `fuentes/` | Sólo si el autor lo pide explícitamente |

Una instrucción directa del autor habilita cualquier cambio: si pide revisar y
reescribir el proyecto entero, eso entra dentro del alcance. Lo que nunca corresponde
es tomar esas decisiones sin que se hayan pedido.

Los `.html` de `publicado/` son **salida regenerable**: se reconstruyen desde el `.txt`
cuantas veces haga falta. Nunca son la fuente de verdad.

---

## 4. Las once reglas, en detalle

Las reglas están enunciadas en `README.md` punto 4. Acá va cómo se aplican al
construir.

### Regla 1 — El `.txt` es el original; el `.html` no se edita a mano

El HTML de `publicado/` se genera completo desde el `.txt`. No se parte de la versión
anterior del HTML para actualizarla.

Si hay que corregir algo de una ficha ya publicada, se corrige el `.txt` y se regenera
el HTML entero. Nunca se edita el HTML directamente, ni siquiera para un error de
tipeo: a partir de ahí el `.txt` y la ficha dejan de coincidir, y la próxima
regeneración pisa la corrección sin avisar.

Si el autor pide editar un `.html` directamente, corresponde señalar esa consecuencia
antes de hacerlo.

### Regla 2 — Un solo `estilo.css`

Al construir se usan los componentes que ya existen. Si un bloque del `.txt` no encaja
con ninguno, se consulta: no se inventa una clase nueva ni se escriben estilos en el
HTML.

Nunca: un `<style>` dentro de un `.html`, ni un atributo `style=` para resolver un caso
particular, ni un segundo archivo `.css` para un formato nuevo. Todo el diseño vive en
un solo archivo.

Cuando se aprueba un componente nuevo, se agrega como sección numerada **al final** de
`estilo.css`, con su comentario. No se intercala entre las existentes ni se modifica
una anterior para que sirva a los dos casos.

El nombre describe la forma, no el tema: `.matriz-comparativa` sí,
`.tabla-de-puertos` no. Un componente bien nombrado se reutiliza en otros temas; uno
nombrado por su primer uso queda atado a él.

### Regla 3 — El contenido lo aporta quien estudió el tema

Todo sale del `.txt`. Si un bloque quedó corto, va corto. Si una definición es
imprecisa, va imprecisa. El agente no mejora, no amplía, no aclara.

**Aunque sepa del tema.** Es el caso más tentador: el agente reconoce que un `.txt`
sobre TCP omitió el `RST` y quiere agregarlo. No corresponde. Puede señalarlo — "el
`.txt` no menciona X, ¿lo agregás?" — pero la ficha se construye con lo que hay.

El motivo: el `.txt` viene de una sesión de estudio con contexto que el agente no
tiene. Lo que parece una omisión puede ser una decisión deliberada de recorte.

Sí corresponde señalar un dato que se contradice con otro dentro del mismo `.txt`, o un
bloque declarado que quedó vacío. Eso es inconsistencia, no recorte.

### Regla 4 — Nunca se inventan datos

Ningún dato se completa de memoria. Fechas, cifras, CVEs, comandos, nombres de firmas,
versiones, puertos: si no está en el `.txt`, no aparece en la ficha.

**El caso peligroso son los datos parciales.** Si el `.txt` dice `CVE-2017-014` — le
falta un dígito — la tentación es corregirlo porque el agente sabe cuál es. No
corresponde: se señala el dato incompleto y se espera respuesta.

Tampoco se completan formatos. Si una fecha dice "14 mar" sin año, va sin año. Si un
comando aparece sin sus flags, va sin flags.

Diferencia con la regla 3: la 3 es sobre no agregar contenido que falta; la 4 es sobre
no rellenar datos que están a medias. La primera es omisión, la segunda es precisión.

Vale para las dos: **un dato falso en material de estudio es peor que un dato ausente.**
Lo ausente se nota y se busca; lo falso se memoriza.

### Regla 5 — Los bloques vacíos se omiten, no se rellenan

Si el `.txt` no trae un bloque, la sección entera se elimina del HTML. No queda un
`<section>` vacío, ni con un título y nada adentro.

Aplica también a las partes opcionales dentro de un bloque. La plantilla trae
`.tres-up`, `.barra`, `.hitos`, `.nota-loop`, `.analogia` y `.aparte`, y todas son
condicionales: si el `.txt` no las alimenta, se borran del HTML.

Los bloques **no se numeran**, ni en la salida ni en las plantillas. La ficha muestra
sólo el título: quien la lee no necesita saber qué posición ocupa en el esqueleto, y una
ficha a la que le falta un bloque mostraría un salto de numeración que parece un error.

### Regla 6 — El orden de los bloques no se altera

Los bloques van en el orden de la plantilla, no en el orden en que aparecen en el
`.txt`. Si un `.txt` trae `[TRAMPAS]` antes de `[QUE HAGO YO]`, la ficha igual los pone
al revés: el orden lo define la plantilla, no el archivo de contenido.

**Y se señala.** Un `.txt` con los bloques desordenados suele ser síntoma de otra cosa
— que se escribió sin la plantilla a la vista, o que se copió de otra variante.

Nunca se reordena para que quede mejor. Aunque en un tema particular tenga más sentido
poner la secuencia antes que el mecanismo, el orden es fijo: esa estabilidad es lo que
hace que la posición funcione como índice mental entre fichas.

Si el orden fijo realmente no sirve para un tema, eso no se resuelve reordenando esa
ficha. Se consulta, y la salida puede ser una variante nueva, o un formato nuevo.

### Regla 7 — Todo string literal va con `.lit`

Llega en el `.txt` entre backticks y sale envuelto en el componente:

```
.txt   `CVE-2017-0144`
html   <span class="lit">CVE-2017-0144</span>
```

Los backticks no se conservan en la salida.

**Qué cuenta como literal.** La prueba: *¿esto se escribe tal cual en una terminal, en
un buscador o en un campo de configuración?*

| Sí | No |
|---|---|
| CVEs, boletines, TTPs de MITRE | Nombres de producto (Windows, FortiGate) |
| Comandos, rutas, nombres de archivo | Nombres de herramienta (EternalBlue, WannaCry) |
| Puertos, protocolos con versión | Conceptos (kernel, buffer overflow) |
| Firmas de IDS, nombres de proceso | |
| Claves de registro, cuentas del sistema | |

**El criterio lo fija el `.txt`, no el agente.** Si algo viene entre backticks, va con
`.lit` aunque parezca que no corresponde. Si no viene marcado, no se agrega.

**Excepción: componentes que ya se ven como literal.** `.lit` marca un fragmento
literal dentro de contenido que no lo es. Cuando el componente ya aplica monoespaciada
y negrita al elemento completo, envolverlo sería redundante y no se hace.

Hoy el único caso es `.pares .nombre`, que el CSS ya renderiza en mono y negrita:

```
.txt    `CVE-2017-0144` | la vulnerabilidad
html    <div class="nombre">CVE-2017-0144</div>
```

En cambio, el `.lit` sí es necesario dentro de una `.lista`, un `.parrafo` o una
`.celda` — donde el texto va en la tipografía de cuerpo —, en `.pares.ancho .nombre` (el
glosario), que también va en tipografía de cuerpo, y en `.nota-loop` y `.pie`, que son
monoespaciados pero sin negrita.

**El `.lit` va adentro, nunca reemplaza.** Cuando todo el contenido de un elemento de
la plantilla es literal, el `<span class="lit">` se anida dentro de ese elemento, sin
sustituirlo. El elemento de la plantilla lleva sus propios estilos — color, tamaño,
márgenes — y reemplazarlo los pierde.

```
.txt    Escaneo | `445/TCP`
html    <div class="paso"><b>Escaneo</b><span><span class="lit">445/TCP</span></span></div>
```

Pasa en el segundo elemento de `.paso` y de `.celda`: ese `<span>` es parte del
componente, no un contenedor genérico.

Sí corresponde señalar una inconsistencia: el mismo término marcado en un lugar y sin
marcar en otro dentro del mismo archivo.

### Regla 8 — Nunca se generan datos técnicos con IA de imágenes

Los modelos de generación de imágenes deforman el texto que dibujan. Un CVE, un
comando o una ruta salen mal escritos, y en material de estudio un dato mal memorizado
cuesta más que un dato ausente.

La regla nació de un caso observado: una infografía profesional donde el prompt de
ejemplo decía "por tipo y **techo**" en lugar de "fecha", y un nombre propio salía como
"Julin". Errores que nadie revisó porque eran etiquetas decorativas.

Hoy el proyecto no usa imágenes generadas, así que la regla es preventiva. Si en algún
momento se agregan ilustraciones:

- Se generan **sin texto** — el prompt lo incluye explícitamente
- Cualquier etiqueta, rótulo o dato va en HTML encima de la imagen
- Ningún dato técnico se confía a un píxel

Vale para diagramas, gráficos, iconos con texto y capturas simuladas: cualquier cosa
donde un modelo dibuje caracteres.

### Regla 9 — Si no entra, se recorta el contenido

Una ficha es **una sola página**: un documento continuo, que se lee de arriba a abajo
con scroll. No tiene que entrar en una pantalla, pero tampoco puede volverse un texto
largo — para eso hará falta otro formato.

Si el contenido se pasa de eso, es un problema de contenido, no de diseño.

**No se hace:** achicar la tipografía, reducir espaciados, meter scroll interno en un
bloque, comprimir el interlineado. Todo eso disimula el problema y rompe la
consistencia con las demás fichas.

**Se hace:** avisar. "El bloque X tiene ocho ítems y la ficha se está estirando
demasiado. ¿Cuáles saco, o partimos el tema en dos?"

**Quién decide qué recortar: el autor.** Elegir qué información sobra es una decisión
de contenido, aunque se presente como un problema de espacio. El agente identifica el
exceso y propone opciones; no elige.

### Regla 10 — Ante cualquier duda, se consulta

Casos concretos en que corresponde frenar y preguntar.

**En el `.txt`:**

- Un marcador que no está en la lista del formato, o mal escrito
- Un bloque presente que no corresponde a ese `TIPO:`
- Una subsección en mayúsculas que la plantilla no contempla
- Falta un campo obligatorio del encabezado
- Un `TIPO:` que no corresponde a ninguna plantilla existente
- Una `!marca` en medio de una oración
- `!destacado` o `!incorrecto` sobre algo que no sea el nombre de un par ni un paso
- Datos que se contradicen dentro del mismo archivo

**Al construir:**

- Contenido que no encaja con ningún componente del CSS
- Un bloque que necesita una variante que no existe
- Un `.tres-up` con más de tres celdas, o un `.hitos` que no tenga exactamente tres entradas
- La ficha se estira más de lo razonable

**En el proyecto:**

- Cualquier tecnología nueva
- Cualquier cambio en plantillas, CSS o estructura de carpetas

**Cómo se consulta:** con la pregunta concreta y las opciones, no con un "no puedo
continuar". Por ejemplo: "El `.txt` trae `[REFERENCIAS]` como bloque, pero en este
formato `REFERENCIAS` es un campo del encabezado. ¿Lo muevo al encabezado, o querés que
sea un bloque nuevo?"

Lo que nunca se hace: interpretar, adivinar la intención, o resolver por analogía con
otra ficha.

### Regla 11 — Repositorio público, sin información sensible

El proyecto se publica en GitHub Pages: todo su contenido es visible para cualquiera.

**Qué no entra, en ningún archivo:**

- Credenciales, claves, tokens, contraseñas
- Nombres de clientes, empleadores o terceros
- Direcciones IP internas, nombres de host, dominios internos
- Rutas, configuraciones o topologías reales de una organización
- Capturas de logs o alertas de un entorno real
- Datos personales de cualquiera

El criterio: el material describe **cómo funcionan las cosas**, no cómo está
configurado un entorno concreto.

Cuando un ejemplo necesita un dato de ese tipo, se usa uno ficticio y se marca como
tal. Para direcciones IP conviene usar los rangos reservados para documentación —
`192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24` — que existen para eso y nunca
corresponden a un sistema real.

Si el agente detecta algo así en un `.txt`, frena y avisa antes de construir. No lo
elimina por su cuenta ni lo reemplaza: puede ser deliberado y ficticio.

---

## 5. Plantillas disponibles

Cada `TIPO:` válido (formato, o formato y variante) se define por tres piezas que
tienen que existir juntas:

| Pieza | Dónde | Para qué |
|---|---|---|
| Plantilla HTML | `plantillas/NOMBRE.html` | La estructura de salida |
| Valor de `TIPO:` | Declarado en el `.txt` | Selecciona la plantilla |
| Lista de bloques | `README.md` 2.1.2 | Qué se valida |

Hoy hay un formato, la ficha, con dos variantes. La definición de cada término está
en `README.md` punto 2.

### 5.1 `ficha-tecnica`

- **Plantilla:** `plantillas/ficha-tecnica.html`
- **Clase del `<body>`:** ninguna
- **Bloques, en orden:** `[BANDA CLAVE]` · `[IDENTIDAD]` · `[MECANISMO]` ·
  `[SECUENCIA]` · `[DATO ANCLA]` · `[QUE HAGO YO]` · `[TRAMPAS]`
- **Subsecciones esperadas:** los dos títulos de columna dentro de `[QUE HAGO YO]`

### 5.2 `ficha-divulgacion`

- **Plantilla:** `plantillas/ficha-divulgacion.html`
- **Clase del `<body>`:** `divulgacion`
- **Bloques, en orden:** `[BANDA CLAVE]` · `[QUE ES]` · `[COMO FUNCIONA]` ·
  `[EN LA PRACTICA]` · `[POR QUE IMPORTA]` · `[QUE HACER]` · `[GLOSARIO]`
- **Subsecciones esperadas:** `ANALOGIA`, `TRADUCCION` y `AVISO` dentro de
  `[COMO FUNCIONA]`; los dos títulos de columna dentro de `[QUE HACER]`

### 5.3 Un `TIPO:` que no existe

Si el `.txt` declara un `TIPO:` sin plantilla, **no se construye nada**. El agente no
improvisa una estructura ni adapta la plantilla más parecida. Avisa y espera: crear un
formato o una variante es trabajo del autor.

---

## 6. De bloque a HTML

### 6.1 `ficha-tecnica`

| Bloque | Componentes |
|---|---|
| `[BANDA CLAVE]` | `.banda-clave` con `.etiqueta` + `.frase` |
| `[IDENTIDAD]` | `.pares` — un par de `<div>` por línea |
| `[MECANISMO]` | `.parrafo` + `.aparte` + `.tres-up` con `.celda` |
| `[SECUENCIA]` | `.cadena` con `.paso` y `.flecha` + `.nota-loop` + `.aparte` |
| `[DATO ANCLA]` | `.ancla-num` + `.ancla-sub` + `.barra` + `.hitos` con `.hito` |
| `[QUE HAGO YO]` | `.dos-col` con `.col-tit` + `.lista` |
| `[TRAMPAS]` | `.trampas` con `.lista`; cada ítem `<b>mito</b> corrección` |

### 6.2 `ficha-divulgacion`

| Bloque | Componentes |
|---|---|
| `[BANDA CLAVE]` | igual que en técnica |
| `[QUE ES]` | `.parrafo` + `.tres-up` con `.celda` y `.cifra` |
| `[COMO FUNCIONA]` | `.parrafo` + `.analogia` con `.traduccion` y `.aviso` + `.aparte` |
| `[EN LA PRACTICA]` | igual que `[SECUENCIA]` |
| `[POR QUE IMPORTA]` | igual que `[DATO ANCLA]` + `.aparte` |
| `[QUE HACER]` | igual que `[QUE HAGO YO]` |
| `[GLOSARIO]` | `.pares.ancho` + `.aparte` |

### 6.3 De marca a HTML

| En el `.txt` | En el HTML |
|---|---|
| `` `texto` `` | `<span class="lit">texto</span>`, salvo en componentes que ya se ven como literal — ver regla 7 |
| `*texto*` | `<span class="destacar">texto</span>` |
| `!destacado` al final del elemento | clase `destacado` en ese elemento |
| `!incorrecto` al final del elemento | clase `incorrecto` en ese elemento |
| `>` al inicio de línea | `<p class="aparte">` |
| `↻` al inicio de línea | `<div class="nota-loop">`; el `↻` se conserva en el texto |
| `\|` | separa los dos `<div>` de un par, o `<b>` de `<span>` |
| `-` al inicio de línea | `<li>` de `.lista`, o una `.celda` de `.tres-up` |

Las marcas de apertura y cierre no se conservan en la salida, salvo el `↻`, que es parte
visible de la nota.

`!destacado` e `!incorrecto` solo tienen estilo sobre el `.nombre` de un `.pares` y sobre
un `.paso`. Sobre cualquier otro elemento se consulta.

### 6.4 Lo que no es un bloque

Además de los bloques, la ficha tiene partes que salen de otras fuentes, y algunos
bloques se leen por posición.

| Parte | Origen |
|---|---|
| `<h1>` | Campo `TITULO` |
| `<title>` | Campo `TITULO`, el mismo texto que el `<h1>`, sin agregarle nada |
| `.subtitulo` | Campo `SUBTITULO`; si no viene, se borra la línea |
| `.meta` | Número del archivo (`NN.N`) + nombre de la carpeta del área: `01.1 · vulnerabilidades` |
| `.etiqueta` de `.banda-clave` | Texto fijo de la plantilla |
| `.pie`, izquierda | Campo `REFERENCIAS`; si no viene, el `<span>` queda vacío |
| `.pie`, derecha | Texto fijo de la plantilla: enlace al índice y nombre de la variante |

**Lecturas por posición**

- `[DATO ANCLA]` y `[POR QUE IMPORTA]`: la primera línea va en `.ancla-num`, la segunda
  en `.ancla-sub`, y cada línea `fecha | qué pasó` es un `.hito` (`<b>` la fecha,
  `<span>` lo que pasó).
- `[TRAMPAS]`: en cada `"mito" | corrección`, el mito va en `<b>` con sus comillas, tal
  como viene en el `.txt`, y la corrección va como texto suelto a continuación, sin
  `<span>`.

**Caracteres especiales.** `&`, `<` y `>` del contenido se escriben como entidades
HTML (`&amp;`, `&lt;`, `&gt;`).

---

## 7. El índice

`publicado/index.html` es la portada. Se actualiza en la misma tarea en que se
construye una ficha, no después.

### 7.1 Estructura

Dos niveles: una `<section class="area">` por área, con su `.area-tit`, y adentro una
`.rejilla` con una `.tarjeta` por ficha.

### 7.2 De dónde sale cada dato de la tarjeta

| Elemento | Origen |
|---|---|
| `href` | Ruta relativa a la ficha, desde `publicado/` |
| `.num` | Número del archivo + formato y variante: `01.1 · ficha técnica` |
| `<h2>` | Campo `TITULO` del `.txt` |
| `.clave` | Contenido de `[BANDA CLAVE]`, completo |
| `.tags` | Todos los términos de `CLAVES`, en el orden en que están escritos |

### 7.3 Reglas del índice

- Si el área todavía no tiene sección, se crea
- La tarjeta va al final de su área, respetando el orden numérico
- El conteo de la cabecera se actualiza: áreas, temas y fichas
- Las tarjetas `.vacia` son temas pendientes anotados por el autor: no se tocan ni se
  eliminan salvo pedido explícito

---

## 8. Vocabulario de CSS

`estilo.css` está dividido en 19 secciones numeradas. Las clases describen **la forma
que toma el contenido**, no el tema: por eso el mismo componente sirve en bloques
distintos.

Si hay diferencia entre esta tabla y el archivo, **manda el archivo**.

### 8.1 Estructura de página

| Clase | Sección | Qué es |
|---|---|---|
| `.ficha` | 04 | Contenedor de una ficha |
| `.indice` | 17 | Contenedor de la portada |
| `.cabecera` | 05 | Encabezado, con `h1` |
| `.subtitulo` | 05 | Línea de contexto bajo el título |
| `.meta` | 05 | Bloque monoespaciado a la derecha del encabezado |
| `.pie` | 15 | Pie de dos columnas |
| `.bloque` | 07 | Un bloque de contenido |
| `.bloque-cab` + `.bloque-tit` | 07 | Cabecera y título de un bloque |

### 8.2 Componentes de contenido

| Clase | Sección | Qué es | Modificadores |
|---|---|---|---|
| `.banda-clave` | 06 | Franja superior, con `.etiqueta` y `.frase` | — |
| `.pares` | 08 | Término → definición, en dos columnas | `.ancho` para términos en texto normal; `.nombre.destacado` y `.nombre.incorrecto` |
| `.tres-up` + `.celda` | 09 | Hasta tres datos en fila; con 1 o 2 celdas se reparte el ancho entre las que haya | `.cifra` dentro de `.celda` para números grandes |
| `.cadena` + `.paso` | 10 | Secuencia horizontal, con `.flecha` entre pasos | `.paso.destacado`, `.paso.incorrecto` |
| `.nota-loop` | 10 | Nota al pie de una secuencia que se repite | — |
| `.ancla-num` + `.ancla-sub` | 11 | Dato memorable, en grande | — |
| `.barra` + `.hitos` + `.hito` | 11 | Línea de tiempo de tres puntos | — |
| `.dos-col` + `.col-tit` | 12 | Dos columnas con título | — |
| `.lista` | 12 | Lista con viñeta | — |
| `.analogia` | 13 | Caja de analogía, con `.traduccion` y `.aviso` | — |
| `.trampas` | 14 | Caja punteada de mitos | — |

### 8.3 Utilidades de texto

| Clase | Sección | Qué es |
|---|---|---|
| `.lit` | 15 | String literal, en monoespaciada |
| `.destacar` | 15 | Fragmento resaltado dentro de una línea |
| `.incorrecto` | 15 | Fragmento marcado como erróneo |
| `.parrafo` | 15 | Párrafo de cuerpo. Dos seguidos se separan solos |
| `.aparte` | 15 | Comentario al margen, en gris y cursiva |
| `.chapa` | 05 | Etiqueta chica con borde |

### 8.4 Índice

| Clase | Sección | Qué es |
|---|---|---|
| `.area` + `.area-tit` | 17 | Agrupación por área |
| `.rejilla` | 17 | Grilla de tarjetas |
| `.tarjeta` | 17 | Tarjeta de una ficha, con `.num`, `h2`, `.clave` y `.tags` |
| `.tarjeta.vacia` | 17 | Tema pendiente, en punteado |

### 8.5 Lo que no se toca al construir

Las secciones 01 (tipografías), 02 (tokens), 03 (base), 16 (variante divulgación),
18 (responsivo) y 19 (impresión) son infraestructura. No se editan al construir una
ficha, y modificarlas requiere aprobación previa.

---

## 9. Qué actualizar cuando algo cambia

Este archivo tiene que reflejar el estado real del proyecto. Un archivo de
instrucciones desactualizado es peor que no tenerlo: el agente lo va a seguir igual.

| Si cambia… | Actualizar |
|---|---|
| Se agrega una variante | `plantillas/`, punto 5, punto 6, `README.md` 2.1.1 y 2.1.2, `FORMATOS.md` 2 y su plantilla |
| Se agrega un formato | `plantillas/`, punto 5, punto 6, `README.md` punto 2 (sección nueva con sus bloques), `FORMATOS.md` 2 y su plantilla, y `estilo.css` + punto 8 si trae componentes |
| Se agrega o quita un bloque de una variante | La plantilla, puntos 5 y 6, `README.md` 2.1.2, `FORMATOS.md` 5 o 6 (la plantilla de esa variante) |
| Se agrega un componente de CSS | `estilo.css` (sección nueva al final), punto 8, y `README.md` 3.4 si cambia el criterio |
| Se agrega o cambia una marca del `.txt` | Punto 6.3, `README.md` 2.1.5, `FORMATOS.md` 4.3 |
| Se agrega un campo al encabezado | Las plantillas, punto 6.4, `README.md` 2.1.4, `FORMATOS.md` 4.1 |
| Cambia una regla | Punto 4, `README.md` punto 4 |
| Se agrega un área | Sólo crear la carpeta en `contenidos/` y en `publicado/` |

Esta tabla tiene una copia en `README.md` 7.3, para quien lee el proyecto sin abrir este
archivo. Cuando cambia una, cambia la otra.

Cuando el agente hace un cambio que toca alguna de estas filas, **actualiza la
documentación en la misma tarea** y avisa qué archivos tocó. No queda para después.

Si el autor hace el cambio por su cuenta, corresponde señalar qué quedó desactualizado.

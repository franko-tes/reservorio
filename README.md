# Reservorio de estudio

Material de estudio propio sobre temas técnicos: redes, Linux, contenedores,
seguridad, protocolos, herramientas.

Cada tema se documenta en el formato que mejor le sirva. Hoy existe uno:

1. **Ficha**: una página con estructura fija, pensada como ayuda-memoria.

Se irán agregando otros a medida que hagan falta.

Todo se construye en HTML, comparte una única hoja de estilos, y se abre desde un
índice común.

Este archivo existe para dar contexto a cualquier persona que abra esta carpeta. Las
instrucciones de trabajo para agentes de IA están en `AGENTS.md`.

---

## Índice

1. [Para qué sirve esto](#1-para-qué-sirve-esto)
2. [Formatos](#2-formatos)
   - 2.1 [Ficha](#21-ficha)
     - 2.1.1 [Dos variantes](#211-dos-variantes)
     - 2.1.2 [Bloques de cada variante](#212-bloques-de-cada-variante)
     - 2.1.3 [Son dos contenidos distintos, no uno traducido](#213-son-dos-contenidos-distintos-no-uno-traducido)
     - 2.1.4 [Encabezado del `.txt`](#214-encabezado-del-txt)
     - 2.1.5 [Marcas del contenido](#215-marcas-del-contenido)
3. [Archivos](#3-archivos)
   - 3.1 [El `.txt` manda](#31-el-txt-manda)
   - 3.2 [Áreas](#32-áreas)
   - 3.3 [Numeración](#33-numeración)
   - 3.4 [El CSS nombra formas, no temas](#34-el-css-nombra-formas-no-temas)
   - 3.5 [Rutas al CSS](#35-rutas-al-css)
4. [Reglas](#4-reglas)
5. [Cómo se agrega un tema](#5-cómo-se-agrega-un-tema)
6. [Ver y exportar](#6-ver-y-exportar)
   - 6.1 [Abrir](#61-abrir)
   - 6.2 [Exportar a imagen](#62-exportar-a-imagen)
   - 6.3 [Exportar a PDF](#63-exportar-a-pdf)
   - 6.4 [Tipografías](#64-tipografías)
7. [Evolución](#7-evolución)
   - 7.1 [Cuando algo no encaja](#71-cuando-algo-no-encaja)
   - 7.2 [Agregar antes que modificar](#72-agregar-antes-que-modificar)
   - 7.3 [Qué actualizar cuando algo cambia](#73-qué-actualizar-cuando-algo-cambia)

---

## 1. Para qué sirve esto

El problema que resuelve no es *aprender* un tema, sino **volver a encontrarlo meses
después**.

Estudiar muchos temas en paralelo deja el conocimiento repartido en notas sueltas,
conversaciones viejas y capturas de pantalla. Cuando hace falta recuperar algo, no
está el material: está el recuerdo de haberlo estudiado.

Este reservorio es el lugar donde ese material queda. Un tema estudiado se documenta
una vez, con la forma que le corresponda, y se puede volver a él cuantas veces sea
necesario.

De ahí salen tres criterios que valen para cualquier formato:

- **El material asume que el tema ya se estudió.** No enseña desde cero: sirve para
  recuperar lo que se aprendió en otro momento.
- **Cada formato tiene su propia estructura; la base visual es común.** Un apunte
  largo y una ficha no se organizan igual — no deberían — pero comparten colores,
  tipografías y jerarquía. La hoja de estilos crece con cada formato nuevo: se
  agregan componentes, no se reemplazan los que ya existen.
- **El contenido lo aporta quien estudió el tema.** Este proyecto documenta y
  construye; no investiga ni completa lo que falte.

---

## 2. Formatos

### 2.1 Ficha

Una ficha es **una sola página** que condensa un tema en bloques fijos. No reemplaza
al material de estudio: sirve para volver a activarlo rápido.

Tres cosas la definen:

- **Es corta a propósito.** Si un tema no entra, no se agranda la ficha: se recorta
  el contenido o se parte en dos temas.
- **La posición de los bloques es información.** Después de varias fichas, la
  ubicación funciona como índice mental — "lo verde de la derecha es siempre qué hago
  con esto" — y se encuentra algo sin leer la ficha entera.
- **El esqueleto no depende del tema.** Los bloques no preguntan sobre redes ni sobre
  seguridad: preguntan cómo se llama, por qué pasa, en qué orden, cuál es el gancho y
  qué se hace con eso. Eso sirve para cualquier tema técnico.

#### 2.1.1 Dos variantes

| Variante | Para quién | `TIPO:` | Clase en `<body>` |
|---|---|---|---|
| **Técnica** | Repaso propio | `ficha-tecnica` | *(ninguna)* |
| **Divulgación** | Alguien que no conoce el tema | `ficha-divulgacion` | `divulgacion` |

Ambas usan el mismo CSS. Lo que cambia es el contenido y, sobre todo, **el orden y el
nombre de los bloques**.

- La técnica abre con **Identidad** (los nombres), porque para quien ya estudió el
  tema, los nombres son el mejor gancho.
- La de divulgación abre con **Qué es** y manda los nombres al final como
  **Glosario**, porque para quien no sabe nada, un nombre sin contexto no engancha con
  nada.

No todos los temas necesitan versión de divulgación. La mayoría tiene solo la técnica.

#### 2.1.2 Bloques de cada variante

Cada variante tiene su propia lista. Los marcadores se escriben **en mayúsculas y sin
acentos**, y el `TIPO:` del archivo determina contra cuál lista se valida.

**`ficha-tecnica`**

| Marcador | Qué contiene |
|---|---|
| `[BANDA CLAVE]` | La frase que reconstruye todo el tema |
| `[IDENTIDAD]` | Los nombres que se confunden entre sí |
| `[MECANISMO]` | Por qué funciona |
| `[SECUENCIA]` | En qué orden pasa |
| `[DATO ANCLA]` | El número o hecho que se pega solo |
| `[QUE HAGO YO]` | Lo operativo, en dos columnas |
| `[TRAMPAS]` | Lo que se cree mal |

**`ficha-divulgacion`**

| Marcador | Qué contiene |
|---|---|
| `[BANDA CLAVE]` | La frase que resume todo |
| `[QUE ES]` | De qué se trata, en contexto |
| `[COMO FUNCIONA]` | El mecanismo, con analogía si hace falta |
| `[EN LA PRACTICA]` | Cómo se ve, cómo opera, qué secuencia sigue |
| `[POR QUE IMPORTA]` | Por qué le debería interesar a quien lee |
| `[QUE HACER]` | Recomendaciones, decisiones, próximos pasos |
| `[GLOSARIO]` | Los términos, al final |

**Los bloques vacíos se omiten, no se rellenan.** No todos los temas llenan los siete:
un tema conceptual puede no tener dato ancla, una comparación no tiene secuencia. Una
ficha de cinco bloques honestos vale más que una de siete con dos inventados. Lo que
se mantiene siempre es el **orden relativo** de los que sí están.

#### 2.1.3 Son dos contenidos distintos, no uno traducido

Cada variante tiene **su propio archivo** en `contenidos/`:

```
contenidos/
├── 001-eternalblue.txt              → TIPO: ficha-tecnica
└── 001-eternalblue-divulgacion.txt  → TIPO: ficha-divulgacion
```

La versión de divulgación **no es la técnica escrita más fácil**. Cambia el orden,
cambian los bloques y cambia el texto entero. Por eso son dos archivos, dos plantillas
y dos listas de marcadores.

#### 2.1.4 Encabezado del `.txt`

Cada archivo abre con un encabezado de cuatro campos, uno por línea, antes del primer
bloque:

```
TIPO: ficha-tecnica
TITULO: EternalBlue / MS17-010
SUBTITULO: La vulnerabilidad que hizo posible WannaCry
CLAVES: smb, ransomware, wannacry, kernel, wormable
REFERENCIAS: MITRE ATT&CK · T1210 · T1021.002 · T1486 · T1490
```

| Campo | Obligatorio | Para qué |
|---|---|---|
| `TIPO` | sí | Elige la plantilla, valida los bloques y define la clase del `<body>` |
| `TITULO` | sí | Va en el `<h1>` y en la tarjeta del índice |
| `SUBTITULO` | no | Línea de contexto bajo el título. Si falta, no se muestra |
| `CLAVES` | sí | Términos de búsqueda. Ver más abajo |
| `REFERENCIAS` | no | Va al pie. TTPs de MITRE, CVEs, RFCs, páginas de `man`: dónde seguir |

El valor de `TIPO:` nombra **el formato y la variante**, separados por guión. Así, al
agregarse formatos nuevos, el mismo campo sigue sirviendo sin ambigüedad.

No hay campo de área: **la carpeta ya lo dice**. Duplicarlo crearía dos fuentes de
verdad que pueden contradecirse si el archivo se mueve.

`CLAVES` hoy no se usa en ninguna parte visible. Se completa igual, porque el buscador
que viene más adelante va a leer de ahí, y completar cuarenta archivos a mano después
es mucho peor que escribir una línea ahora.

#### 2.1.5 Marcas del contenido

Dentro de los bloques, el `.txt` usa un puñado de marcas. Son las mismas para las dos
variantes.

| Marca | Para qué | Ejemplo |
|---|---|---|
| `` `texto` `` | String literal: CVE, comando, ruta, puerto | `` `vssadmin delete shadows` `` |
| `*texto*` | Destacar un fragmento dentro de una línea | `en el perímetro *y entre segmentos*` |
| `\|` | Separa término de definición, o título de descripción | `` `MS17-010` \| el parche `` |
| `-` | Ítem de una lista | `- Backups offline` |
| `>` | Comentario al margen, en tono aparte | `> Es aritmética mal hecha.` |
| `!destacado` `!incorrecto` | Marca **un elemento entero** | `` `EternalBlue` !incorrecto \| el exploit `` |
| `↻` | Nota de bucle, al pie de una secuencia | `↻ el último paso reinicia el primero` |

Dos aclaraciones que evitan confusiones:

- **`*asteriscos*` es para fragmentos; `!marca` es para elementos completos.** Una
  `!marca` en medio de una oración no tiene dónde terminar: si aparece así, es un
  error del `.txt` y se consulta antes de construir.
- **Las marcas no llevan color propio.** `!destacado` e `!incorrecto` nombran la
  función, no el tono. Si la paleta cambia, el `.txt` no se toca.

**Subsecciones dentro de un bloque.** Una línea sola en MAYÚSCULAS, sin corchetes,
abre una subsección. Se usa cuando un bloque tiene partes con nombre:

```
[QUE HAGO YO]
MITIGAR
- Aplicar el parche `MS17-010`

DETECTAR
- Tráfico SMB este-oeste anómalo
```

Las subsecciones que espera cada bloque están fijadas por su plantilla: los títulos de
las dos columnas en `[QUE HAGO YO]` y `[QUE HACER]`, y las tres partes de la analogía
(`ANALOGIA`, `TRADUCCION`, `AVISO`) en `[COMO FUNCIONA]`. Una subsección que la
plantilla no contempla se consulta.

---

## 3. Archivos

```
reservorio/
├── README.md
├── AGENTS.md                              instrucciones para agentes de IA
├── estilo.css                             el diseño, uno solo para todo
│
├── fuentes/                               tipografías alojadas localmente
│   ├── Inter-Regular.ttf
│   ├── Inter-Medium.ttf
│   ├── JetBrainsMono-Regular.ttf
│   ├── JetBrainsMono-Bold.ttf
│   ├── OFL-Inter.txt                      licencias, se distribuyen con la fuente
│   └── OFL-JetBrainsMono.txt
│
├── plantillas/
│   ├── ficha-tecnica.html
│   └── ficha-divulgacion.html
│
├── contenidos/                            la fuente de verdad
│   └── vulnerabilidades/
│       ├── 01.1-eternalblue.txt
│       └── 01.2-eternalblue-divulgacion.txt
│
└── publicado/                             lo que se abre en el navegador
    ├── index.html
    └── vulnerabilidades/
        ├── 01.1-eternalblue.html
        └── 01.2-eternalblue-divulgacion.html
```

### 3.1 El `.txt` manda

`contenidos/` es el original; `publicado/` es la salida.

Para cambiar algo se edita el `.txt` y se reconstruye el `.html`. **Los archivos de
`publicado/` no se editan a mano**: si se editan, las dos versiones dejan de coincidir
y se pierde cuál es la buena.

### 3.2 Áreas

Los temas se agrupan por área, y la misma división se repite en `contenidos/` y en
`publicado/`.

Conviene que las áreas sean **angostas**: `vulnerabilidades`, `active-directory`,
`redes`, `linux`. Un área tan amplia que termine conteniendo todo no ordena nada.

**Las áreas se crean cuando hay contenido**, no antes. Una carpeta vacía esperando
temas futuros es ruido.

### 3.3 Numeración

```
01.1-eternalblue.txt              ← tema 01, pieza 1
01.2-eternalblue-divulgacion.txt  ← tema 01, pieza 2
02.1-kerberoasting.txt            ← tema 02, pieza 1
```

- El **primer número es el tema**, y arranca en `01` dentro de cada área.
- El **segundo es la pieza**, en orden de creación. No tiene significado fijo: qué es
  cada una lo dice el sufijo del nombre (`-divulgacion`, `-apunte`).
- El formato base va sin sufijo.

No hay numeración global ni contador de archivos en los nombres: un número que lleve
la cuenta se rompe apenas se borra o se inserta algo en el medio.

Para saber cuánto hay, se cuenta desde la terminal:

```bash
find contenidos -name "*.txt" | wc -l        # archivos en total
ls contenidos/vulnerabilidades/ | wc -l      # archivos de un área
```

Más adelante, un script podrá generar el índice con sus conteos automáticamente.

### 3.4 El CSS nombra formas, no temas

`estilo.css` está organizado en secciones numeradas, y sus clases describen **la forma
que toma el contenido**, no el tema que lo contiene: `.pares` es "término y
definición", `.cadena` es "pasos en fila", `.lit` es "texto que se escribe exacto".

Por eso el mismo componente sirve en contextos distintos — `.pares` arma tanto el
bloque de identidad de una ficha técnica como el glosario de una de divulgación — y
por eso cambiar los nombres de los bloques no obliga a tocar el CSS.

Cuando un formato nuevo necesita una forma que no existe, se **agrega** una sección al
final del archivo. No se reemplazan las que ya están, porque romperían el material ya
construido.

La lista completa de componentes, con qué bloque usa cada uno, está en `AGENTS.md`.

### 3.5 Rutas al CSS

La profundidad es fija, así que el enlace también:

| Archivo | Enlace |
|---|---|
| `publicado/index.html` | `../estilo.css` |
| `publicado/area/loquesea.html` | `../../estilo.css` |

---

## 4. Reglas

Las once reglas del proyecto. Las que tienen desarrollo remiten al punto donde se
explican.

1. **El `.txt` es el original; el `.html` no se edita a mano.** Para cambiar algo se
   edita el contenido y se reconstruye la salida. → 3.1
2. **Un solo `estilo.css`.** Crece agregando secciones, nunca reemplazando las que ya
   están. → 3.4
3. **El contenido lo aporta quien estudió el tema.** Este proyecto documenta y
   construye: no investiga, no completa, no opina sobre qué debería decir una ficha.
   → 1
4. **Nunca se inventan datos.** Fechas, cifras, comandos, nombres de firmas: si no
   está en el `.txt`, no entra en la salida.
5. **Los bloques vacíos se omiten, no se rellenan.** Vale más una ficha de cinco
   bloques honestos que una de siete con dos inventados. → 2.1.2
6. **El orden de los bloques no se altera dentro de un mismo formato.** Es lo que hace
   que la posición signifique algo. → 2.1
7. **Todo string literal va con `.lit`.** CVEs, rutas, comandos, puertos, nombres de
   archivo: cualquier cosa que se escriba tal cual en una terminal.
8. **Nunca se generan datos técnicos con IA de imágenes.** Los modelos de imagen
   deforman el texto, y un dato mal escrito en material de estudio es peor que no
   tener el material. Si se agregan ilustraciones, se generan sin texto y las
   etiquetas se ponen en HTML encima.
9. **Si no entra en una página, se recorta el contenido.** No se achica la tipografía
   ni se agrega scroll. Qué recortar lo decide el autor, no el agente.
10. **Ante cualquier duda, se consulta.** Un marcador que no coincide, un bloque que
    no encaja, un componente que no existe: se pregunta. No se interpreta ni se
    improvisa.
11. **Este es un repositorio público. No entra información sensible.** Ni
    credenciales, claves o tokens; ni datos de clientes, empleadores o terceros; ni
    direcciones IP internas, nombres de host, rutas o configuraciones reales de una
    organización. El material describe **cómo funcionan las cosas**, no cómo está
    configurado un entorno concreto. Si un ejemplo necesita un dato de ese tipo, se
    inventa uno ficticio y se marca como tal.

---

## 5. Cómo se agrega un tema

1. **Estudiar el tema.** Fuera de este proyecto, donde sea.
2. **Escribir el `.txt`.** Con el encabezado y los bloques del formato elegido
   (ver 2.1.2 y 2.1.4). Puede escribirse a mano o pedírselo a la misma IA con la que
   se estudió el tema, que es la que tiene el contexto completo.
3. **Guardarlo** en `contenidos/area/NN.N-nombre.txt`, siguiendo la numeración de 3.3.
   Si el área no existe todavía, se crea.
4. **Pedirle al agente que lo construya**, indicando qué archivo y qué formato.
5. **Revisar el resultado** en el navegador y, si algo no cierra, corregir el `.txt` y
   reconstruir. Nunca el `.html`.

El procedimiento de construcción — cómo se traduce cada bloque a HTML, qué componente
usa cada uno, cómo se valida — está en `AGENTS.md`.

---

## 6. Ver y exportar

### 6.1 Abrir

```bash
xdg-open publicado/index.html
```

Se abre con doble clic, sin servidor. El CSS externo funciona con `file://`.

Esto puede cambiar si más adelante se agrega JavaScript — el buscador, por ejemplo —
según cómo se implemente. Mientras el material sea HTML y CSS, no hace falta nada.

### 6.2 Exportar a imagen

```bash
chromium --headless --screenshot=ficha.png \
  --window-size=1000,2100 --hide-scrollbars \
  file://$PWD/publicado/vulnerabilidades/01.1-eternalblue.html
```

El segundo número de `--window-size` es el alto, y **cambia según la ficha**. Si la
captura sale cortada o con espacio de sobra, se ajusta ese valor.

### 6.3 Exportar a PDF e imprimir

`Ctrl+P` en el navegador → guardar como PDF o mandar a la impresora.

`estilo.css` trae reglas `@media print` que ajustan el tamaño a A4 y **invierten los
colores a fondo claro**. En papel manda la legibilidad, no la estética: el material se
lee igual, pero sin gastar tinta en un fondo oscuro.

### 6.4 Tipografías

Las fuentes están **alojadas en el proyecto**, en `fuentes/`. No se cargan de ningún
servicio externo, así que el material se ve igual con o sin conexión y no depende de
que un servicio siga existiendo dentro de unos años.

Son dos: **Inter** para el texto y **JetBrains Mono** para los literales. La
monoespaciada no es decorativa — distingue el cero de la O y el uno de la ele, que en
un CVE o en un comando importa.

---

## 7. Evolución

Todo lo anterior es **el estado actual**, no un diseño cerrado. Hoy hay un solo formato
porque es el único que se necesitó hasta ahora; van a aparecer temas que pidan otros.

Los formatos, plantillas y componentes nuevos **los define el autor**. El agente no los
propone por su cuenta ni los improvisa sobre la marcha.

### 7.1 Cuando algo no encaja

Un tema puede traer contenido que la plantilla no contempla. Ahí el agente consulta, y
la respuesta va a ser una de estas tres:

1. **Agregar un componente** a `estilo.css`, y a la plantilla si corresponde.
2. **Reutilizar uno existente** con otra etiqueta o en otro contexto.
3. **Recortar el contenido** para que entre en lo que ya hay.

### 7.2 Agregar antes que modificar

Ante la duda, la primera opción es **agregar**: un componente nuevo no afecta a nada
de lo ya construido, mientras que cambiar el significado de uno existente se propaga a
todo el material anterior.

No es una regla rígida. Si hay que modificar algo, se modifica — pero evaluando antes
qué se rompe y qué hay que rehacer.

### 7.3 Qué actualizar cuando algo cambia

| Si se agrega o cambia… | Actualizar |
|---|---|
| Un formato | `plantillas/`, valores válidos de `TIPO:`, punto 2, `AGENTS.md` |
| Un bloque de un formato | La plantilla, 2.1.2, `AGENTS.md` |
| Un componente de CSS | `estilo.css`, 3.4 si cambia el criterio, `AGENTS.md` |
| Una regla de trabajo | Punto 4, `AGENTS.md` |
| Un área | Solo crear la carpeta, en `contenidos/` y en `publicado/` |

`AGENTS.md` aparece en casi todas las filas: **se actualiza siempre**. Un archivo de
instrucciones desactualizado es peor que no tenerlo, porque el agente lo va a seguir
igual.

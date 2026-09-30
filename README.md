# Reservorio de estudio

Material de estudio propio sobre diversos temas: redes, Linux, contenedores,
seguridad, protocolos, herramientas.

Cada tema se documenta en un `.txt`, que se estructura combinando piezas de un
catálogo previamente configurado (títulos, listas, términos, secuencias,
árboles...).

Luego, todo se construye en HTML, comparte una única hoja de estilos, y se abre
desde un índice común.

Las instrucciones de trabajo para agentes de IA están en `AGENTS.md`.

---

## Índice

1. [Para qué sirve esto](#1-para-qué-sirve-esto)
2. [Plantillas](#2-plantillas)
   - 2.1 [Ficha](#21-ficha)
     - 2.1.1 [Un tema puede tener más de una ficha](#211-un-tema-puede-tener-más-de-una-ficha)
     - 2.1.2 [Encabezado del `.txt`](#212-encabezado-del-txt)
     - 2.1.3 [Marcas del `.txt`](#213-marcas-del-txt)
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
   - 6.3 [Exportar a PDF e imprimir](#63-exportar-a-pdf-e-imprimir)
   - 6.4 [Tipografías](#64-tipografías)
7. [Evolución](#7-evolución)
   - 7.1 [Cuando algo no encaja](#71-cuando-algo-no-encaja)
   - 7.2 [Agregar antes que modificar](#72-agregar-antes-que-modificar)
   - 7.3 [Qué actualizar cuando algo cambia](#73-qué-actualizar-cuando-algo-cambia)

---

## 1. Para qué sirve esto

El problema que resuelve no es _aprender_ un tema, sino **volver a encontrarlo meses después**.

Estudiar muchos temas en paralelo deja el conocimiento repartido en notas sueltas, conversaciones viejas y capturas de pantalla.

Este reservorio es el lugar donde ese material queda. Un tema estudiado se documenta
una vez, y se puede volver a él cuantas veces sea necesario. O incluso actualizar lo documentado.

De ahí salen tres criterios:

- **El material asume que el tema ya se estudió.** No enseña desde cero, sirve para
  repasar lo que se aprendió anteriormente.
- **El contenido de cada tema es libre, pero manteniendo una base visual en común.** Cada archivo `.txt` se estructura a partir de piezas configuradas y documentadas en un catálogo, permitiendo mantener colores, tipografías y jerarquía iguales, entre distintos temas. La hoja de estilos crece agregando
  componentes nuevos.
- **El contenido lo aporta quien estudió el tema.** Este proyecto documenta y
  construye; no investiga ni completa lo que falte.

---

## 2. Plantillas

Una **plantilla** es una familia de documento: hoy la ficha, y mañana quizás un
apunte o una lista de definiciones. Cada plantilla se arma con un **esqueleto** — el
`.html` que se copia y rellena — y un catálogo de piezas disponibles, documentado en
`FORMATOS.md`.

No hay `TIPO:` ni variantes fijas por archivo: un solo esqueleto (`esqueleto.html`)
alcanza para cualquier tema de la plantilla, porque el catálogo es abierto y el orden
de las piezas lo decide quien escribe, no una estructura predefinida.

### 2.1 Ficha

Una ficha es **una sola página** que condensa un tema. No reemplaza al material de
estudio: sirve para volver a activarlo rápido.

Tres cosas la definen:

- **El orden y las piezas los decide quien escribe**, según lo que el tema pida. No
  hay una estructura fija que se repita igual en todas las fichas — cada una arma su
  propio catálogo de piezas, en el orden que tenga sentido para ese tema.
- **El catálogo es genérico.** Las piezas (una lista, un término y su definición, una
  secuencia de pasos, un árbol jerárquico...) no preguntan sobre un tema en
  particular — sirven para cualquiera. Eso es lo que las hace reutilizables.
- **Sigue siendo una sola página, de lectura continua.** El largo lo decide el
  contenido, no un límite fijo — pero sigue siendo un documento que se lee de una
  sentada con scroll, no algo que se reparte en varias páginas.

#### 2.1.1 Un tema puede tener más de una ficha

Sigue siendo válido escribir dos fichas sobre el mismo tema con enfoques distintos —
una técnica, para repasar, y otra para alguien que no conoce el tema. Pero ya no es
un mecanismo del sistema: no hay un `TIPO:` que las distinga ni un esqueleto separado
para cada una. Cada ficha es, simplemente, un `.txt` más, armado con las piezas del
catálogo que su enfoque necesite.

La de divulgación **no es la técnica escrita más fácil**: cambia el orden, cambian
las piezas y cambia el texto entero. Si se escriben las dos, son dos archivos
separados en `contenidos/`, cada uno pensado desde cero para su lector.

#### 2.1.2 Encabezado del `.txt`

Cada archivo abre con un encabezado, un campo por línea, antes del contenido:

```
TITULO: Active Directory
SUBTITULO: Introducción
RESUMEN: Servicio de directorio de Microsoft que centraliza identidades, autenticación y autorización de una organización.
CLAVES: active directory, AD, domain controller, LDAP, Kerberos, NTLM, Entra ID
REFERENCIAS:
```

| Campo         | Obligatorio | Para qué                                                                                                                                                                                                      |
| ------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `TITULO`      | sí          | Va en el `<h1>`, en el `<title>` y en la tarjeta del índice                                                                                                                                                   |
| `SUBTITULO`   | no          | Línea de contexto bajo el título. Si falta, no se muestra                                                                                                                                                     |
| `RESUMEN`     | sí          | Una frase que resume el tema. Se usa en la tarjeta del índice y en los metadatos de la página (`description`, `og:description`) — no es lo mismo que `SUBTITULO`, que es solo la línea visible bajo el título |
| `CLAVES`      | sí          | Términos de búsqueda y tags de la tarjeta del índice. Ver más abajo                                                                                                                                           |
| `REFERENCIAS` | no          | Va al pie. CVEs, TTPs de MITRE, RFCs, páginas de `man`: dónde seguir                                                                                                                                          |

No hay campo de área: **la carpeta ya lo dice**. Duplicarlo crearía dos fuentes de
verdad que pueden contradecirse si el archivo se mueve.

Cada término de `CLAVES` se muestra como tag en la tarjeta del índice, en el orden en
que está escrito. Por eso conviene que sean pocos: los imprescindibles. El buscador
que viene más adelante también va a leer de ahí, y completar cuarenta archivos a mano
después es mucho peor que escribir una línea ahora.

#### 2.1.3 Marcas del `.txt`

El catálogo completo de piezas y marcas — 18 piezas, cada una con su marca y un
ejemplo — vive en `FORMATOS.md`. Acá el resumen:

- `` `texto` `` marca un string literal: comando, ruta, CVE, puerto.
- `*texto*` destaca un fragmento; `~texto~` lo marca como incorrecto o erróneo. Son
  las dos únicas marcas de énfasis — no existen sufijos de elemento como
  `!destacado`/`!incorrecto`. Única excepción: en la pieza de secuencia, si el
  nombre completo de un paso va envuelto en `*...*` o `~...~`, se marca el recuadro
  entero, no solo el texto (ver `FORMATOS.md` 2.15).
- `!! frase` es la franja de idea clave. Puede aparecer en cualquier punto del texto,
  las veces que haga falta, sin una etiqueta fija.
- `## texto` abre una sección nueva; `### texto` abre un subtítulo dentro de ella.

Ante contenido que no encaje en ninguna pieza del catálogo, se consulta — no se
improvisa.

---

## 3. Archivos

```
reservorio/
├── README.md
├── AGENTS.md                              instrucciones para agentes de IA
├── FORMATOS.md                            catálogo de piezas para escribir el contenido
├── estilo.css                             el diseño, uno solo para todo
├── esqueleto.html                         el esqueleto único, se copia para cada ficha
│
├── fuentes/                               tipografías alojadas localmente
│   ├── Inter-Regular.ttf
│   ├── Inter-Medium.ttf
│   ├── JetBrainsMono-Regular.ttf
│   ├── JetBrainsMono-Bold.ttf
│   ├── OFL-Inter.txt                      licencias, se distribuyen con la fuente
│   └── OFL-JetBrainsMono.txt
│
├── contenidos/                            la fuente de verdad
│   ├── active-directory/
│   │   └── 01.1-active-directory-introduccion.txt
│   └── vulnerabilidades/
│       ├── 01.1-eternalblue.txt
│       └── 01.2-eternalblue-divulgacion.txt
│
└── publicado/                             lo que se abre en el navegador
    ├── index.html
    ├── active-directory/
    │   └── 01.1-active-directory-introduccion.html
    └── vulnerabilidades/
        ├── 01.1-eternalblue.html
        └── 01.2-eternalblue-divulgacion.html
```

### 3.1 El `.txt` manda

`contenidos/` es el original; `publicado/` es la salida.

Para cambiar algo se edita el `.txt` y se reconstruye el `.html`. **Los archivos de
`publicado/` no se editan a mano**: si se editan, las dos versiones dejan de coincidir
y se pierde cuál es la buena.

`publicado/index.html` es la excepción: junta datos de todas las fichas y se actualiza
tarjeta por tarjeta, no se regenera desde un solo `.txt`.

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
- La pieza base (hoy, la ficha técnica) va sin sufijo.

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

Por eso el mismo componente sirve en contextos distintos — `.pares` arma tanto un
grupo de nombres que se confunden entre sí como un glosario — y por eso el catálogo
de piezas no obliga a tocar el CSS cada vez que se usa una combinación distinta.

Cuando una plantilla nueva necesita una forma que no existe, se **agrega** una sección
al final del archivo. No se reemplazan las que ya están, porque romperían el material
ya construido.

La lista completa de componentes, con qué pieza usa cada uno, está en `AGENTS.md`.

### 3.5 Rutas al CSS

La profundidad es fija, así que el enlace también:

| Archivo                        | Enlace             |
| ------------------------------ | ------------------ |
| `publicado/index.html`         | `../estilo.css`    |
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
5. **Las piezas sin contenido real se omiten, no se rellenan.** Vale más una ficha
   con pocas piezas honestas que una completa con contenido inventado. → `FORMATOS.md`
6. **El orden de las piezas lo decide quien escribe el `.txt`.** Ya no hay un orden
   fijo que se repita entre fichas — cada tema arma sus piezas en el orden que tenga
   más sentido para él. → 2.1
7. **Todo string literal va con `.lit`.** CVEs, rutas, comandos, puertos, nombres de
   archivo: cualquier cosa que se escriba tal cual en una terminal, o que aparezca
   exactamente así en la salida de una herramienta real. La excepción son
   los componentes que ya se ven como un literal (monoespaciados y en negrita), donde
   marcarlo sería redundante.
8. **Nunca se generan datos técnicos con IA de imágenes.** Los modelos de imagen
   deforman el texto, y un dato mal escrito en material de estudio es peor que no
   tener el material. Si se agregan ilustraciones, se generan sin texto y las
   etiquetas se ponen en HTML encima.
9. **El texto puede ser tan largo como haga falta — pero no se simula que entra.** No
   hay límite de piezas ni de repeticiones: un paso o diez, una celda o ninguna. Lo
   que no se hace es achicar la tipografía ni comprimir el espaciado para forzar el
   contenido en menos espacio. Sigue siendo una sola página continua, de scroll, no
   un documento partido en varias.
10. **Ante cualquier duda, se consulta.** Contenido que no encaja en ninguna pieza del
    catálogo, una marca que no se entiende, un componente de CSS que no existe: se
    pregunta. No se interpreta ni se improvisa.
11. **Este es un repositorio público. No entra información sensible.** Ni
    credenciales, claves o tokens; ni datos de clientes, empleadores o terceros; ni
    direcciones IP internas, nombres de host, rutas o configuraciones reales de una
    organización. El material describe **cómo funcionan las cosas**, no cómo está
    configurado un entorno concreto. Si un ejemplo necesita un dato de ese tipo, se
    inventa uno ficticio y se marca como tal.

---

## 5. Cómo se agrega un tema

1. **Estudiar el tema.** Fuera de este proyecto, donde sea.
2. **Escribir el `.txt`.** `FORMATOS.md` tiene el catálogo completo de piezas, cómo
   marcarlas y el encabezado. Está pensado para llevárselo a la conversación donde se
   estudió el tema y pedirle a esa IA que vuelque el contenido, que es la que tiene
   el contexto completo.
3. **Guardarlo** en `contenidos/area/NN.N-nombre.txt`, siguiendo la numeración de 3.3.
   Si el área no existe todavía, se crea.
4. **Pedirle al agente que lo construya.**
5. **Revisar el resultado** en el navegador y, si algo no cierra, corregir el `.txt` y
   reconstruir. Nunca el `.html`.

El procedimiento de construcción — cómo se traduce cada pieza a HTML, qué componente
usa cada una, cómo se valida — está en `AGENTS.md`.

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

Todo lo anterior es **el estado actual**, no un diseño cerrado. Hoy hay una sola
plantilla porque es la única que se necesitó hasta ahora; van a aparecer temas que
pidan otras.

Las plantillas, los esqueletos, las piezas del catálogo y los componentes de CSS
nuevos **los define el autor**. El agente no los propone por su cuenta ni los
improvisa sobre la marcha.

### 7.1 Cuando algo no encaja

Un tema puede traer contenido que el esqueleto no contempla. Ahí el agente consulta, y
la respuesta va a ser una de estas tres:

1. **Agregar un componente** a `estilo.css`, y al esqueleto si corresponde.
2. **Reutilizar uno existente** con otra etiqueta o en otro contexto.
3. **Recortar el contenido** para que entre en lo que ya hay.

### 7.2 Agregar antes que modificar

Ante la duda, la primera opción es **agregar**: un componente nuevo no afecta a nada
de lo ya construido, mientras que cambiar el significado de uno existente se propaga a
todo el material anterior.

No es una regla rígida. Si hay que modificar algo, se modifica — pero evaluando antes
qué se rompe y qué hay que rehacer.

### 7.3 Qué actualizar cuando algo cambia

Cuando algo del sistema cambia (una plantilla, una pieza del catálogo, un componente
de CSS, una marca del `.txt`, una regla de trabajo) hay que tocar más de un documento.
La lista de qué actualizar en cada caso está en `AGENTS.md` punto 9.

`AGENTS.md` se actualiza siempre: un archivo de instrucciones desactualizado es peor
que no tenerlo, porque el agente lo va a seguir igual.

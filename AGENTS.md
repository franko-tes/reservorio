# AGENTS.md

Instrucciones de trabajo para agentes de IA que operen sobre este repositorio.
Reemplaza a la versión anterior, pensada para el sistema de `contenidos/` →
`publicado/` con esqueletos, que ya no existe.

Última revisión: octubre de 2026.

---

## 1. Qué es este proyecto

Un reservorio de material de estudio sobre temas técnicos, publicado como sitio
estático. Es documentación propia del progreso del autor, no una plataforma.

- Todo vive en `docs/` y se publica con GitHub Pages desde la rama `main`,
  carpeta `/docs`. El repositorio es público: ver la regla de datos sensibles
  en la sección 7.
- Pendiente de decidir: dominio propio (hoy, dirección `github.io`). Al
  definirlo, completar `og:url` y `og:image` de las fichas.
- El contenido lo escribe el autor. El agente ayuda con estructura, forma y
  revisión; no decide qué dice cada ficha.

## 2. Stack

**HTML y CSS. Nada más.** Sin JavaScript, frameworks, preprocesadores ni
dependencias externas.

- Las páginas tienen que abrirse con doble clic (`file://`) y desde GitHub Pages.
- Rutas siempre relativas.
- Cualquier tecnología nueva se propone y se espera la decisión del autor.

## 3. Estructura

```
docs/
  index.html                        portada: solo muestra áreas
  estilo.css                        hoja única compartida
  <area>/
    index.html                      índice del área: sus contenidos
    NN.N-<abreviatura>-<nombre>.html
```

Jerarquía: **área** (carpeta) → **tema** (primer número) → **contenido**
(segundo número).

- Nombre de archivo: `NN.N-nombre.html`. Ejemplo: `01.1-ad-introduccion.html`.
- El tema se llama como lo define el autor, y va como subtítulo de cada ficha.
  En Active Directory: tema 01 "Introducción" (`01.1`, `01.2`) y tema 02
  "Fundamental" (`02.1-ad-estructura.html`, primer grupo de un glosario que se
  planea en varios grupos).
- Un área puede tener muchos temas (se planean al menos 5 en Active Directory).
- `docs/fuentes/` no está en uso y no la referencia el CSS actual.

## 4. Cómo se trabaja con el autor

- **Analizar y proponer antes de cambiar.** Cuando el autor pide "analicemos" o
  "no cambiemos nada", no se toca ningún archivo.
- **Listas numeradas** para modificaciones, y se espera confirmación punto por
  punto.
- **Nunca se hace `git add`, `git commit` ni `git push`.** Lo hace siempre el
  autor. El agente solo pasa los comandos y muestra el diff si se lo piden;
  ante una pregunta ambigua ("¿podemos commitear?") se pregunta quién ejecuta.
- **Alcance mínimo:** solo se tocan los archivos que el pedido nombra.
- **Recomendar sí, aplicar sin aviso no.** El agente señala mejoras, pero la
  decisión es del autor.
- **Ante la duda, se pregunta**, con opciones y una recomendación, no con un
  "no puedo continuar".
- **Respaldar con datos.** Contrastes, medidas y comparaciones se calculan o se
  verifican en el navegador, no se afirman de memoria. Si algo no se pudo
  verificar, se dice.
- Se reconoce el error cuando lo hay (por ejemplo, recomendar un cambio que no
  se percibe).

## 5. Diseño decidido

### Paleta

**Gruvbox con acento naranja, modo oscuro fijo.** Sin modo claro en pantalla.
En impresión (`@media print`) se usa Gruvbox claro.

| Token | Valor | Uso |
|---|---|---|
| `--color-bg` | `#282828` | Fondo |
| `--color-bg-subtle` | `#3c3836` | Fondos suaves, callouts |
| `--color-text` | `#ebdbb2` | Texto |
| `--color-text-muted` | `#aca095` | Texto secundario |
| `--color-border` | `#504945` | Bordes |
| `--color-primary` | `#8ec07c` | Enlaces, borde de banda clave, cifras |
| `--color-accent` | `#fe8019` | Solo `strong.highlight` |
| `--color-warning` | `#fc7d6e` | Solo `span.error-mark`, siempre con tachado |
| `--color-code-bg` | `#3c3836` | Fondo de código |

Reglas:

- Los colores se usan solo mediante tokens; no hay valores sueltos en el CSS.
- Todo texto debe cumplir contraste WCAG AA (4,5:1).
- El error nunca depende solo del color: lleva tachado.
- Se evaluaron y descartaron Tokyo Night, Gruvbox amarillo y la paleta de
  Crunchyroll. El naranja se eligió porque separa mejor lo remarcado del texto,
  y el modo oscuro porque el rojo de error se ve mejor.

### Enlaces

- El color de enlace actual (`#8ec07c`) está aceptado, aunque el autor no
  percibe diferencia con la alternativa apagada. Si se revisa, el candidato
  evaluado es el celeste `#7cc4f4`.
- **El subrayado se mantiene** en los enlaces. Se evaluó quitarlo en los de
  navegación y se decidió dejarlo.
- Un enlace dentro de una oración debe tener algo más que el color (WCAG 1.4.1).

### Tipografía y grilla

Fuentes del sistema (decisión del autor; ver pendiente 6). Una sola regla:

- **Espaciado, alturas e interlineado: múltiplos de 4 px** (tokens `--space-*`,
  `--tap-size`, `--lh-*`).
- **Tamaños de letra: pares, en pasos de 4 px desde 16 px**; 14 px es la única
  excepción, por legibilidad en celular.

| Token | Valor | Interlineado |
|---|---|---|
| `--fs-sm` | 14 px | `--lh-sm` = 20 px |
| `--fs-base` | 16 px | `--lh-base` = 24 px |
| `--fs-lg` | 20 px | `--lh-lg` = 28 px |
| `--fs-xl` | 24 px | 36 px (hereda 1,5) |
| `--fs-2xl` | 28 px, 32 px desde 641 px | `--lh-2xl` = 36 px / 40 px |
| `--fs-code` | `0.875em` (14 px sobre 16) | `--lh-sm` |

- Los tamaños van en `rem` (respetan la preferencia de letra del usuario); el
  `em` solo se usa en `--fs-code`, para que el código acompañe al texto que lo
  rodea. No se escriben tamaños sueltos ni `px` en el texto.
- Un componente nuevo con texto usa estos tokens, y si cambia el tamaño define
  también su interlineado.

### Componentes del CSS

Clases con nomenclatura tipo BEM: `.ficha`, `.ficha__header`, `.ficha__kicker`,
`.ficha__subtitle`, `.ficha__pagination`, `.site-footer`, `dl.term-list`,
`.two-col`, `ul.tree`, `.tags`, `aside.callout`, `p.callout--key`,
`strong.highlight`, `span.error-mark`, `.sr-only`, `.concept` (+ `__head`,
`__id`, `__analogy`), `.toc` (+ `__id`) y `.topic` (+ `__summary`, `__title`,
`__count`).

- Índice del área: cada tema es un `<details class="topic">`, **cerrado por
  defecto**, con su nombre (`NN - Tema`) y el contador de contenidos en el
  `<summary>`, y sus contenidos adentro. Sin JavaScript. Al sumar un contenido o
  un tema hay que actualizar a mano el contador. Dentro de un tema, los enlaces
  no repiten el nombre del tema (`02.1 - Estructura jerárquica`).

- Conceptos de un glosario (`.concept` / `.toc`): se numeran con un entero
  simple del 1 al N dentro de la ficha, solo para ver cuántos son; sin prefijo
  de grupo, para que no se confundan con la numeración de contenidos (`01.3`).
  La analogía va en texto atenuado y cursiva, no en naranja (el naranja es del
  `strong.highlight`).
- Listas anidadas (un `<ul>` dentro de un `<li>` de una lista de sección o de un
  `.concept`): llevan sangría propia de 1,25 rem, ya resuelta en el CSS. En el
  HTML se escriben con 2 espacios por nivel y el `</li>` del punto padre cierra
  después del `</ul>` anidado.
- No se escriben estilos en el HTML (`<style>`, `style=`).
- Para contenido nuevo se reutilizan las clases existentes. Un componente nuevo
  se consulta antes y se agrega al final del CSS, con su sección numerada.

## 6. Convenciones del HTML

### Ficha (contenido)

```
<main id="inicio">
  <article class="ficha">
    <header class="ficha__header">
      <p class="ficha__kicker">  nombre del área  </p>
      <h1>  nombre del contenido  </h1>
      <p class="ficha__subtitle">  nombre del tema  </p>
    </header>
    … secciones …
    <nav class="ficha__pagination" aria-label="Paginación del contenido">…</nav>
  </article>
</main>
<footer class="site-footer">
  <p><a href="index.html">← Área</a> · <a href="#inicio">↑ Volver arriba</a></p>
</footer>
```

- Paginación: `← 01.1 - Título` y `01.2 - Título →`; sin "Parte N de M". Cruza
  de un tema a otro, y en ese caso el enlace lleva el nombre del tema:
  `02.1 - Fundamental: Estructura jerárquica →`. Al sumar un contenido hay que
  actualizar el enlace "siguiente" de la ficha anterior.
- Los ejemplos de dominio son ficticios y comunes a todo el sitio: `techcorp.local`
  (y `labcorp.local` cuando hace falta un segundo).
- El pie vuelve al **área** (no al inicio del sitio) y sube al inicio de la
  página sin tener que desplazarse.
- No hay notas al pie como "Reservorio — notas de estudio personales" ni
  "Parte 2 de 2".

### Textos y vocabulario

- La palabra para los elementos de un área es **"Contenidos"** (no "Fichas").
- En los índices no se muestran etiquetas (tags).
- Idioma `es`; archivos en UTF-8 con `<meta charset>`. Se escriben las tildes y
  la ñ directamente; las entidades se reservan para `&`, `<` y `>`.

### `<title>` y metadatos

- `<title>`: `Active Directory: qué es y cómo funciona` (área + título, sin
  sufijo "— Reservorio", para no alargar la pestaña).
- `og:title` y `headline` del JSON-LD: el mismo texto.
- `meta description`, Open Graph y JSON-LD por ficha. Los comentarios
  "Completar…" quedan para el momento de publicar.

### Formato del código

- `<head>` y `<body>` sin sangría; 2 espacios por nivel dentro de `<main>`.
- Todos los HTML siguen el mismo formato.

## 7. Contenido

Rescatado de las reglas anteriores, que siguen aplicando:

- **No se inventan datos.** Fechas, cifras, CVEs, comandos, puertos, versiones:
  si el autor no los dio, no se agregan. Un dato falso en material de estudio es
  peor que uno ausente.
- **No se completa ni se mejora el contenido** del autor aunque el agente sepa
  del tema. Se puede señalar: "falta X, ¿lo agregás?".
- Se señalan las contradicciones o los datos incompletos dentro de una ficha.
- **Repositorio público, sin información sensible:** nada de credenciales,
  nombres de clientes o empleadores, IPs/hosts internos ni datos personales.
  Para ejemplos de red se usan los rangos de documentación `192.0.2.0/24`,
  `198.51.100.0/24` y `203.0.113.0/24`.
- No se generan datos técnicos con IA de imágenes.

## 8. Pendientes (por prioridad)

1. ~~Mobile first y revisión a 375 px~~ (hecho, a revisar): los `@media` pasaron
   a `min-width: 40.0625rem`; áreas de toque de 44 px (`--tap-size`) en pie,
   paginación y listas; títulos más chicos en móvil (`--fs-xl`/`--fs-2xl`).
   Verificado por el autor en un celular real, ya publicado: funciona bien.
2. ~~Tokens de tamaño de letra~~ (hecho): escala de 14/16/20/24/28→32 px sobre
   la grilla de 4, interlineados en múltiplos de 4 y `--fs-code`; ver la
   sección de tipografía. Cuerpo de 17 a 16 px y páginas ~10–15% más cortas.
3. ~~Índice del área con temas desplegables~~ (hecho): `<details>/<summary>`
   cerrados por defecto, sin JS.
4. ~~`meta description` y Open Graph en la portada y en el índice del área~~
   (hecho).
5. ~~Indentación de `docs/index.html`~~ (hecho).
6. **Tipografía y `docs/fuentes/`:** decidido por ahora: **fuentes del sistema**
   (poco contenido, un solo lector). Inter (400/500) y JetBrains Mono (400/700)
   eran parte del diseño original y siguen en `docs/fuentes/` (`.ttf`, ~920 KB),
   **sin publicar y sin borrar**. Revisar cuando se publique con dominio propio;
   en ese caso convertirlas a `woff2` y solo latín (~100–150 KB).
7. **Revisar este archivo.** `AGENTS.md` debería contener solo lo que importa
   para construir y mantener el proyecto (estructura, convenciones, decisiones
   de diseño vigentes). Decidir qué de lo que hoy tiene no merece estar acá
   (por ejemplo la lista de pendientes, el historial de alternativas
   descartadas o las notas de cómo trabajar con el autor) y qué corresponde
   dejar solo en la memoria del asistente.
8. **JavaScript: reconsiderar solo con un disparador concreto.** Hoy el sitio
   se mantiene sin JS (decisión del autor). Revisar cuando haya unas 20 a 30
   páginas y haga falta un **buscador** (no hay búsqueda de servidor en GitHub
   Pages), o cuando actualizar a mano contadores, índices y enlaces de
   paginación cause olvidos o enlaces rotos: ahí lo que corresponde es un
   **script generador que corra al construir**, no JavaScript en el navegador.
9. **Dominio propio, `og:url` y `og:image`.** Hoy el sitio vive en la dirección
   `github.io`. Las etiquetas Open Graph `og:url` (dirección absoluta y
   canónica de cada página) y `og:image` (imagen de la vista previa, PNG o JPG
   de 1200 × 630 px, sin texto técnico) quedan marcadas con "Completar" en las
   páginas hasta decidir el dominio, para no cargarlas dos veces.

Otros: el kicker de la portada ("N áreas · N temas · N contenidos"), el contador
de la tarjeta del área y los contadores de cada tema del índice del área se
actualizan a mano al agregar contenido.

## 9. Mantener este archivo al día

Un archivo de instrucciones desactualizado es peor que no tenerlo. Si el autor
decide algo que contradice este documento, se actualiza en la misma tarea y se
avisa qué cambió.

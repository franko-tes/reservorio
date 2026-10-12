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

### Componentes del CSS

Clases con nomenclatura tipo BEM: `.ficha`, `.ficha__header`, `.ficha__kicker`,
`.ficha__subtitle`, `.ficha__pagination`, `.site-footer`, `dl.term-list`,
`.two-col`, `ul.tree`, `.tags`, `aside.callout`, `p.callout--key`,
`strong.highlight`, `span.error-mark`, `.sr-only`, `.concept` (+ `__head`,
`__id`, `__analogy`) y `.toc` (+ `__id`).

- Conceptos de un glosario (`.concept` / `.toc`): se numeran con un entero
  simple del 1 al N dentro de la ficha, solo para ver cuántos son; sin prefijo
  de grupo, para que no se confundan con la numeración de contenidos (`01.3`).
  La analogía va en texto atenuado y cursiva, no en naranja (el naranja es del
  `strong.highlight`).
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
2. **Tokens de tamaño de letra.** Tokenizar los `em` sueltos (`0.92em`, `0.9em`)
   y decidir si los títulos llevan `clamp()` en lugar de los dos tamaños fijos
   actuales (base móvil y `min-width`).
3. **Índice del área con temas desplegables:** mostrar solo los temas y
   desplegar los contenidos con un clic, con `<details>/<summary>` (sin JS; el
   hover no existe en celular). El tema 01 abierto mientras sea el único.
4. **`meta description`** en el índice del sitio y en el del área.
5. ~~Indentación de `docs/index.html`~~ (hecho).
6. **Tipografía y `docs/fuentes/`:** Inter (400/500) y JetBrains Mono (400/700)
   son parte del diseño original, pero el CSS actual usa fuentes del sistema.
   Decidir entre sistema o fuentes propias (en `woff2` y solo latín, ~100–150 KB,
   en lugar de los `.ttf` de ~920 KB). **No se borra la carpeta**; queda sin
   publicar (fuera del commit) hasta decidirlo.
7. **Revisar este archivo.** `AGENTS.md` debería contener solo lo que importa
   para construir y mantener el proyecto (estructura, convenciones, decisiones
   de diseño vigentes). Decidir qué de lo que hoy tiene no merece estar acá
   (por ejemplo la lista de pendientes, el historial de alternativas
   descartadas o las notas de cómo trabajar con el autor) y qué corresponde
   dejar solo en la memoria del asistente.

Otros: el kicker de la portada dice "1 área · 1 tema · 2 contenidos" y se
actualiza a mano al agregar contenido.

## 9. Mantener este archivo al día

Un archivo de instrucciones desactualizado es peor que no tenerlo. Si el autor
decide algo que contradice este documento, se actualiza en la misma tarea y se
avisa qué cambió.

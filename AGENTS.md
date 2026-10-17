# AGENTS.md

Instrucciones de trabajo para agentes de IA (y para cualquiera) que construya o
mantenga este repositorio. Última revisión: octubre de 2026.

---

## 1. Qué es y stack

Un reservorio de material de estudio sobre temas técnicos, publicado como sitio
estático. Es documentación propia del progreso del autor, no una plataforma.

- Todo vive en `docs/` y se publica con GitHub Pages desde la rama `main`,
  carpeta `/docs`. El repositorio es **público** (ver sección 6).
- El contenido lo escribe el autor. El agente ayuda con estructura, forma y
  revisión; no decide qué dice cada contenido.

**HTML y CSS. Nada más.** Sin JavaScript, frameworks, preprocesadores ni
dependencias externas.

- Las páginas tienen que abrirse con doble clic (`file://`) y desde GitHub Pages.
- Rutas siempre relativas.
- Cualquier tecnología nueva se propone y se espera la decisión del autor.
- JavaScript solo con un disparador concreto: un buscador (GitHub Pages no tiene
  búsqueda de servidor) o actualizaciones manuales que causen enlaces rotos. En
  ese segundo caso corresponde un script que genere el HTML al construir, no
  JavaScript en el navegador.

## 2. Estructura y nomenclatura

```
docs/
  index.html                        portada: solo muestra áreas
  estilo.css                        hoja única compartida
  <area>/
    index.html                      índice del área: sus temas y contenidos
    NN.N-<abreviatura>-<nombre>.html
```

Jerarquía: **área** (carpeta) → **tema** (primer número) → **contenido**
(segundo número).

- `NN` es el tema, `N` el orden dentro del tema, `<abreviatura>` la sigla del
  área (`ad` = Active Directory) y `<nombre>` una palabra que describe el
  contenido. Ejemplo: `01.1-ad-introduccion.html`.
- El tema lo nombra el autor y va como subtítulo de cada contenido.

## 3. Cómo se trabaja

- **Proponer antes de cambiar.** Ante la duda se pregunta, con opciones y una
  recomendación. Si el autor pide "analicemos", no se toca ningún archivo.
- **`git add`, `git commit` y `git push` los hace siempre el autor.** El agente
  pasa los comandos y muestra el diff si se lo piden.
- **Alcance mínimo:** solo se tocan los archivos que el pedido nombra.
- **Verificar antes de afirmar.** Medidas, contrastes y comparaciones se
  calculan o se prueban en el navegador. Si algo no se pudo verificar, se dice.

## 4. Diseño

### Paleta

**Gruvbox con acento naranja, modo oscuro fijo**; en impresión (`@media print`)
pasa a Gruvbox claro. Los valores viven en `:root` de `estilo.css`.

| Token | Uso |
|---|---|
| `--color-bg`, `--color-bg-subtle`, `--color-code-bg` | Fondo, bloques y callouts, código |
| `--color-text`, `--color-text-muted` | Texto y texto secundario |
| `--color-border` | Bordes |
| `--color-primary` | Enlaces, borde de banda clave, cifras |
| `--color-accent` | **Solo** `strong.highlight` |
| `--color-warning` | **Solo** `span.error-mark`, siempre con tachado |

- Los colores se usan solo mediante tokens; no hay valores sueltos.
- Todo texto cumple contraste WCAG AA (4,5:1).
- El error nunca depende solo del color: lleva tachado.

### Enlaces

Color `--color-primary`, con **subrayado**. Un enlace dentro de una oración debe
distinguirse por algo más que el color (WCAG 1.4.1).

### Tipografía y grilla

Fuentes del sistema. Una sola regla:

- **Espaciado, alturas e interlineado: múltiplos de 4 px** (`--space-*`,
  `--tap-size`, `--lh-*`).
- **Tamaños de letra: pares, en pasos de 4 px desde 16 px** (14 · 16 · 20 · 24 ·
  28 → 32 px); 14 px es la única excepción, por legibilidad en celular.
- Tamaños en `rem` mediante los tokens `--fs-*`. El `em` solo se usa en
  `--fs-code`. No se escriben tamaños sueltos ni `px` en el texto.
- Un componente nuevo con texto usa estos tokens y, si cambia el tamaño, define
  su interlineado.

### Componentes

Las clases están documentadas por sección en `estilo.css` (nomenclatura tipo
BEM: `.ficha__header`, `.topic__summary`).

- No se escriben estilos en el HTML (`<style>`, `style=`).
- Se reutilizan las clases existentes. Un componente nuevo se consulta antes y se
  agrega al **final** del CSS, con su sección numerada.
- **Glosario** (`.concept` / `.toc`): los conceptos se numeran con un entero
  simple del 1 al N dentro de la ficha (sin prefijo de grupo, para no confundirlo
  con `01.3`). Debajo del título, el subtítulo del concepto
  (`.concept__subtitle`: una analogía o una aclaración corta) va en texto
  atenuado y cursiva; el naranja es de `strong.highlight`.
- **Índice del área**: cada tema es un `<details class="topic">` **cerrado por
  defecto**, con `NN - Tema` y su contador de contenidos en el `<summary>`.
- **Listas anidadas**: llevan sangría propia (ya resuelta en el CSS). En el HTML,
  2 espacios por nivel y el `</li>` del punto padre después del `</ul>` anidado.

## 5. Convenciones del HTML

### Contenido (ficha)

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

- **Paginación:** `← 01.1 - Título` y `01.2 - Título →`. Cruza de un tema a otro,
  y en ese caso el enlace lleva el nombre del tema: `02.1 - Fundamental:
  Estructura jerárquica →`. El "siguiente" va siempre a la derecha.
- **Pie:** vuelve al **área** y sube al inicio de la página.
- **Etiquetas** (`ul.tags`) al final de cada contenido; no se muestran en los
  índices.

### Textos y vocabulario

- Para lo que ve el lector se dice **"contenido"** (no "ficha"); `.ficha` es solo
  el nombre de la clase.
- Etiquetas en `strong.highlight` al inicio de un punto: **"Riesgo:"** solo para
  problemas de seguridad y **"Relevante:"** para el resto.
- Idioma `es`; archivos en UTF-8 con `<meta charset>`. Las tildes y la ñ se
  escriben directamente; las entidades se reservan para `&`, `<` y `>`.

### `<title>` y metadatos

- **Contenido:** `<title>` = `<Área>: <título>` (por ejemplo `Active Directory:
  qué es y cómo funciona`), sin sufijo, para no alargar la pestaña.
- **Índices:** portada `Reservorio de estudio`; área `<Área> — Reservorio`.
- Toda página lleva `meta description` y Open Graph (`og:title`,
  `og:description`, `og:type`, `og:locale`). Los contenidos suman JSON-LD
  (`TechArticle`, con `isPartOf` = `<Área> — <Tema>` y `position`).
- `og:url`, `og:image`, `author` y `datePublished` quedan con el comentario
  "Completar…" hasta definir el dominio propio.

### Formato del código

`<head>` y `<body>` sin sangría; 2 espacios por nivel dentro de `<main>`. Todos
los HTML siguen el mismo formato.

## 6. Contenido

- **No se inventan datos.** Fechas, cifras, CVEs, comandos, puertos, versiones:
  si el autor no los dio, no se agregan. Un dato falso en material de estudio es
  peor que uno ausente.
- **No se completa ni se mejora el contenido** del autor aunque el agente sepa
  del tema. Se puede señalar: "falta X, ¿lo agregás?". También se señalan las
  contradicciones y los datos incompletos.
- **Repositorio público, sin información sensible:** nada de credenciales,
  nombres de clientes o empleadores, IPs/hosts internos ni datos personales.
  Para ejemplos de red, los rangos de documentación `192.0.2.0/24`,
  `198.51.100.0/24` y `203.0.113.0/24`.
- **Ejemplos ficticios y comunes a todo el sitio:** `techcorp.local` (y
  `labcorp.local` cuando hace falta un segundo).
- **Nombres de ejemplo en castellano** (OUs, áreas, grupos propios: `Finanzas`,
  `Sistemas`, `Empleados`). Los nombres reales de AD y Windows quedan en inglés
  (`Domain Controllers`, `CN=Users`, `Domain Admins`, atributos, etiquetas de la
  interfaz).
- No se generan datos técnicos con IA de imágenes.

## 7. Calidad mínima

- Contraste AA y áreas de toque de al menos 44 px (`--tap-size`).
- Un solo `h1` por página y encabezados sin saltos de nivel.
- Cada `<nav>` con su `aria-label`; `lang="es"`.
- Sin scroll horizontal desde 320 px de ancho.
- Enlaces relativos que resuelvan, y anclas (`#id`) que existan.

## 8. Mantenimiento

### Agregar un contenido

1. Crear `NN.N-<abreviatura>-<nombre>.html` a partir del formato de otro.
2. Índice del área: sumar la entrada dentro de su tema y actualizar el contador
   de contenidos de ese tema.
3. Paginación: completar "anterior" en el nuevo y el "siguiente" del contenido
   que lo precede.
4. Portada: contadores del encabezado (`N áreas · N temas · N contenidos`) y de
   la entrada del área.
5. Metadatos del nuevo: `<title>`, descripción, Open Graph y JSON-LD.
6. Verificar (ver abajo).

**Un tema nuevo** suma además un `<details class="topic">` en el índice del
área. **Un área nueva**, una carpeta con su `index.html` (copiando el de otra) y
su entrada en la portada.

### Verificar un cambio

- Servidor local: `python3 -m http.server --directory docs 8000`.
- Probar a 320, 375 y 1024 px: sin scroll horizontal y con los enlaces resueltos.
- Si el cambio es de CSS, comparar antes y después que las demás páginas no se
  mueven. El navegador puede servir el CSS viejo de caché: verificar en otro
  puerto o forzando la recarga.

### Este archivo

Tiene que reflejar el proyecto tal como está. Si el autor decide algo que lo
contradice, se actualiza en la misma tarea y se avisa qué cambió. Los pendientes
y el historial de decisiones no van acá.

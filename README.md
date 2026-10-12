# Reservorio

Notas de estudio personales sobre diversos temas, pensadas para consultar rápido,
sobre todo desde el celular. Es documentación propia del progreso de estudio: lo
que se aprende, ordenado para volver a leerlo.

**Sitio:** https://franko-tes.github.io/reservorio/

## Qué hay

El material se organiza en tres niveles:

| Nivel         | Qué es                     | Cómo se ve                            |
| ------------- | -------------------------- | ------------------------------------- |
| **Área**      | Un campo de estudio amplio | Una carpeta, con su propio índice     |
| **Tema**      | Un bloque dentro del área  | El primer número del archivo (`01.x`) |
| **Contenido** | Una ficha concreta         | Una página HTML (`01.1`, `01.2`, …)   |

## Cómo está armado

```
docs/
  index.html                  portada: lista las áreas
  estilo.css                  hoja de estilos única, compartida
  <área>/
    index.html                índice del área
    NN.N-nombre.html          un contenido (NN = tema, N = orden dentro del tema)
```

Por ejemplo, `active-directory/01.1-ad-introduccion.html` es el contenido 1 del
tema 01 del área Active Directory.

- **HTML y CSS, nada más.** Sin JavaScript, frameworks ni dependencias externas.
- **Rutas relativas**, así que las páginas se abren igual desde el sitio publicado
  que desde una copia local.
- **Diseño:** paleta Gruvbox con acento naranja, en modo oscuro fijo (en
  impresión pasa a claro). Pensado primero para pantallas chicas.

## Verlo en local

Alcanza con abrir `docs/index.html` en el navegador. Si se prefiere un servidor
local:

```bash
python3 -m http.server --directory docs 8000
```

y abrir `http://localhost:8000`.

## Publicación

El sitio se publica con GitHub Pages desde la rama `main`, carpeta `/docs`. Cada
`push` a `main` lo actualiza solo.

## Convenciones de trabajo

Las decisiones de diseño, la estructura de las fichas y los pendientes están en
[`AGENTS.md`](AGENTS.md). Ese archivo es la referencia para quien trabaje sobre el
repositorio, incluidos los asistentes de IA.

## Nota

El contenido son notas de estudio personales y pueden tener errores o quedar
desactualizadas. No son documentación oficial de ningún producto.

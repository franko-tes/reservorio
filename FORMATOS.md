# FORMATOS.md

Guía para volcar un tema estudiado a un archivo que el reservorio pueda recibir.

Este archivo está pensado para llevárselo a la conversación donde se estudió el tema:
contiene todo lo necesario para escribir el contenido, sin que haga falta conocer el
resto del proyecto.

---

## 1. Qué es esto

El reservorio guarda material de estudio sobre temas técnicos. Cada tema se escribe en
un archivo de texto plano con una estructura fija, y de ahí se construye la página.

El trabajo acá es uno solo: **volcar lo estudiado en la estructura de la plantilla
elegida**. La página se genera después, en otro momento y en otro lugar.

Dos cosas importantes sobre el contenido:

- **No se inventa nada.** Si un dato no se estudió, no entra. Un dato falso en material
  de estudio es peor que un dato ausente.
- **No se rellena para completar.** Un bloque sin contenido real se omite; es preferible
  a inventarle algo.

---

## 2. Los formatos

Hoy hay un formato, la **ficha**, con dos variantes:

| Variante (valor de `TIPO:`) | Para qué sirve | Quién lo lee |
|---|---|---|
| `ficha-tecnica` | Ayuda-memoria de una página. Condensa un tema en bloques fijos para recordarlo rápido meses después | Quien ya estudió el tema |
| `ficha-divulgacion` | Explicación del mismo tema sin conocimientos previos | Alguien ajeno al tema |

Las dos son **fichas**: material corto, de una página, pensado para leerse de una
sentada. No sirven para desarrollos largos.

---

## 3. Cómo elegir

**¿Quién va a leer esto?**

- Yo, para repasar → `ficha-tecnica`
- Otra persona que no conoce el tema → `ficha-divulgacion`
- Los dos → dos archivos separados, uno de cada variante

**¿El tema entra en una ficha?**

Una ficha condensa; no desarrolla. Si el tema necesita párrafos largos, ejemplos
extendidos o varios niveles de detalle, no entra en este formato. En ese caso conviene
avisarlo antes de escribir: hoy el reservorio no tiene un formato para eso.

**¿Un tema puede tener las dos fichas?**

Sí, y son **dos archivos completamente distintos**. La de divulgación no es la técnica
escrita más fácil: cambia el orden, cambian los bloques y cambia el texto entero. Si se
piden las dos, se escriben por separado.

---

## 4. Reglas de escritura

### 4.1 El encabezado

Todo archivo abre con estos campos, uno por línea, antes del primer bloque:

```
TIPO: ficha-tecnica
TITULO: EternalBlue / MS17-010
SUBTITULO: La vulnerabilidad que hizo posible WannaCry
CLAVES: smb, ransomware, wannacry, kernel, wormable
REFERENCIAS: MITRE ATT&CK · T1210 · T1021.002 · T1486 · T1490
```

| Campo | Obligatorio | Qué va |
|---|---|---|
| `TIPO` | sí | El formato y la variante, separados por guión: `ficha-tecnica` o `ficha-divulgacion` |
| `TITULO` | sí | El nombre del tema |
| `SUBTITULO` | no | Una línea de contexto |
| `CLAVES` | sí | Términos por los que se buscaría este tema. Cada uno se muestra como tag en el índice: conviene que sean pocos, los imprescindibles |
| `REFERENCIAS` | no | Dónde seguir: TTPs, CVEs, RFCs, páginas de manual |

### 4.2 Los bloques

Cada bloque se abre con su nombre entre corchetes, **en mayúsculas y sin acentos**:

```
[MECANISMO]
```

Eso vale para los marcadores y las subsecciones, que son las etiquetas del formato. El
**contenido se escribe con acentos normales**, aunque vaya en mayúsculas: lo que se lee
en la ficha es castellano y se escribe como tal.

Van en el orden que indica la plantilla. Un bloque sin contenido real se omite entero.

### 4.3 Las marcas

| Marca | Para qué | Ejemplo |
|---|---|---|
| `` `texto` `` | String literal: comando, ruta, CVE, puerto | `` `vssadmin delete shadows` `` |
| `*texto*` | Destacar un fragmento dentro de una línea | `*y entre segmentos internos*` |
| `\|` | Separa término de definición | `` `MS17-010` \| el parche `` |
| `-` | Ítem de una lista | `- Backups offline` |
| `>` | Comentario al margen | `> Es aritmética mal hecha.` |
| `!destacado` | Marca un elemento entero como relevante | `WannaCry !destacado \| el ransomware` |
| `!incorrecto` | Marca un elemento entero como ofensivo o erróneo | `EternalBlue !incorrecto \| el exploit` |
| `↻` | Nota al pie de una secuencia que se repite | `↻ el último paso reinicia el primero` |

Dos aclaraciones:

- `*asteriscos*` marca **fragmentos** dentro de una oración. `!destacado` e
  `!incorrecto` marcan **elementos completos**, y van al final del elemento. Hoy se usan
  sobre el nombre de un par (`[IDENTIDAD]`) y sobre un paso (`[SECUENCIA]`,
  `[EN LA PRACTICA]`). Un nombre de herramienta como `WannaCry` o `EternalBlue` no lleva
  backticks: no es un literal (ver regla 7 de `AGENTS.md`), solo la marca de énfasis.
- Una línea sola en MAYÚSCULAS, sin corchetes, abre una subsección dentro de un bloque.
  Se usa para los títulos de columna y para las partes de la analogía.

---

## 5. Plantilla · `ficha-tecnica`

```
TIPO: ficha-tecnica
TITULO:
SUBTITULO:
CLAVES:
REFERENCIAS:

[BANDA CLAVE]
Una sola frase: la que, si se olvida todo lo demás, permite reconstruir el tema.

[IDENTIDAD]
Los nombres que se confunden entre sí, y qué es cada uno. Un par por línea.
`nombre` | qué es
`otro nombre` !incorrecto | qué es

[MECANISMO]
Por qué funciona, en una o dos líneas. El detalle fino no va acá.

> Un comentario al margen, si aporta.

Hasta tres propiedades destacadas, opcional:
- PROPIEDAD | explicación corta
- PROPIEDAD | explicación corta
- PROPIEDAD | explicación corta

[SECUENCIA]
En qué orden pasan las cosas. Máximo cinco pasos.
Paso | detalle
Paso !incorrecto | detalle
Paso !destacado | detalle

↻ una nota, si la secuencia se repite

> Una aclaración, si hace falta.

[DATO ANCLA]
El número o hecho que se pega solo
Una línea que lo explique.

Tres hitos, si el dato tiene una línea de tiempo:
fecha | qué pasó
fecha | qué pasó
fecha | qué pasó

[QUE HAGO YO]
Lo operativo, en dos columnas. Los títulos dependen del tema:
mitigar/detectar, qué comando corro/qué reviso, qué configuro/qué miro.

TITULO DE LA PRIMERA COLUMNA
- Un ítem
- Otro ítem

TITULO DE LA SEGUNDA COLUMNA
- Un ítem
- Otro ítem

[TRAMPAS]
Lo que se cree mal sobre el tema, y la corrección.
"El mito." | La corrección.
"Otro mito." | La corrección.
```

---

## 6. Plantilla · `ficha-divulgacion`

```
TIPO: ficha-divulgacion
TITULO:
SUBTITULO:
CLAVES:
REFERENCIAS:

[BANDA CLAVE]
Una frase que se entienda sin saber nada del tema.

[QUE ES]
De qué se trata, en contexto. Uno o dos párrafos.

Hasta tres cifras de contexto, opcional:
- 200.000 | equipos afectados
- 150 | países alcanzados
- 1 día | para llegar a todos

[COMO FUNCIONA]
El mecanismo, en lenguaje llano. Un párrafo.

ANALOGIA
Una comparación con algo cotidiano. Opcional, pero si va, lleva las dos partes
siguientes.

TRADUCCION
Qué representa cada elemento de la analogía en el tema real.

AVISO
Qué alcance tiene la analogía y qué no explica.

> Un comentario al margen, si aporta.

[EN LA PRACTICA]
Cómo se ve u opera, paso a paso, en lenguaje llano. Máximo cinco pasos.
Paso | detalle
Paso !incorrecto | detalle

↻ una nota, si se repite

[POR QUE IMPORTA]
El dato que hace entender por qué el tema es relevante
Una línea que lo explique.

fecha | qué pasó
fecha | qué pasó
fecha | qué pasó

> Por qué sigue importando hoy.

[QUE HACER]
Recomendaciones o decisiones, en dos columnas. Sin tecnicismos.

TITULO DE LA PRIMERA COLUMNA
- Un ítem
- Otro ítem

TITULO DE LA SEGUNDA COLUMNA
- Un ítem
- Otro ítem

[GLOSARIO]
Los términos del tema, explicados en lenguaje llano. Van al final: quien lee
recién acá se encuentra con los nombres, cuando ya entendió de qué se trata.
Término | qué es
Término | qué es

> Una aclaración sobre los términos, si hace falta.
```

---

## 7. Cuando se termina

El archivo se guarda como `.txt` y se entrega tal cual. La conversión a página se hace
después, en el repositorio.

Si algo del tema no encaja en ninguna de las dos fichas, conviene decirlo en vez de
forzarlo: puede ser señal de que hace falta una variante o un formato nuevo.

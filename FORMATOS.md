# FORMATOS.md

Guía para volcar un tema estudiado a un archivo `.txt` que el reservorio pueda
convertir en una ficha. No hay estructura obligatoria: el texto puede ser tan largo
como haga falta, y las piezas van en el orden que tenga más sentido para el tema.

**Reglas de contenido, sin excepción:**
- No se inventa nada. Si un dato no se estudió, no entra.
- No se rellena para completar. Si algo no tiene contenido real, se omite.
- Todo string literal (comando, ruta, CVE, puerto) va marcado como literal.
- Ninguna pieza tiene un mínimo ni un máximo de repeticiones: se usan tantas veces
  (o ninguna) como el contenido real lo pida.

---

## 1. Encabezado

Antes del contenido, estos campos, uno por línea:

```
TITULO: 
SUBTITULO: 
RESUMEN: 
CLAVES: 
REFERENCIAS: 
```

| Campo | Obligatorio | Qué va |
|---|---|---|
| `TITULO` | sí | El nombre del tema |
| `SUBTITULO` | no | Una línea de contexto bajo el título |
| `RESUMEN` | sí | Una frase que resuma el tema. Se usa en la tarjeta del índice y en los metadatos de la página |
| `CLAVES` | sí | Términos de búsqueda, pocos, los imprescindibles |
| `REFERENCIAS` | no | CVEs, TTPs de MITRE, RFCs, páginas de `man`: dónde seguir leyendo |

---

## 2. El cuerpo: formatos disponibles

A partir de acá, el texto se arma combinando estos formatos, en el orden que el tema
pida. Cada uno tiene una marca fija; el resto (orden, cantidad, largo) queda a
criterio de quien escribe.

### 2.1 Título de sección

```
## Qué es
```
Abre una sección nueva. Usar tantas como haga falta.

### 2.2 Subtítulo

```
### Un aspecto puntual dentro de la sección
```
Para organizar una sección larga en partes.

### 2.3 Párrafo

Texto suelto, sin marca. Cada línea en blanco separa un párrafo del siguiente.

### 2.4 Lista

```
- Un ítem
- Otro ítem
```

### 2.5 Término → definición

```
`término` | qué es
`otro término` | qué es
```
Para un grupo de nombres que se confunden entre sí, o un glosario. Hay dos formas,
y la elige el propio marcado:

- **Con backticks en el término** (como en el ejemplo de arriba): queda en
  monoespaciada, pensada para nombres cortos y técnicos — comandos, siglas, nombres
  de proceso. Con esta forma no hace falta agregar además el literal en línea (2.6)
  sobre el término: el componente ya lo muestra como tal.
- **Sin backticks en el término**:
  ```
  término | qué es
  otro término | qué es
  ```
  queda en tipografía normal, pensada para definiciones más largas o conceptuales.

### 2.6 Literal en línea

```
`vssadmin delete shadows`
```
Cualquier cosa que se escriba tal cual en una terminal, un buscador o un campo de
configuración: comandos, rutas, puertos, CVEs, nombres de archivo.

### 2.7 Destacar un fragmento

```
*este fragmento es relevante*
```
Para una palabra o frase dentro de una oración que merece resaltarse. Se ve en el
color de énfasis del sitio.

### 2.8 Marcar un fragmento como incorrecto o erróneo

```
~esto es un error común~
```
Se ve en el color de alerta del sitio. Usar solo cuando el fragmento describe algo
mal hecho, un mito o un error real — no como sinónimo de "importante".

### 2.9 Comentario al margen

```
> Una aclaración en tono aparte, que no es parte del cuerpo principal.
```

### 2.10 Banda / idea destacada

```
!! La frase que resume o refuerza una idea clave.
```
Se puede usar en cualquier punto del texto, las veces que haga falta (o ninguna). Se
ve como un recuadro con una franja de color.

### 2.11 Dos columnas

```
PRIMERA COLUMNA
- Un ítem
- Otro ítem

SEGUNDA COLUMNA
- Un ítem
- Otro ítem
```
Un título en MAYÚSCULAS seguido de una lista, dos veces seguidas. Para comparar dos
grupos o dividir en dos categorías (ej. mitigar/detectar, decisiones/resguardos).

### 2.12 Cifras en fila

```
- 200.000 | equipos afectados
- 150 | países alcanzados
```
Para números de contexto que conviene ver de un vistazo.

### 2.13 Árbol jerárquico

```
[ARBOL]
Forest: techcorp.local
  Domain: techcorp.local
    OU Finance | usuarios, equipos
    OU IT | usuarios, equipos
[/ARBOL]
```
Cada nivel se indenta 2 espacios respecto del anterior. El `|` es opcional, separa el
nombre del nodo de un detalle corto.

### 2.14 Código multilínea

```
[CODIGO]
vssadmin delete shadows /all /quiet
reg add HKLM\...\LSA /v RunAsPPL /t REG_DWORD /d 1
[/CODIGO]
```
Para un comando o configuración de más de una línea. No confundir con el literal en
línea (2.6), que es para una palabra o frase suelta dentro del texto.

### 2.15 Secuencia de pasos

```
[SECUENCIA]
Paso | detalle
*Paso destacado* | detalle
~Paso incorrecto~ | detalle

↻ una nota, si la secuencia se repite
[/SECUENCIA]
```
En qué orden pasan las cosas. Si el nombre del paso (antes del `|`) va envuelto entero en
`*...*` o `~...~`, se marca el recuadro completo con el borde de color, no solo el texto —
mismas marcas que 2.7/2.8, pero aplicadas al campo entero en vez de a un fragmento. La `↻`
es opcional y va al final, solo si el proceso vuelve a empezar.

### 2.16 Dato ancla

```
[ANCLA]
El número o hecho que se pega solo
Una línea que lo explique.

fecha | qué pasó
fecha | qué pasó
[/ANCLA]
```
Un dato de contexto que ancla el tema. Los hitos de fecha son opcionales.

### 2.17 Analogía

```
[ANALOGIA]
La comparación con algo cotidiano.

TRADUCCION
Qué representa cada elemento de la analogía en el tema real.

AVISO
Qué alcance tiene la analogía y qué no explica.
[/ANALOGIA]
```
Las tres partes van juntas: no tiene sentido la analogía sin su traducción y su
aviso de alcance.

### 2.18 Trampas

```
[TRAMPAS]
"El mito." | La corrección.
"Otro mito." | La corrección.
[/TRAMPAS]
```
Lo que se cree mal sobre el tema, y la corrección.

---

## 3. Lo que no está contemplado

Si el tema necesita algo que no está en esta lista, no se improvisa: se avisa antes
de escribir, describiendo qué se necesita y para qué.

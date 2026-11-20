---
name: charts
description: Gráficos con Charts.css 1.2.0 por CDN — tablas con caption, tamaño y color con propiedades arbitrarias de Tailwind, tipos y colores de DESIGN.md §8 y cifras siempre visibles
scope: index.html (tablas con class="charts-css …")
---

# Reglas de los gráficos (Charts.css)

Aplican a los tres gráficos del bloque 2: embudo de ventas, rendimiento por plataforma y reparto
de comisiones por producto. Lee también [`tailwind.md`](tailwind.md) (TW-02 y TW-04) y
[`accessibility.md`](accessibility.md).

## CH-01 · Charts.css 1.2.0 por CDN: la única excepción a "solo Tailwind"

**Regla:** Charts.css se carga con este `<link>` exacto, en el `<head>`, antes del `<script>`
de Tailwind:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/charts.css@1.2.0/dist/charts.min.css">
```

No se usa ninguna otra librería de gráficos (Chart.js, ApexCharts, D3…), ni SVG ni `<canvas>`
dibujados a mano, ni otra versión de Charts.css sin preguntar a Mateo.

**Por qué:** `PLAN.md` §3 ("Única excepción: Charts.css por CDN
(`…charts.css@1.2.0/dist/charts.min.css`) para los gráficos") y §6; `DESIGN.md` §8 ("Es la
**única** excepción a 'solo Tailwind' que permite el enunciado").

**✅ Haz:** el `<link>` con la versión `@1.2.0` fijada.

**❌ Evita:** `charts.css@latest`, o un `<script src="…chart.js">`.

**Cómo comprobarlo:** `grep -n "charts.css@" index.html` devuelve una línea con `@1.2.0`.

## CH-02 · Cada gráfico es una `<table class="charts-css …">`, con tamaño y color en clases

**Regla:**

- Cada gráfico es una `<table>` con la clase `charts-css` y su tipo, y lleva `<caption>`,
  `<th scope="col">` en la cabecera y `<th scope="row">` en cada fila (como [HT-05](html.md)).
- El **valor** de cada dato se da con la propiedad arbitraria de Tailwind `[--size:…]` en su
  `<td>`, y el **color** con `[--color:var(--color-…)]`, tomando la variable del tema.
- Nunca con `style="--size: …"`: estaría prohibido por [TW-02](tailwind.md).
- La altura: en `column`, la da Charts.css con `aspect-ratio: 21/9` sobre el `<tbody>` (no
  depende del contenedor); en `bar`, se pone la altura en un `<div>` que envuelve la tabla
  (`h-44`…) y `h-full` en el `<tbody>`. La separación, con las clases `data-spacing-*` de
  Charts.css.
- **Charts.css no va en ninguna capa y Tailwind v4 pone sus utilidades en `@layer
  utilities`:** si los dos tocan la misma propiedad del mismo elemento (`background`,
  `padding`, `height`…), gana siempre Charts.css. Primero se busca otro elemento donde poner la
  clase (el relleno del dato va en `<span class="data">`, no en el `<td>`). Si no lo hay, se usa
  el modificador `!` de Tailwind (`[&_tr]:bg-lavanda-50!`) y se anota en el PR. Las variables de
  datos (`--size`, `--color`) no chocan, porque Charts.css solo las lee.

**Por qué:** `DESIGN.md` §8 ("Tamaño y color, con clases de Tailwind, no con `style`:
`[--size:0.63]` … y `[--color:var(--color-morado-500)]` … como propiedades arbitrarias en cada
`<td>`. Así no hace falta CSS propio"). Los tamaños de cada gráfico están en
[`plans/phase-2-html.md`](../../plans/phase-2-html.md) paso 5. Lo de la altura y las capas se
comprobó en el navegador en la fase 3 ([`memory-bank/progress.md`](../../memory-bank/progress.md)
§ "Fase 3").

**✅ Haz:** `<td class="[--size:0.63] [--color:var(--color-morado-900)]">…</td>` en la fila de
TikTok.

**❌ Evita:** `<td style="--size: 0.63; --color: #2F1C6A">`.

**Cómo comprobarlo:** `grep -c 'class="charts-css' index.html` devuelve 3; `grep -n "style=" index.html`
no devuelve nada; cada `<td>` de un gráfico tiene `[--size:`.

## CH-03 · Tipos, orden y colores de `DESIGN.md` §6 y §8

**Regla:**

| Gráfico | Clases de Charts.css | Orden y color de cada dato | `--size` |
|---|---|---|---|
| Embudo de ventas | `charts-css column show-labels data-spacing-*` | Alcance `morado-900` · Interacciones `morado-500` · Clics `lavanda-300` · Ventas `rosa-500` | 1 · 0,7 · 0,44 · 0,2 (orientativo) |
| Rendimiento por plataforma | `charts-css bar show-labels` | Instagram `morado-500` · TikTok `morado-900` · YouTube `rosa-500` | 1 · 0,63 · 0,53 |
| Reparto por producto | `charts-css bar multiple stacked` (una fila, 3 datos) | Producto A `morado-500` · Producto C `morado-900` · Producto B `rosa-500` (por comisión) | 0,352 · 0,344 · 0,304 |

En el embudo se añade la nota "Barras en escala orientativa, no proporcional", tal cual de `CONTENT.md` §3.1 (su sitio lo da `DESIGN.md` §6).

**Por qué:** `DESIGN.md` §8 (tipos) y §6 (colores de cada etapa, red y producto; "Los colores de
cada red se distinguen también por claridad"); tamaños en `plans/phase-2-html.md` paso 5.

**✅ Haz:** el embudo como `column`, con las 4 etapas en el orden de `CONTENT.md` §3.1.

**❌ Evita:** dibujar el embudo como `bar`, cambiar el orden de las redes o pintar YouTube de
morado.

**Cómo comprobarlo:** revisión del marcado frente a esta tabla y capturas de la fase 3 frente a
`design/mockup-2b-escritorio.dc.html`.

## CH-04 · Las cifras siempre visibles: nunca solo el color

**Regla:** Cada gráfico muestra **sus cifras escritas** (de `CONTENT.md`): la cifra de cada etapa
y su porcentaje de paso en el embudo; la red, la comisión y el ROI en cada barra de plataforma;
el producto y su comisión en el reparto. El color ayuda, pero nunca es la única forma de leer un
dato.

**Por qué:** `DESIGN.md` §1, regla 3 ("Cada gráfico explica algo … y lleva sus cifras escritas:
nunca depende solo del color"), §8 ("se mantienen … las cifras visibles") y §10.

**✅ Haz:** "Instagram · 1.779 € · ROI 2,97×" escrito encima o al lado de su barra.

**❌ Evita:** una barra apilada de tres colores sin ninguna cifra ni nombre de producto.

**Cómo comprobarlo:** en las capturas de la fase 3, cada barra y cada columna tiene su cifra
legible; todas esas cifras se encuentran en `CONTENT.md` §3.

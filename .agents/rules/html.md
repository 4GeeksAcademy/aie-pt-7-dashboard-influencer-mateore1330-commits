---
name: html
description: Cómo se escribe index.html — un solo archivo, semántico, con landmarks, jerarquía de títulos, anclas fijas, tablas accesibles y los textos de CONTENT.md
scope: index.html
---

# Reglas de HTML

Aplican a cualquier cambio en la estructura o los textos de `index.html`. Para las clases y el
tema, lee también [`tailwind.md`](tailwind.md); para los gráficos, [`charts.md`](charts.md); para
`aria-*`, foco y contraste, [`accessibility.md`](accessibility.md).

## HT-01 · Todo el dashboard va en un único `index.html`

**Regla:** La web es **un solo archivo**, `index.html`, en la raíz. No se crean otros `.html`,
ni archivos `.css`, ni `.js`. Lo único externo se carga por CDN desde el `<head>`: Tailwind v4,
Charts.css y Google Fonts (ver [TW-01](tailwind.md) y [CH-01](charts.md)).

**Por qué:** `PLAN.md` §1 ("Un dashboard de una sola página") y §3 (restricciones bloqueantes:
"CSS propio (archivos `.css` o reglas en `<style>`)" y "JavaScript propio" prohibidos).
`plans/phase-2-html.md` § "Entregables" solo lista `index.html`.

**✅ Haz:** escribir todo el marcado en `index.html`, con el `<head>` en el orden de
`plans/phase-2-html.md` paso 2.

**❌ Evita:** crear `styles.css`, `menu.js` o un `dashboard.html` aparte.

**Cómo comprobarlo:**

```bash
find . \( -name "*.css" -o -name "*.js" \) -not -path "./.git/*"   # sin resultados
find . -name "*.html" -not -path "./.git/*" -not -path "./design/*" # solo ./index.html
```

## HT-02 · HTML semántico y landmarks

**Regla:** Usa la etiqueta con significado, no un `div`. La página tiene, en este orden:

1. Enlace "Saltar al contenido" (`href="#contenido"`).
2. `<aside>` con el logo y `<nav aria-label="Secciones del panel">` (sidebar, ≥ `md`).
3. `<header id="cabecera">` (barra del móvil) con el enlace "Menú" y el panel `id="menu"`, que
   lleva un segundo `<nav aria-label="Secciones del panel">`.
4. `<main id="contenido">` con la cabecera del panel (`h1`, subtítulo, periodo) y **tres
   `<section>`**, una por bloque, cada una con `aria-labelledby` hacia su `h2`.
5. Dentro de cada bloque, cada tarjeta es un `<article>` con su `h3`.
6. `<footer>` con el texto de `CONTENT.md` §5.

Listas con `ul`/`ol`/`li` (enlaces, alertas, actividad, rankings), filtros con
`fieldset`/`legend`, cifras y etiquetas sin significado propio en `p` o `span`. El `div` solo
para agrupar sin significado (rejillas, el panel del menú).

**Por qué:** criterio 1 de `PLAN.md` §5 ("HTML semántico: etiquetas estructurales y landmarks
correctos") y `DESIGN.md` §4 (landmarks). La estructura detallada está en
[`plans/phase-2-html.md`](../../plans/phase-2-html.md) pasos 3 a 6.

**✅ Haz:** `<section id="resumen" aria-labelledby="resumen-titulo">` con
`<h2 id="resumen-titulo">01 · Resumen del mes</h2>` y un `<article>` por KPI.

**❌ Evita:** `<div class="kpi">` para un KPI, o un bloque sin `aria-labelledby`.

**Cómo comprobarlo:** el validador Nu de W3C (https://validator.w3.org/nu/) da 0 errores, y
`grep -c "<section" index.html` devuelve 3.

## HT-03 · Jerarquía de títulos: un `h1`, un `h2` por bloque, `h3` por tarjeta, sin saltos

**Regla:**

- Un solo `h1`: "Hola, Lucía".
- Un `h2` por bloque: "01 · Resumen del mes", "02 · Qué explica el resultado", "03 · El detalle".
- Un `h3` por tarjeta: el nombre de cada KPI y el título de cada tarjeta de drivers y detalle
  ("Embudo de ventas", "Plataformas", "Rankings"…).
- Nunca se salta un nivel ni se elige un título por su tamaño: el tamaño lo dan las clases.

**Por qué:** criterio 1 de `PLAN.md` §5 ("Un `h1`, un `h2` por bloque y `h3` por tarjeta, sin
saltos"). Los textos de cada título están en `CONTENT.md` §1 a §4; los tamaños, en `DESIGN.md` §3.

**✅ Haz:** `<h3>Comisiones</h3>` dentro del `<article>` del KPI de comisiones.

**❌ Evita:** un `h4` directamente bajo un `h2`, o poner la cifra de un KPI en un `h3` para que
salga grande.

**Cómo comprobarlo:** `grep -noE "<h[1-6]" index.html` lista los títulos en orden; hay un `h1`,
tres `h2`, y ningún nivel sube en más de uno respecto al anterior.

## HT-04 · Los IDs de ancla son fijos

**Regla:** Usa exactamente estos IDs, sin cambiarlos ni traducirlos:

| ID | Elemento |
|---|---|
| `contenido` | `<main>` (destino de "Saltar al contenido") |
| `cabecera` | `<header>` de la barra fija del móvil (destino de "Cerrar") |
| `menu` | Panel del menú hamburguesa (destino de "Menú") |
| `resumen` | `<section>` del bloque 1 |
| `plataformas` | `<section>` del bloque 2 |
| `productos` | `<article>` "Rendimiento por producto" |
| `campanas` | `<article>` "Campañas de octubre" |
| `alertas` | `<article>` "Alertas" |

Los radios de los rankings llevan `id="r-…"` y `name="ranking"` (ver
[`plans/phase-2-html.md`](../../plans/phase-2-html.md) paso 6).

**Por qué:** `CONTENT.md` §1 fija los destinos del menú (`#resumen`, `#plataformas`,
`#productos`, `#campanas`, `#alertas`); `DESIGN.md` §4 y §7 fijan `#contenido`, `#cabecera` y
`#menu`. El menú sin JavaScript depende de ellos.

**✅ Haz:** `<article id="campanas" aria-labelledby="campanas-titulo">`.

**❌ Evita:** `id="campañas"` (con ñ) o `id="campaigns"`: rompen los enlaces del menú.

**Cómo comprobarlo:** cada `href="#…"` apunta a un `id` que existe
(`grep -o 'href="#[^"]*"' index.html | sort -u` frente a `grep -o 'id="[^"]*"' index.html`).

## HT-05 · Tablas con `caption` y `th` con `scope`

**Regla:** Toda `<table>` (las de datos y las de Charts.css) lleva:

- `<caption>`. Puede ir oculta con `sr-only` si el `h3` de la tarjeta ya la nombra.
- `<thead>` con `<th scope="col">` en cada columna.
- En cada fila, la primera celda como `<th scope="row">` (plataforma, producto, campaña o etapa).
- El pie de tabla de `CONTENT.md` ("★ = mejor plataforma en esa métrica", "Las 135 ventas
  restantes llegaron fuera de campaña.") en un `<p>` o `<tfoot>` justo después.

**Por qué:** criterio 1 de `PLAN.md` §5 ("`table` con `caption` y `th scope`") y `DESIGN.md` §6
(Tablas). `DESIGN.md` §8: los gráficos son tablas "para que se lean bien con lector de pantalla".

**✅ Haz:** `<th scope="row">Instagram</th>` como primera celda de su fila.

**❌ Evita:** una tabla sin `caption`, o la fila de cabecera hecha con `<td>` en negrita.

**Cómo comprobarlo:** `grep -c "<table" index.html` y `grep -c "<caption" index.html` dan el
mismo número; ningún `<th>` aparece sin `scope` (`grep -n "<th>" index.html` sin resultados).

## HT-06 · Textos y cifras tal cual de `CONTENT.md`, y formato del código

**Regla:**

- Todo texto visible, cifra, `aria-label`, `<title>` y `meta description` sale **literal** de
  [`CONTENT.md`](../../CONTENT.md). No se reescribe, no se resume, no se redondea y no se añade
  ninguno.
- Las cifras van con el formato español de `CONTENT.md` §0: punto para los miles (`1.180.000`),
  coma para los decimales (`1,61 %`), espacio antes de `%` y de `€`, ROI como `2,48×`, y los
  signos `▲ ▼ ◆ ★ −` tal cual.
- Formato: `<!DOCTYPE html>`, `<html lang="es">`, sangría de **2 espacios** sin tabuladores, un
  elemento de bloque por línea.

**Por qué:** `CONTENT.md` (cabecera): "se copian **tal cual**. Si un texto o una cifra no está
aquí, se pregunta". `PLAN.md` §5: "Ningún texto ni cifra que no venga de `CONTENT.md`". El
formato de cifras está en `CONTENT.md` §0.

**✅ Haz:** el texto de la alerta de caída, exacto: "**Conversión en YouTube −0,6 pp.** Baja al
1,67 % durante "Unboxing B"." (`CONTENT.md` §4.4).

**❌ Evita:** "1.61%" (formato inglés), "3,8K €", "−0.6pp" o cualquier cifra calculada que no
esté escrita en `CONTENT.md`.

**Cómo comprobarlo:** cada texto se encuentra con `grep -F` en `CONTENT.md`; `grep -nP "\t"
index.html` no devuelve nada.

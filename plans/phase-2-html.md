# Fase 2 — HTML semántico completo

> Rama: `feat/phase-2-html` · PR a `main` · Depende de: fase 1 fusionada

## Objetivo

Escribir `index.html` con **toda la estructura y todo el contenido** del dashboard: landmarks,
los tres bloques, las tarjetas, las tablas, los gráficos de Charts.css, el menú móvil y los
rankings. El `<head>` ya carga Tailwind, el tema, las fuentes y Charts.css, pero **todavía no se
maqueta**: las únicas clases de esta fase son `sr-only`, las de Charts.css y las propiedades de
datos de los gráficos (`[--size:…]`). El estilo llega en la fase 3.

## Lee antes

- `AGENTS.md` y las reglas `using-rules.md`, `html.md`, `tailwind.md`, `charts.md` y
  `accessibility.md`.
- `CONTENT.md` entero (de ahí sale cada texto y cada cifra) y `DESIGN.md` §4, §7, §8 y §9.
- `design/mockup-2b-escritorio.dc.html` para el orden de las piezas dentro de cada bloque.

## Entregables

| Archivo | Contenido |
|---|---|
| `index.html` | Documento completo, sin maquetar |

## Pasos

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b feat/phase-2-html
```

### Paso 2 — `<head>`

En este orden:

1. `<meta charset="utf-8">` y `<meta name="viewport" content="width=device-width, initial-scale=1">`.
2. `<title>` y `<meta name="description">` de `CONTENT.md` §0. `<html lang="es">`.
3. Google Fonts: `preconnect` y el `<link>` de Geist (400, 500, 600, 700) y Geist Mono (400,
   500, 600).
4. Charts.css: `<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/charts.css@1.2.0/dist/charts.min.css">`.
5. Tailwind: `<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>`.
6. `<style type="text/tailwindcss">` con **solo** `@theme`: las fuentes y **todos** los
   colores de `DESIGN.md` §2, con sus nombres exactos.

Commit: `feat: add document head with tailwind theme, fonts and charts.css`

### Paso 3 — Esqueleto y navegación

- Enlace "Saltar al contenido" (`href="#contenido"`, clase `sr-only` por ahora).
- `<aside>` con el logo y `<nav aria-label="Secciones del panel">` con los 5 enlaces
  (`CONTENT.md` §1).
- `<header id="cabecera">` del móvil con el logo y el enlace "Menú" (`href="#menu"`, con el
  icono SVG de tres rayas con `aria-hidden="true"`). Dentro, el panel `<div id="menu">` con el
  enlace "Cerrar" (`href="#cabecera"`, nombre accesible "Cerrar menú"), un segundo
  `<nav aria-label="Secciones del panel">` con los 5 enlaces y sus números "01 /" … "05 /" con
  `aria-hidden="true"`, y el pie del menú.
- `<main id="contenido">` con la cabecera del panel: `h1` "Hola, Lucía", subtítulo y periodo.
- `<footer>` con el texto de `CONTENT.md` §5.

Commit: `feat: add page skeleton, sidebar and mobile menu markup`

### Paso 4 — Bloque 1: Resumen

`<section id="resumen" aria-labelledby="…">` con su `h2` y los 5 KPIs, cada uno un `<article>`
con `h3` (nombre), cifra, cambio y detalle (`CONTENT.md` §2).

Commit: `feat: add kpi summary block`

### Paso 5 — Bloque 2: Drivers

`<section id="plataformas" aria-labelledby="…">` con su `h2` y 4 tarjetas (`<article>` con `h3`
y subtítulo):

1. **Embudo de ventas:** `<table class="charts-css column show-labels">` con `caption`, una fila
   por etapa (`th scope="row"` y `td` con `[--size:…]`). Debajo, la lista de cifras y
   porcentajes de paso, y la nota de escala. Tamaños orientativos: 1 · 0,7 · 0,44 · 0,2.
2. **Rendimiento por plataforma:** `<table class="charts-css bar show-labels">` con la comisión
   y el ROI de cada red. Tamaños: 1 · 0,63 · 0,53. Pie con los costes.
3. **Rendimiento por producto** (`id="productos"`): las 3 tarjetas pequeñas y la
   `<table class="charts-css bar multiple stacked">` del reparto (0,352 · 0,344 · 0,304).
4. **Engagement y actividad:** tabla de engagement por red y lista de lo publicado.

Commit: `feat: add drivers block with charts.css tables`

### Paso 6 — Bloque 3: Detalle

`<section aria-labelledby="…">` con su `h2` y, en este orden:

1. **Alertas** (`id="alertas"`): una lista de 3 alertas con su tipo y su texto.
2. **Plataformas:** tabla completa de `CONTENT.md` §4.1 con su pie (★).
3. **Campañas de octubre** (`id="campanas"`) y **Productos**: tablas de §4.3 y §4.2.
4. **Rankings:** contenedor con la clase `group`; `<fieldset>` con
   `<legend class="sr-only">Elegir ranking</legend>` y 4 `<label>`, cada uno con su
   `<input type="radio" name="ranking" id="r-…" class="sr-only">` (el primero `checked`). Debajo,
   las **4 listas** `<ol>` (una por filtro, con `aria-label`), todas en el HTML. Cuál se ve se
   decide en la fase 4.

Commit: `feat: add operational detail block with tables, alerts and rankings`

### Paso 7 — Validar

- Validador Nu de W3C (https://validator.w3.org/nu/): **0 errores**, salvo los 2 del bloque `@theme` que exige Tailwind v4 (`type="text/tailwindcss"` y `@theme`, aceptados por Mateo el 20-11-2026). Para comprobar que no hay más, valida también una copia sin ese bloque: debe dar 0 mensajes.
- Esquema de títulos: un `h1`, tres `h2` y `h3` por tarjeta, sin saltos.
- Comparar cada texto y cada cifra con `CONTENT.md` (pega en el PR la lista revisada).
- `grep` sin resultados para `style=`, `cdn.tailwindcss.com`, `@apply`, `@tailwind`,
  `tailwind.config` y `onclick`.

Estado de la fase 2 en `PLAN.md` §4: **En revisión**; la 1, **Hecha**. Actualizar
`memory-bank/progress.md` y `current-state.md`.

Commit: `docs: update plan status and memory bank`

### Paso 8 — Push y PR

```bash
git push -u origin feat/phase-2-html
gh pr create --base main --title "feat: phase 2 – semantic html" --body "<resumen y criterios>"
```

## Criterios de aceptación

- [ ] Validador Nu con 0 errores, salvo los 2 del bloque `@theme` (resultado en el PR).
- [ ] Landmarks: `aside` + `nav`, `header`, `main`, 3 `section` con `aria-labelledby`, `footer`.
- [ ] 5 KPIs, 5 drivers (embudo, plataforma, producto, engagement, actividad) y detalle con 3
      tablas, alertas y 4 rankings.
- [ ] Las 3 tablas de Charts.css y las 4 de datos tienen `caption` y `th` con `scope`.
- [ ] Todos los textos y cifras coinciden con `CONTENT.md`.
- [ ] El `<style>` solo contiene `@theme`; 0 `style=""`; 0 JavaScript propio.

## Fuera de alcance

- Maquetar, colores, tamaños y breakpoints (fase 3).
- Que el menú y los filtros funcionen (fase 4).

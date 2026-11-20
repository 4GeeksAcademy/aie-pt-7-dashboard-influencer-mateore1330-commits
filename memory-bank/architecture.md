---
name: architecture
description: Estructura prevista del repositorio y de index.html — landmarks, los 3 bloques con sus tarjetas, anclas y breakpoints
last_verified: 2026-11-20 (sobre el commit e76d619, cierre de la fase 3)
---

# Arquitectura

> Describe la estructura de `PLAN.md` y `DESIGN.md` §4–5. A 20-11-2026 `index.html` tiene toda la
> estructura y el contenido (fase 2) y todo el estilo (fase 3); falta el menú y los filtros (fase 4).
> Ver [`current-state.md`](current-state.md).

## Estructura de archivos

```text
/
├── index.html                  ← el dashboard (fase 2: HTML; fase 3: Tailwind; fase 4: menú y filtros)
├── design/                     ← maqueta aprobada (solo referencia, no se publica)
│   └── screenshots/            ← capturas de las fases 3, 4 y 5
├── BRIEFING.md, CONTENT.md, DESIGN.md, PLAN.md, plans/
├── verification.md             ← fase 5
├── AGENTS.md, CLAUDE.md, .agents/ (rules, skills), memory-bank/
├── .githooks/pre-commit        ← gitleaks
├── .gitignore
├── README.md                   ← de la plantilla; se sustituye en la fase 5 (decisión abierta)
└── server.py, learn.json, .vscode/, README.es.md, README.cn.md   ← plantilla de 4Geeks
```

No hay archivos `.css` ni `.js` propios (regla [HT-01](../.agents/rules/html.md)).

## `index.html`, de arriba abajo

| Orden | Parte | Elemento e ID | Se ve en |
|---|---|---|---|
| — | `<head>` | Metas, Google Fonts, Charts.css, CDN de Tailwind y `<style type="text/tailwindcss">` con `@theme` | — |
| 1 | Saltar al contenido | `<a href="#contenido">`, `sr-only` hasta recibir el foco | Todos |
| 2 | Sidebar | `<aside>` con logo "LV", nombre, @usuario y `<nav aria-label="Secciones del panel">` | ≥ `md` |
| 3 | Barra fija del móvil | `<header id="cabecera">` con logo y enlace "Menú" → `#menu` | < `md` |
| 3a | Panel del menú | `<div id="menu">` (`hidden target:flex`), con "Cerrar" → `#cabecera`, `<nav>` con 5 enlaces y pie | < `md`, al abrirlo |
| 4 | `main` | `<main id="contenido">` | Todos |
| 4a | Cabecera del panel | `h1` "Hola, Lucía", subtítulo y periodo | Todos |
| 4b | Bloque 1 · Resumen | `<section id="resumen">`: 5 KPIs (`<article>`) | Todos |
| 4c | Bloque 2 · Drivers | `<section id="plataformas">`: embudo, plataforma, producto (`#productos`), engagement y actividad | Todos |
| 4d | Bloque 3 · Detalle | `<section aria-labelledby="detalle-titulo">`: alertas (`#alertas`), tabla de plataformas, campañas (`#campanas`) y productos (los dos en un mismo `div`, para ponerlos lado a lado en `xl`) y rankings | Todos |
| 5 | Pie | `<footer>` | Todos |

Anclas fijas: regla [HT-04](../.agents/rules/html.md). Las anclas llevan `scroll-mt-*` para que la
barra fija del móvil no tape el título.

## Breakpoints (`DESIGN.md` §5)

| Rango | Qué cambia |
|---|---|
| Base (< 640 px) | Barra superior fija con "Menú"; una columna; KPIs en 2 columnas (comisiones ocupa 2) |
| `sm` (≥ 640 px) | `px-6`; tarjetas de producto en 3 columnas |
| `md` (≥ 768 px) | Sidebar fija `w-56`; desaparecen la barra y el menú; periodo a la derecha |
| `lg` (≥ 1024 px) | KPIs en 3 columnas (comisiones 2 filas); alertas en 3 columnas |
| `xl` (≥ 1280 px) | KPIs en una franja de 6 columnas; drivers en 2 columnas; campañas y productos lado a lado |

## Piezas sin JavaScript

- **Menú:** `:target` sobre `#menu`; bloqueo de scroll con `has-[#menu:target]:overflow-hidden`
  en el `<body>` ([A11Y-05](../.agents/rules/accessibility.md)).
- **Filtros de los rankings:** contenedor `group`, radios `name="ranking"` con `id="r-…"`,
  `has-checked:` en cada `<label>` y `group-has-[#r-…:checked]:block` en cada `<ol>`
  ([A11Y-06](../.agents/rules/accessibility.md)).
- **Gráficos:** 3 `<table class="charts-css …">` con `[--size:…]` y `[--color:…]`
  ([CH-02](../.agents/rules/charts.md)).

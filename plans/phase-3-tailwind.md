# Fase 3 — Estilo con Tailwind, mobile-first

> Rama: `feat/phase-3-tailwind` · PR a `main` · Depende de: fase 2 fusionada

## Objetivo

Dar a `index.html` el aspecto aprobado (propuesta 2b) **solo con clases de Tailwind v4**,
empezando por el móvil y subiendo con `sm:`, `md:`, `lg:` y `xl:`. Al terminar, el dashboard se
ve como la maqueta a 1440 px y a 390 px, con la sidebar desde `md` y sin scroll horizontal en
ningún ancho. El menú móvil queda **oculto** (`hidden`); se activa en la fase 4.

## Lee antes

- `AGENTS.md` y las reglas `tailwind.md`, `charts.md` y `accessibility.md`.
- `DESIGN.md` entero, sobre todo §2 (colores), §3 (tipografía), §5 (breakpoints), §6
  (componentes) y §8 (gráficos).
- `design/mockup-2b-escritorio.dc.html` y `design/mockup-2b-movil.dc.html` para proporciones y
  espaciados.

## Entregables

| Archivo | Contenido |
|---|---|
| `index.html` | Con todas las clases de Tailwind |
| `design/screenshots/fase-3/` | Capturas a 375, 768, 1024 y 1440 px |

## Pasos

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b feat/phase-3-tailwind
```

### Paso 2 — Base y estructura

- `<body>`: `bg-fondo text-tinta font-sans antialiased`.
- Contenedor general: `md:flex`. Sidebar: `hidden md:flex md:w-56 md:shrink-0 md:sticky md:top-0
  md:h-dvh md:flex-col`. `main`: `flex-1 min-w-0` con su relleno.
- Barra superior del móvil: `fixed inset-x-0 top-0 md:hidden`; el `main` compensa su alto en
  móvil (`pt-*`) y las anclas llevan `scroll-mt-*`.
- Panel `#menu`: `hidden` (se activa en la fase 4).

Commit: `feat: style page layout, sidebar and mobile top bar`

### Paso 3 — Componentes base

Las clases comunes de `DESIGN.md` §6, **idénticas** en todos los elementos del mismo tipo:
tarjeta, `h2` de bloque, `h3` de tarjeta, cifra de KPI, etiqueta de estado, cabecera y filas de
tabla. Tablas dentro de `overflow-x-auto` con un ancho mínimo (`min-w-*`), y sus contenedores con
`min-w-0`.

Commit: `feat: add shared card, heading and table styles`

### Paso 4 — Bloque 1: KPIs

Rejilla con `gap-px bg-linea rounded-2xl overflow-hidden`:
`grid-cols-2` (comisiones `col-span-2`) → `lg:grid-cols-3` (comisiones `lg:col-span-1
lg:row-span-2`) → `xl:grid-cols-6` (comisiones `xl:col-span-2 xl:row-span-1`, el resto
`xl:col-span-1`). Comisiones en `bg-morado-500 text-white` con la píldora `bg-rosa-500
text-tinta`.

Commit: `feat: style kpi summary block`

### Paso 5 — Bloque 2: Drivers y gráficos

- Rejilla de tarjetas: una columna → `xl:grid-cols-2`.
- Gráficos de Charts.css con los colores de `DESIGN.md` §6 y §8 como propiedades arbitrarias
  (`[--color:var(--color-morado-900)]`…), alturas con clases de Tailwind (`h-48`…) y
  `data-spacing-*`.
- Tarjetas de producto: una columna → `sm:grid-cols-3`.

Commit: `feat: style drivers block and charts`

### Paso 6 — Bloque 3: Detalle

- Alertas: una columna → `lg:grid-cols-3`, con sus colores de `DESIGN.md` §6.
- Campañas y productos: una columna → `xl:grid-cols-2`.
- Ranking: cápsula de filtros `bg-lavanda-50`. Por ahora se ven las 4 listas; en la fase 4
  solo una.

Commit: `feat: style operational detail block`

### Paso 7 — Capturas y comprobaciones

Con la skill `rx-test-web`:

- Capturas de página completa a **375, 768, 1024 y 1440 px** en `design/screenshots/fase-3/`.
- A esos 4 anchos: `document.documentElement.scrollWidth === clientWidth`.
- Contraste: comprobar 5 pares al azar con una herramienta (deben coincidir con `DESIGN.md` §2).
- `grep` sin resultados para `style=`, `bg-[#`, `text-[#` y colores de la paleta por defecto
  (`purple-`, `pink-`, `violet-`, `gray-`, `slate-`…).

Estado de la fase 3 en `PLAN.md` §4: **En revisión**; la 2, **Hecha**. Actualizar el memory
bank.

Commit: `docs: add phase 3 screenshots and update memory bank`

### Paso 8 — Push y PR

```bash
git push -u origin feat/phase-3-tailwind
gh pr create --base main --title "feat: phase 3 – tailwind styles" --body "<resumen, capturas y criterios>"
```

Mateo compara las capturas con la maqueta antes de fusionar.

## Criterios de aceptación

- [ ] A 1440 px coincide con `mockup-2b-escritorio`; a 375 px, con `mockup-2b-movil`.
- [ ] Sidebar visible desde 768 px; por debajo, la barra superior con "Menú".
- [ ] 0 scroll horizontal a 375, 768, 1024 y 1440 px.
- [ ] Todos los colores salen del tema; 0 `style=""`; 0 CSS propio.
- [ ] Componentes del mismo tipo con la misma base de clases.

## Fuera de alcance

- Abrir y cerrar el menú y que los filtros cambien el listado (fase 4).

---
name: accessibility
description: Contraste con los pares de DESIGN.md, aria-hidden en lo decorativo, saltar al contenido, foco visible, zonas táctiles, menú con :target y filtros con fieldset
scope: index.html
---

# Reglas de accesibilidad

Aplican a cualquier cambio en `index.html`. Para auditar, usa la skill
[`accessibility`](../skills/accessibility/SKILL.md) (WCAG 2.2).

## A11Y-01 · Contraste de 4,5:1 o más, con los pares de `DESIGN.md` §2

**Regla:** Todo texto tiene un contraste de **4,5:1 o más** con su fondo. Usa solo las
combinaciones de texto y fondo que describe `DESIGN.md` §2 y §6. En concreto:

- **`rosa-500` nunca es color de texto sobre fondo claro** (da 3,16:1). Sobre claro, el rosa de
  texto es `rosa-700` (o `rosa-800` en la etiqueta "Por debajo").
- Sobre `rosa-500` (píldora "+12 %", botón "Cerrar") el texto es `tinta`, no blanco.
- Sobre `morado-900` (menú móvil), los enlaces van en blanco y los números y flechas, en
  `rosa-300`.

Si necesitas un par nuevo, mide su contraste y pregunta a Mateo antes de usarlo.

**Por qué:** `DESIGN.md` §2 ("Contraste comprobado … todas las combinaciones de texto superan
4,5:1" y "`rosa-500` sobre blanco da 3,16: por eso **no se usa como texto** sobre fondo claro") y
`PLAN.md` §5 ("Contraste de 4,5:1 o más en todo el texto").

**✅ Haz:** las bajadas (▼) en `text-rosa-700`.

**❌ Evita:** `text-rosa-500` sobre `bg-superficie` para "Caída", o texto blanco sobre la píldora
`rosa-500`.

**Cómo comprobarlo:** `grep -n "text-rosa-500" index.html` no devuelve nada; en la fase 3 se
miden 5 pares al azar con una herramienta de contraste
([`plans/phase-3-tailwind.md`](../../plans/phase-3-tailwind.md) paso 7).

## A11Y-02 · Lo decorativo, oculto al lector de pantalla

**Regla:** Lleva `aria-hidden="true"` todo lo que es solo decoración: el icono SVG de tres
rayas, el "✕" de "Cerrar", los números "01 /" … "05 /" y las flechas → del menú, los puntos de
la sidebar. Los signos con significado (▲ ▼ ◆ ★) **sí se leen**, y siempre van acompañados de
texto ("+12 %", "Caída", "★ = mejor plataforma en esa métrica"). El enlace "Cerrar" tiene como
nombre accesible "Cerrar menú".

**Por qué:** `DESIGN.md` §7 ("El '✕' va oculto al lector de pantalla", "Números y flechas son
decorativos (`aria-hidden="true"`)") y §10 ("Iconos decorativos con `aria-hidden="true"`; ▲ ▼ ◆ ★
van acompañados de texto"). Nombres accesibles en `CONTENT.md` §1.

**✅ Haz:** `<a href="#cabecera" aria-label="Cerrar menú"><span aria-hidden="true">✕</span> Cerrar</a>`.

**❌ Evita:** que el lector lea "cero uno barra Resumen flecha", o un ▼ solo, sin la cifra.

**Cómo comprobarlo:** `grep -n "<svg" index.html` y cada línea lleva `aria-hidden="true"`; en la
fase 5, prueba con VoiceOver del menú (`plans/phase-5-verification.md` paso 2).

## A11Y-03 · Enlace "Saltar al contenido" y foco siempre visible

**Regla:**

- El primer elemento del `<body>` es el enlace "Saltar al contenido" a `#contenido`: oculto con
  `sr-only` y visible al recibir el foco (`focus:not-sr-only` y su estilo).
- Todo lo que se puede pulsar (enlaces de la sidebar y del menú, "Menú", "Cerrar", filtros)
  tiene foco visible: `focus-visible:outline-2 focus-visible:outline-morado-500
  focus-visible:outline-offset-2`. Sobre el panel `morado-900`, el contorno es blanco. En los
  filtros, el foco del radio se ve en su `<label>` (`has-focus-visible:outline-*`).
- Las cajas `overflow-x-auto` de las tablas también reciben el foco (Chrome hace enfocables las
  zonas con scroll, y así se pueden mover con el teclado): llevan el mismo contorno morado, con
  `focus-visible:-outline-offset-2` para que no lo recorte la tarjeta.
- Nunca se quita el contorno (`outline-none`) sin poner otro foco visible.

**Por qué:** `DESIGN.md` §10 ("Foco visible en todos los enlaces y filtros (`focus-visible:…`)"),
`CONTENT.md` §1 ("Saltar al contenido") y
[`plans/phase-4-menu-filters.md`](../../plans/phase-4-menu-filters.md) paso 4.

**✅ Haz:** recorrer la página con Tab a 375 y 1440 px y ver siempre dónde está el foco.

**❌ Evita:** `outline-none` en los `<label>` de los filtros sin `has-focus-visible:`.

**Cómo comprobarlo:** recorrido con teclado en la fase 4 (orden lógico y foco visible en cada
paso); `grep -n "outline-none" index.html` solo aparece junto a otro estilo de foco.

## A11Y-04 · Zonas táctiles de 44 px o más

**Regla:** Los enlaces de la sidebar, "Menú", "Cerrar" y los filtros miden **44 px de alto o
más** (`min-h-11`). Los enlaces del panel del menú miden 60 px (`min-h-15`).

**Por qué:** `DESIGN.md` §6 (Sidebar: "Enlaces de 44 px o más"), §7 ("44 px de alto o más",
"de 60 px de alto") y §10 ("Zonas táctiles de 44 px o más").

**✅ Haz:** `min-h-11 inline-flex items-center` en "Menú".

**❌ Evita:** un filtro con `py-1 text-xs` que mide 24 px.

**Cómo comprobarlo:** en Playwright, `getBoundingClientRect().height >= 44` en cada enlace de
navegación, botón y `<label>` de filtro.

## A11Y-05 · Menú con `:target`: lo que funciona y lo que se pierde

**Regla:** El menú hamburguesa se hace **sin JavaScript**, con la técnica `:target` de
`DESIGN.md` §7:

- "Menú" es un enlace a `#menu`; el panel tiene `id="menu"` y `hidden target:flex`.
- "Cerrar" apunta a `#cabecera` (la barra fija), así que cierra sin mover la página.
- Al pulsar una sección, `#menu` deja de estar apuntado y el panel se cierra.
- Mientras está abierto, la página no hace scroll: `has-[#menu:target]:overflow-hidden` en el
  `<body>`, y `md:has-[#menu:target]:overflow-visible` para que el escritorio no se quede sin
  scroll si la dirección lleva `#menu`.
- En `md` y más, el panel nunca se ve: está dentro del `<header id="cabecera">`, que lleva
  `md:hidden`. No hace falta `md:target:hidden`.
- Mientras está abierto, lo que queda detrás (enlace "Saltar al contenido", logo y "Menú" de la
  barra, `<main>` y `<footer>`) lleva `[body:has(#menu:target)_&]:invisible`; en `<main>` y
  `<footer>`, además, `md:[body:has(#menu:target)_&]:visible`. Así el tabulador y el lector de
  pantalla no salen del panel.

Se **acepta** lo que se pierde: el lector oye "enlace" en vez de "botón, expandido"; Esc no
cierra; la URL muestra `#menu`; "Atrás" lo cierra. No se intenta arreglar con JavaScript ni con
ARIA que mienta (`role="button"`, `aria-expanded` fijo).

**Por qué:** `DESIGN.md` §7 ("Cómo se hace sin JavaScript (técnica `:target`, como en
web-artist)" y "Lo que se pierde (aceptado, igual que en web-artist)"); `PLAN.md` §6. Que el
foco se escape a la página oculta no está entre lo que `DESIGN.md` §7 acepta perder; el scroll
en escritorio y el foco atrapado se comprobaron en la fase 4
([`memory-bank/progress.md`](../../memory-bank/progress.md) § "Fase 4").

**✅ Haz:** `<div id="menu" class="hidden target:flex fixed inset-0 …">`.

**❌ Evita:** un `<button onclick>`, un `<input type="checkbox">` oculto para el menú, o
`aria-expanded="false"` en un enlace que nunca lo cambia.

**Cómo comprobarlo:** la prueba a 375 px de
[`plans/phase-4-menu-filters.md`](../../plans/phase-4-menu-filters.md) paso 2 (abrir, cerrar sin
moverse, ir a "Campañas", sin scroll con el menú abierto).

## A11Y-06 · Filtros de los rankings con `fieldset`, `legend` y radios reales

**Regla:** Los filtros son un `<fieldset>` con `<legend class="sr-only">Elegir ranking</legend>`
y 4 `<label>`, cada uno con su `<input type="radio" name="ranking">` real, oculto con `sr-only`
(no con `hidden`, que lo saca del teclado). El primero viene `checked`. El elegido se pinta con
`has-checked:` y cada listado se muestra con `group-has-[#r-…:checked]:block`. Cada `<ol>` lleva
su `aria-label`.

**Por qué:** `DESIGN.md` §10 ("Filtros de los rankings: `<fieldset>` con
`<legend class="sr-only">Elegir ranking</legend>` y radios reales ocultos con `sr-only` dentro
de su `<label>`"), `CONTENT.md` §4.5 (nombre del grupo y de los filtros) y
`plans/phase-4-menu-filters.md` paso 3.

**✅ Haz:** `<label class="… has-checked:bg-morado-500 has-checked:text-white"><input type="radio"
name="ranking" id="r-productos" class="sr-only" checked> Top productos</label>`.

**❌ Evita:** `<a>` o `<span>` que parecen filtros, o el radio con `hidden`.

**Cómo comprobarlo:** con teclado (Tab hasta el grupo y flechas) cada filtro muestra su listado
y solo ese; el lector anuncia "Elegir ranking, grupo".

## A11Y-07 · Audita con la skill `accessibility`

**Regla:** Al terminar una fase que toque `index.html`, y en la verificación final, usa la skill
[`accessibility`](../skills/accessibility/SKILL.md) para revisar la página contra WCAG 2.2. Lo
que encuentre se corrige o se anota en el PR.

**Por qué:** `plans/phase-1-agent-harness.md` (tabla de reglas: "Usar la skill `accessibility`
para auditar") y `plans/phase-5-verification.md` paso 2, comprobación 8 (Lighthouse con objetivo
100 y auditoría con la skill).

**✅ Haz:** citar en el PR de la fase 5 el resultado de la auditoría y de Lighthouse.

**❌ Evita:** dar la accesibilidad por buena sin haberla medido.

**Cómo comprobarlo:** `verification.md` incluye la auditoría y la puntuación de Lighthouse.

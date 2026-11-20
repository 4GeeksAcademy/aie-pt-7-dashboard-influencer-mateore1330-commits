# Fase 4 — Menú hamburguesa, filtros y foco

> Rama: `feat/phase-4-menu-filters` · PR a `main` · Depende de: fase 3 fusionada

## Objetivo

Hacer que funcionen, **sin JavaScript**, las dos piezas interactivas del dashboard:

1. El **menú hamburguesa** del móvil, con `:target`, igual que en Iron Wolf (`DESIGN.md` §7).
2. Los **filtros de los rankings**, con radios y las variantes `has-checked:` y
   `group-has-[…]:` de Tailwind.

Además, foco visible en todo lo que se puede pulsar.

## Lee antes

- `AGENTS.md` y las reglas `tailwind.md` y `accessibility.md`.
- `DESIGN.md` §6 (rankings), §7 (menú) y §10 (accesibilidad).
- `design/mockup-2b-menu-abierto.dc.html`.

## Pasos

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b feat/phase-4-menu-filters
```

### Paso 2 — Menú hamburguesa

- Panel `#menu`: `hidden target:flex fixed inset-0 z-50 flex-col bg-morado-900 text-white`.
- "Menú" (`href="#menu"`) y "Cerrar" (`href="#cabecera"`) con el estilo de `DESIGN.md` §7,
  44 px de alto o más.
- Enlaces del panel: 60 px de alto, líneas `border-morado-800`, números y flechas `rosa-300`
  con `aria-hidden="true"`.
- Bloqueo del scroll: `has-[#menu:target]:overflow-hidden` en el `<body>`.
- En `md` y más, el panel no se ve aunque esté apuntado (`md:hidden` junto a `target:flex`;
  comprobar cuál gana y ajustar con `md:target:hidden` si hace falta).

**Comprobar en el navegador (375 px):** abrir con "Menú"; cerrar con "Cerrar" sin que la página
se mueva; pulsar "Campañas" lleva a la tabla y cierra el menú; con el menú abierto, la página
no hace scroll.

Commit: `feat: add css-only mobile menu with target variant`

### Paso 3 — Filtros de los rankings

- Cada `<label>`: estilo de filtro sin elegir y, con `has-checked:`, el del elegido
  (`bg-morado-500 text-white`), según `DESIGN.md` §6.
- Cada lista: `hidden` y, con `group-has-[#r-…:checked]:block`, visible solo cuando su radio
  está marcado. La de "Top productos" se ve al cargar, porque su radio viene `checked`.
- Foco: el anillo de foco del radio se ve en su `<label>` (`has-focus-visible:outline-*`).

**Comprobar:** con ratón y con teclado (Tab hasta el grupo y flechas), cada filtro muestra su
listado y solo ese.

Commit: `feat: add css-only ranking filters with has-checked`

### Paso 4 — Foco visible y repaso de accesibilidad

- `focus-visible:outline-2 focus-visible:outline-morado-500 focus-visible:outline-offset-2` en
  enlaces y filtros. En el panel morado, contorno blanco.
- Enlace "Saltar al contenido": visible al recibir el foco (`focus:not-sr-only` y su estilo).
- Recorrido completo con el teclado a 375 y a 1440 px: el orden es lógico y nada queda sin foco
  visible.

Commit: `feat: add visible focus states and skip link styles`

### Paso 5 — Capturas y cierre

- Capturas en `design/screenshots/fase-4/`: menú abierto a 375 px, cada filtro de los rankings y
  el foco en la sidebar.
- Estado de la fase 4 en `PLAN.md` §4: **En revisión**; la 3, **Hecha**. Actualizar el memory
  bank.

Commit: `docs: add phase 4 screenshots and update memory bank`

### Paso 6 — Push y PR

```bash
git push -u origin feat/phase-4-menu-filters
gh pr create --base main --title "feat: phase 4 – mobile menu and ranking filters" --body "<resumen y criterios>"
```

## Criterios de aceptación

- [ ] El menú se abre, se cierra con "Cerrar" sin mover la página y se cierra solo al pulsar
      una sección.
- [ ] Con el menú abierto, la página no hace scroll; en `md` y más, el panel nunca se ve.
- [ ] Cada filtro muestra solo su listado, con ratón y con teclado.
- [ ] Foco visible en todos los enlaces y filtros; "Saltar al contenido" aparece con Tab.
- [ ] 0 JavaScript propio; 0 `style=""`; 0 CSS propio.

## Fuera de alcance

- Cambiar textos, colores o la maquetación de la fase 3, salvo un fallo que aparezca aquí (se
  anota en el PR).

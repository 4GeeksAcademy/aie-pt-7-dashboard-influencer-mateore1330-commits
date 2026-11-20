---
name: progress
description: Registro por fase — qué se hizo, decisiones, problemas y cómo se verificó
last_verified: 2026-11-20 (sobre el commit 5bc6e25, ajustes de la fase 4)
---

# Progreso

> Una sección por fase, en orden. Mantén este archivo al día al cerrar cada fase (regla UR-04).
> El plan de cada fase está en [`plans/`](../plans/).

## Sesión de diseño (20-11-2026)

**Qué se hizo:** antes de implementar, Mateo y el agente fijaron, en este orden: `BRIEFING.md` →
`CONTENT.md` → varias propuestas en el lienzo de diseño de Claude → `DESIGN.md` → `PLAN.md` y
`plans/`.

**Decisiones:**

- Influencer ficticia: Lucía Vega, @luvega.daily, lifestyle y bienestar. Datos de ejemplo de
  octubre de 2026, cuadrados con los precios (50, 120 y 80 €) y el 15 % de comisión.
- Mateo rechazó una primera maqueta por genérica, por los colores y por los gráficos. Diseño
  aprobado: "propuesta 2b · Studio claro morado" (estructura Studio en tema claro, morados y
  rosas), con sidebar desde `md` y menú hamburguesa con `:target` por debajo.
- Tailwind v4 solo por CDN, tema con `@theme`; Charts.css para los gráficos; sin JavaScript.
- Git simplificado: `main` + una rama por fase, sin `develop` ni GitHub Project.
- La implementación se hace en sesiones nuevas que solo dependen de lo que hay en el repositorio.

## Fase 0 — Preparación del repositorio (PR #1, fusionado el 20-11-2026)

**Qué se hizo:** `.gitignore` (primer commit de la rama), hook `.githooks/pre-commit` con gitleaks,
y versionados los documentos, la maqueta y el plan. 5 commits (`25763ca` a `c420433`).
`PLAN.md` pasó a **APROBADO**.

**Verificación:**

- El hook bloqueó un token falso `ghp_…` preparado en un archivo temporal (`leaks found: 1`,
  salida 1); el archivo no se commiteó y se borró.
- Los 4 commits posteriores al hook pasaron gitleaks (`no leaks found`); ninguno con
  `--no-verify`.
- `git status` limpio al terminar: `.learn/` y `.playwright-mcp/` ignorados.

## Fase 1 — Archivos para el agente (PR #2, fusionado el 20-11-2026)

**Qué se hizo:** `AGENTS.md`, `CLAUDE.md`, 6 archivos de reglas en `.agents/rules/` (UR-01 a
UR-04, HT-01 a HT-06, TW-01 a TW-07, CH-01 a CH-04, A11Y-01 a A11Y-07 y GD-01 a GD-05), los 5
archivos del memory bank y la skill `accessibility` copiada de Iron Wolf (idéntica, comprobado con
`diff -r`).

**Prueba en frío (paso 6):** un agente nuevo, que solo podía leer este repositorio, respondió bien
las 4 preguntas, citando la fuente de cada respuesta:

1. Qué fase toca: terminar la fase 1 (no empezar la 2 sin la fusión), según `AGENTS.md` §4.
2. `bg-purple-600` y `style="width: 60%"`: los dos prohibidos (TW-04, TW-02); la barra va con
   `[--size:…]` (CH-02).
3. Alerta de caída: `CONTENT.md` §4.4, texto exacto.
4. Menú sin JavaScript: `:target` (`DESIGN.md` §7, A11Y-05).

**Huecos que encontró y cómo se resolvieron:**

- La nota del embudo ("Barras en escala orientativa, no proporcional") solo estaba en `DESIGN.md`
  §6, y las reglas exigen que todo texto salga de `CONTENT.md`. Mateo decidió añadirla a
  `CONTENT.md` §3.1; CH-03 cita ahora esa fuente.
- `BRIEFING.md` y `CONTENT.md` seguían como "BORRADOR". Mateo los aprobó el 20-11-2026.
- La tabla de `PLAN.md` §4 y `last_verified` estaban desfasados: se actualizan al cerrar la fase.
- El choque entre `md:hidden` y `target:flex` sigue abierto a propósito: se resuelve en la fase 4
  (anotado en `current-state.md`).

## Fase 2 — HTML semántico completo (PR #3, fusionado el 20-11-2026)

**Qué se hizo:** `index.html` completo y sin maquetar, en 5 commits (uno por paso): `<head>`,
esqueleto y navegación, bloque 1 (5 KPIs), bloque 2 (embudo, plataforma y reparto por producto con
Charts.css, tarjetas de producto, engagement y actividad) y bloque 3 (alertas, tablas de
plataformas, campañas y productos, y rankings con `fieldset` y 4 radios).

**Decisiones:**

- **Engagement y actividad** es una sola tarjeta (`DESIGN.md` §6) con dos `h3`, que son los
  títulos de `CONTENT.md` §3.5 y §3.4, cada uno con su subtítulo. Lo decidió Mateo: no se usa el
  título de la maqueta ("Engagement y actividad"), que no está en `CONTENT.md`.
- **Validador W3C:** da 2 errores y los dos salen del `<style type="text/tailwindcss">` con
  `@theme`, que exige Tailwind v4 por CDN. Una copia sin ese bloque da 0 mensajes. Mateo los aceptó
  como justificados. Se actualizaron `PLAN.md` §5, HT-02, `plans/phase-2-html.md` y
  `plans/phase-5-verification.md`.
- Los textos de la maqueta que no están en `CONTENT.md` no se usan: "A 35 % · C 34 % · B 31 %",
  cabeceras abreviadas ("Coment.") y "vs septiembre".
- En la barra de cada red, la cifra es "1.779 € · ROI 2,97×", una combinación de valores y
  etiquetas de `CONTENT.md` §3.2 (CH-04).
- El reparto por producto es una `bar multiple stacked` con una fila ("Comisión") y una columna
  por producto, ordenadas por comisión (A, C, B). La celda de la esquina va vacía (`<td></td>`).
- El orden de las redes en las tablas es el de `CONTENT.md` (Instagram, TikTok, YouTube), no el de
  la maqueta.

**Verificación:**

- Validador Nu: los 2 errores aceptados del bloque `@theme`; sin el bloque, 0 mensajes.
- Títulos: 1 `h1`, 3 `h2` y 16 `h3`, sin saltos. 3 `section` con `aria-labelledby`.
- 7 tablas y 7 `caption`, sin ningún `<th>` sin `scope`. 3 gráficos de Charts.css.
- Las 8 anclas de los enlaces existen.
- 233 textos comparados con `CONTENT.md`: todos son literales o combinan valores y etiquetas
  literales.
- `grep`: 0 `style="`, 0 `cdn.tailwindcss.com`, `@apply`, `@tailwind`, `tailwind.config`, `on*=`;
  un solo `<script>` (el CDN) y un solo `<style>`.

## Fase 3 — Estilo con Tailwind, mobile-first (PR #4, fusionado el 20-11-2026)

**Qué se hizo:** todo el estilo de `index.html` con clases de Tailwind v4, en 6 commits: estructura
(sidebar fija desde `md`, barra superior fija en móvil, `scroll-mt-*` en las anclas), componentes
base, franja de KPIs, drivers con los gráficos, bloque de detalle y un `fix:` de las tarjetas de
producto. El panel `#menu` queda con `hidden` y las 4 listas de los rankings se ven todas (fase 4).

**Problemas y cómo se resolvieron:**

- **Charts.css gana a Tailwind:** Charts.css no va en ninguna capa y Tailwind v4 pone sus
  utilidades en `@layer utilities`, así que en la misma propiedad del mismo elemento siempre gana
  Charts.css. Por eso:
  - El relleno de las cifras de las barras va en `<span class="data">`, no en el `<td>`.
  - La pista `lavanda-50` de las barras de plataforma necesita `[&_tr]:bg-lavanda-50!`. Es el
    único `!` del archivo.
  - Queda escrito en CH-02.
- **Altura de los gráficos:**
  - En `column` la da `aspect-ratio: 21/9` sobre el `<tbody>`, y el sitio de las etiquetas
    lo reserva Charts.css con el margen inferior de cada fila.
  - En `bar` hace falta `h-full` en el `<tbody>`; si no, las barras no llenan el contenedor.
- **Etiquetas del embudo en móvil:** "Interacciones" se partía por cualquier letra (Charts.css
  pone `overflow-wrap: anywhere` en la fila). Se arregla con `break-normal hyphens-auto` en los
  `th`: "Interac-ciones".
- **Cifras del embudo en móvil:** se juntaban; pasan a `text-xs` en la base y a `text-sm` desde `sm`.
- **Tarjetas de producto a 768 y 1280 px:** "1.350 €" se partía. La lista de datos va en una
  columna desde `sm` y con `whitespace-nowrap`.
- **Barras de plataforma:** la cifra va dentro de la barra, en dos líneas (comisión y ROI), con
  la etiqueta de la red a la izquierda. Es una diferencia aceptada por `DESIGN.md` §8 respecto a la
  maqueta (que pone la cifra encima).
- **Comprobación de TW-01:** el patrón `@tailwind` encontraba el propio CDN
  (`@tailwindcss/browser`). Se cambia a `@tailwind[[:space:]]`.
- **Vista previa:** el puerto 8000 lo usa Docker en el equipo de Mateo; se usa el 8080.

**Verificación (Playwright):**

- Capturas de página completa a 375, 768, 1024 y 1440 px en `design/screenshots/fase-3/`.
- `scrollWidth === clientWidth` a 375, 768, 1024, 1280 y 1440 px.
- Sidebar visible desde 768 px; por debajo, la barra superior con "Menú".
- Contraste de todo el texto visible, con la fórmula de WCAG: el par más bajo es `rosa-700` sobre
  `rosa-50` (5,05:1). Las 4 cifras del embudo dentro de las columnas dan menos, pero están ocultas a
  la vista con `hide-data` (recortadas a 1×1 px, solo para el lector de pantalla).
- `grep`: 0 `style="`, 0 `[#…]`, 0 colores de la paleta por defecto, 0 `px` arbitrarios,
  0 `text-rosa-500`, 0 sintaxis de v3. Breakpoints en uso: `sm` (19), `md` (31), `lg` (4),
  `xl` (10). Las 8 tarjetas comparten la base de TW-06.

## Fase 4 — Menú hamburguesa, filtros y foco (en revisión)

**Qué se hizo:** las piezas interactivas, sin JavaScript, en 3 commits:

- **Menú hamburguesa** con `:target`: panel `morado-900` a pantalla completa, con "✕ Cerrar" en
  `rosa-500`, 5 enlaces de 60 px con número y flecha en `rosa-300`, y el pie.
- **Filtros de los rankings:** `has-checked:` en cada `<label>` y
  `group-has-[#r-…:checked]:flex` en cada `<ol>`.
- **Foco visible** en los 13 enlaces, en los 4 filtros y en las 4 cajas con scroll de las tablas.
  "Saltar al contenido" se ve al recibir el foco.

**Decisiones y problemas:**

- **Punto abierto de la fase 1 (`md:hidden` frente a `target:flex`):** no hace falta
  `md:target:hidden`. El panel está dentro del `<header>`, que lleva `md:hidden`; con el padre en
  `display: none`, el panel no se ve en `md` aunque `#menu` esté apuntado. Comprobado a 768 px.
- **Scroll en escritorio con `#menu` en la dirección:** el `<body>` se quedaba con
  `overflow: hidden` a 768 px. Se añade `md:has-[#menu:target]:overflow-visible`.
- **Foco que se escapaba del panel:** con el menú abierto, el tabulador salía a la página
  oculta. Lo que queda detrás pasa a `invisible` mientras `#menu` está apuntado
  (`[body:has(#menu:target)_&]:invisible`), y en `md` se deshace. El foco da vueltas dentro del
  panel: Cerrar → 5 enlaces → Cerrar.
- **Cajas con scroll de las tablas:** Chrome las hace enfocables. Llevan el contorno morado, con
  `-outline-offset-2`.
- **Comprobación de TW-04:** `\[#` encontraba `[#menu:target]` y `[#r-…:checked]`. Se cambia a
  `\[#[0-9a-fA-F]{3,8}\]`.
- **Playwright no puede pulsar los radios** (`sr-only`, 1 px): se prueban pulsando el `<label>`,
  como hace una persona.

**Verificación (Playwright):**

- **Menú a 375 px:**
  - Abrir no mueve la página (1500 px antes y después).
  - La rueda no desplaza la página con el menú abierto.
  - "Cerrar" deja la página donde estaba (`#cabecera`).
  - "Campañas" lleva a la tabla con el título a 105 px, por debajo de la barra de 64 px, y cierra
    el menú. Después el scroll vuelve.
- **Menú a 768 y 1440 px con `#menu`:** el panel no se ve, `<main>` y `<footer>` siguen visibles
  y hay scroll.
- **Filtros, con ratón y con teclado (flechas):** cada filtro muestra solo su lista y se pinta en
  `morado-500`. Al cargar, "Top productos". El foco del teclado se ve en el `<label>`.
- **Recorrido con Tab:**
  - A 1440 px: Saltar al contenido → 5 enlaces de la sidebar → tablas → filtros, todos con el
    contorno morado.
  - A 375 px: Saltar al contenido → Menú → (Enter) Cerrar y 5 enlaces, con el contorno blanco.
- **Zonas táctiles:** "Menú", "Cerrar", los filtros y la sidebar miden 44 px; los enlaces del
  panel, 60 px.
- **Scroll horizontal:** `scrollWidth === clientWidth` a 375, 768, 1024 y 1440 px.
- **`grep`:** 0 `style="`, 0 `on*=`, 0 colores arbitrarios, 0 `px` arbitrarios, 0
  `outline-none`; 1 `<script>` y 1 `<style>`.
- **Capturas** en `design/screenshots/fase-4/`: el menú abierto, los 4 filtros, el foco en la
  sidebar y "Saltar al contenido".

**Ajustes tras la revisión de Mateo (20-11-2026):** Mateo vio en Brave que la tarjeta de
comisiones era más grande que las otras, que las tablas se cortaban sin barra de scroll visible
(macOS la oculta) y fallos de márgenes. Decidió con un cuestionario:

- **KPIs iguales, como la maqueta:** 5 columnas iguales desde `xl`. Antes `DESIGN.md` §5 hacía
  comisiones el doble (en eso chocaba con la maqueta y no se le avisó en la fase 3). Cifras en
  `text-3xl` hasta `2xl`, para que "3.840 €" quepa a 1280 px. Nombres de KPI con `xl:min-h-10`
  para alinear las cifras.
- **Tablas sin scroll en escritorio:** desde 1024 px caben todas. Hacía falta:
  - Engagement y producto ocupan las 2 columnas en `xl`.
  - Campañas y productos, una debajo de otra.
  - Celdas `text-xs px-1.5` hasta `xl`, y títulos de columna que pueden partirse.
  - Margen lateral `px-6` hasta `xl` (la de plataformas no cabía a 1024 px por 32 px).
- **Tablas por debajo de 1024 px:** todas se desplazan (`min-w-3xl`), con el aviso "Desliza para
  ver toda la tabla →" (nuevo en `CONTENT.md` §0) y un degradado a la derecha. Con un ancho
  mínimo común, el aviso nunca aparece en una tabla que cabe (entre 768 y 1023 px alguna cabía).
- **Márgenes:**
  - Alertas dentro de una tarjeta.
  - Huecos de 16 px en las 3 secciones.
  - Pie de costes al fondo de su tarjeta.
  - "(sept: …)" sin partir.
  - Datos de producto en 2 columnas desde `lg`.

`DESIGN.md` §3, §5 y §6, TW-05 y TW-07 quedan actualizados. Comprobado con Playwright a 375, 640,
768, 900, 1023, 1024, 1100, 1279, 1280, 1440 y 1728 px: sin scroll en la página y, desde 1024 px,
ninguna tabla cortada. Capturas `pagina-*.png` en `design/screenshots/fase-4/`.


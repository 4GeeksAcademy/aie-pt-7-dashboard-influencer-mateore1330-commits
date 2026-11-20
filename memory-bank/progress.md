---
name: progress
description: Registro por fase — qué se hizo, decisiones, problemas y cómo se verificó
last_verified: 2026-11-20 (sobre el commit a244c9b, cierre de la fase 2)
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

## Fase 2 — HTML semántico completo (en revisión)

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

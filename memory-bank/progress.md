---
name: progress
description: Registro por fase — qué se hizo, decisiones, problemas y cómo se verificó
last_verified: 2026-11-20 (sobre el commit 5a01430, fase 1)
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

## Fase 1 — Archivos para el agente (en curso)

**Qué se hizo:** `AGENTS.md`, `CLAUDE.md`, 6 archivos de reglas en `.agents/rules/` (UR, HT, TW,
CH, A11Y y GD), los 5 archivos del memory bank y la skill `accessibility` copiada de Iron Wolf.

**Verificación:** pendiente de la prueba en frío (paso 6 de
[`plans/phase-1-agent-harness.md`](../plans/phase-1-agent-harness.md)).

---
name: current-state
description: Qué hay hoy en el repositorio, qué falta, cuál es la siguiente fase y qué decisiones siguen abiertas
last_verified: 2026-11-20 (sobre el commit 5bc6e25, ajustes de la fase 4)
---

# Estado actual

> **Actualízalo** al cerrar cada fase o cuando cambie el resultado de una comprobación (regla
> UR-04). La fecha y el commit de la cabecera indican cuándo se comprobó por última vez.

## Fases

| Fase | Estado |
|---|---|
| 0 — Preparación del repositorio | Hecha (PR #1 fusionado) |
| 1 — Archivos para el agente | Hecha (PR #2 fusionado) |
| 2 — HTML semántico completo | Hecha (PR #3 fusionado) |
| 3 — Estilo con Tailwind | Hecha (PR #4 fusionado) |
| 4 — Menú, filtros y foco | En revisión (rama `feat/phase-4-menu-filters`, PR a `main` sin fusionar) |
| 5 | Pendiente |

La tabla que manda es la de [`PLAN.md`](../PLAN.md) §4; lo que decide si una fase está terminada
es la fusión en `main`.

## Qué hay

- Documentos aprobados por Mateo: `BRIEFING.md`, `CONTENT.md`, `DESIGN.md`, `design/` y
  `PLAN.md` con `plans/`.
- `.gitignore` y hook de gitleaks (`.githooks/pre-commit`).
- Reglas, skill `accessibility`, memory bank, `AGENTS.md` y `CLAUDE.md` (fase 1).
- `index.html` completo (fase 2), con todo el estilo de Tailwind (fase 3) y con el menú, los
  filtros y el foco funcionando sin JavaScript (fase 4). Capturas en `design/screenshots/fase-3/`
  y `fase-4/`.

## Qué falta

- La verificación completa (validador, Lighthouse, skill `accessibility`, VoiceOver, revisión
  con `rx-review`) y `verification.md` (fase 5).
- `verification.md` y el README de entrega (fase 5).

## Siguiente fase

**Fase 5 — Verificación y entrega** ([`plans/phase-5-verification.md`](../plans/phase-5-verification.md)),
rama `chore/phase-5-verification`. Solo se empieza cuando el PR de la fase 4 esté fusionado en
`main` y Mateo haya dicho "sí" al resumen del plan. Antes del README se le preguntan las decisiones
abiertas de abajo.

## Decisiones abiertas (`PLAN.md` §7)

Se preguntan a Mateo cuando toque, con un cuestionario:

- **README de la plantilla (fase 5):** se propone sustituir `README.md` por uno del proyecto en
  español y quitar `README.es.md` y `README.cn.md`.
- **Publicación (fase 5):** si se publica en GitHub Pages. No lo pide el enunciado.
- **Contradicción del enunciado** ("solo Tailwind" frente a "el CSS con los estilos y las media
  queries"): se resuelve con los breakpoints de Tailwind y se explica en el README (fase 5).

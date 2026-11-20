---
name: current-state
description: Qué hay hoy en el repositorio, qué falta, cuál es la siguiente fase y qué decisiones siguen abiertas
last_verified: 2026-11-20 (sobre el commit 40d7539, cierre de la fase 1)
---

# Estado actual

> **Actualízalo** al cerrar cada fase o cuando cambie el resultado de una comprobación (regla
> UR-04). La fecha y el commit de la cabecera indican cuándo se comprobó por última vez.

## Fases

| Fase | Estado |
|---|---|
| 0 — Preparación del repositorio | Hecha (PR #1 fusionado) |
| 1 — Archivos para el agente | En revisión (rama `docs/phase-1-agent-harness`, PR a `main` sin fusionar) |
| 2 a 5 | Pendientes |

La tabla que manda es la de [`PLAN.md`](../PLAN.md) §4; lo que decide si una fase está terminada
es la fusión en `main`.

## Qué hay

- Documentos aprobados por Mateo: `BRIEFING.md`, `CONTENT.md`, `DESIGN.md`, `design/` y
  `PLAN.md` con `plans/`.
- `.gitignore` y hook de gitleaks (`.githooks/pre-commit`).
- Reglas, skill `accessibility`, memory bank, `AGENTS.md` y `CLAUDE.md` (fase 1).

## Qué falta

- `index.html`: no existe todavía.
- `verification.md` y el README de entrega (fase 5).

## Siguiente fase

**Fase 2 — HTML semántico completo** ([`plans/phase-2-html.md`](../plans/phase-2-html.md)), rama
`feat/phase-2-html`. Solo se empieza cuando el PR de la fase 1 esté fusionado en `main` y Mateo
haya dicho "sí" al resumen del plan.

## Decisiones abiertas (`PLAN.md` §7)

Se preguntan a Mateo cuando toque, con un cuestionario:

- **README de la plantilla (fase 5):** se propone sustituir `README.md` por uno del proyecto en
  español y quitar `README.es.md` y `README.cn.md`.
- **Publicación (fase 5):** si se publica en GitHub Pages. No lo pide el enunciado.
- **Contradicción del enunciado** ("solo Tailwind" frente a "el CSS con los estilos y las media
  queries"): se resuelve con los breakpoints de Tailwind y se explica en el README (fase 5).

## Pendiente para la fase 4

- Comprobar cuál gana entre `md:hidden` y `target:flex` en el panel `#menu`, y usar
  `md:target:hidden` si hace falta (`plans/phase-4-menu-filters.md` paso 2).

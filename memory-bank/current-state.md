---
name: current-state
description: Qué hay hoy en el repositorio, qué falta, cuál es la siguiente fase y qué decisiones siguen abiertas
last_verified: 2026-11-22 (sobre el commit 7cca890, cierre de la fase 5)
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
| 4 — Menú, filtros y foco | Hecha (PR #5 y sus arreglos en el PR #6, fusionados) |
| 5 — Verificación y entrega | En revisión (rama `chore/phase-5-verification`, PR a `main` sin fusionar) |

La tabla que manda es la de [`PLAN.md`](../PLAN.md) §4; lo que decide si una fase está terminada
es la fusión en `main`.

## Qué hay

El proyecto está **completo**:

- `index.html` con toda la estructura, el estilo de Tailwind y el menú, los filtros y el foco
  funcionando sin JavaScript.
- [`verification.md`](../verification.md) con las 10 comprobaciones en ✅: validador W3C,
  Lighthouse 100, axe sin problemas y revisión de Claudia sin nada bloqueante.
- `README.md` de entrega, en español.
- Capturas finales en `design/screenshots/fase-5/`.
- Documentos, reglas, memory bank y plan al día.

## Qué falta

- Que Mateo revise y fusione el PR de la fase 5.
- Que Mateo entregue en 4Geeks la URL del repositorio.

## Decisiones tomadas en la fase 5

- `README.md` propio en español; `README.es.md` y `README.cn.md` borrados.
- No se publica en GitHub Pages.
- La contradicción del enunciado ("solo Tailwind" frente a "el CSS y las media queries") se
  explica en el README: las media queries son los breakpoints de Tailwind.
- `server.py` borrado.
- VoiceOver no se probó; Lighthouse lo pasó Mateo en Brave.

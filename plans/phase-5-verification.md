# Fase 5 — Verificación y entrega

> Rama: `chore/phase-5-verification` · PR a `main` · Depende de: fase 4 fusionada

## Objetivo

Comprobar, con pruebas reales, que el dashboard cumple los 4 criterios de evaluación del
enunciado y los criterios globales de `PLAN.md` §5. Dejarlo documentado en `verification.md` y
preparar el README de entrega.

## Lee antes

- `PLAN.md` §5 y §7, `AGENTS.md` y todas las reglas.
- La skill `accessibility` y la skill `rx-review`.

## Pasos

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b chore/phase-5-verification
```

### Paso 2 — Comprobaciones

| # | Comprobación | Cómo |
|---|---|---|
| 1 | HTML válido | Validador Nu de W3C: 0 errores, salvo los 2 del bloque `@theme` que exige Tailwind v4; sin ese bloque, 0 mensajes |
| 2 | Semántica y jerarquía | Esquema de títulos y landmarks (lista en `verification.md`) |
| 3 | Solo Tailwind | `grep` sin resultados: `style=`, `cdn.tailwindcss.com`, `@apply`, `@tailwind`, `tailwind.config`, `<script` (aparte del CDN), `on[a-z]*=`, archivos `.css` propios. El `<style>` solo contiene `@theme` |
| 4 | Colores del tema | `grep` sin colores de la paleta por defecto ni `[#…]` |
| 5 | Mínimos del enunciado | Contar KPIs (≥ 3), drivers (≥ 3) y tablas o listados del bloque 3 |
| 6 | Responsivo | Capturas a 375, 768, 1024 y 1440 px en `design/screenshots/fase-5/`; `scrollWidth === clientWidth` en los 4 anchos |
| 7 | Menú y filtros | Prueba con ratón y teclado (fase 4) repetida |
| 8 | Accesibilidad | Lighthouse Accesibilidad (objetivo: 100) y auditoría con la skill `accessibility`. Prueba con VoiceOver: el menú, los filtros y una tabla |
| 9 | Textos y cifras | Repaso contra `CONTENT.md` |
| 10 | Revisión de código | Skill `rx-review` (o la agente Claudia) sobre `index.html` |

Si algo falla, se corrige en esta rama con un commit `fix:` por problema y se anota.

### Paso 3 — `verification.md`

Una tabla con cada comprobación, su resultado (✅/❌), la evidencia (comando, captura o enlace) y
el commit que la corrige si hubo fallo.

Commit: `docs: add verification report`

### Paso 4 — README de entrega

Preguntar antes a Mateo las decisiones abiertas de `PLAN.md` §7 (README de la plantilla y
publicación). Propuesta:

- `README.md` en español: qué es, cómo verlo en local, stack (Tailwind v4 por CDN y Charts.css),
  cómo se cumple cada criterio de evaluación, la contradicción del enunciado sobre "el CSS y las
  media queries" (se resuelve con los breakpoints de Tailwind) y cómo activar el hook de
  gitleaks.
- Quitar `README.es.md` y `README.cn.md` de la plantilla.

Commit: `docs: add delivery readme`

### Paso 5 — Cierre

Estado de la fase 5 en `PLAN.md` §4: **En revisión**; la 4, **Hecha**. Memory bank al día.

Commit: `docs: update plan status and memory bank`

```bash
git push -u origin chore/phase-5-verification
gh pr create --base main --title "chore: phase 5 – verification and delivery" --body "<resumen y criterios>"
```

Tras fusionar, Mateo entrega en 4Geeks la URL del repositorio.

## Criterios de aceptación

- [ ] Las 10 comprobaciones en ✅ en `verification.md`, con su evidencia.
- [ ] Capturas de los 4 anchos en `design/screenshots/fase-5/`.
- [ ] README de entrega aprobado por Mateo.
- [ ] El PR va contra `main` y no está fusionado.

## Fuera de alcance

- Funcionalidades nuevas que no estén en `CONTENT.md` o `DESIGN.md`.

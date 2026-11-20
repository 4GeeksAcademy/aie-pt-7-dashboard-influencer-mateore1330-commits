---
name: product-overview
description: Qué es el ejercicio, para quién es el panel, qué se entrega, con qué restricciones, cómo se evalúa y qué decide cada documento
last_verified: 2026-11-20 (sobre el commit c89abef, cierre de la fase 4)
---

# Descripción del producto

## El ejercicio

Ejercicio del bootcamp 4Geeks (AI Engineering PT 7): **"Un dashboard sencillo en Tailwind CSS"**
(`simple-dashboard-tailwind-css`). Se construye un dashboard de **una sola página** para una
influencer, que junta sus resultados de Instagram, TikTok y YouTube en tres bloques: **KPIs**,
**drivers** (qué explica el resultado) y **detalle operativo**. El repositorio parte de la
plantilla `html-hello` de 4Geeks (`server.py`, `learn.json`, README de la plantilla y
`.vscode/`). Fuente: [`PLAN.md`](../PLAN.md) §1 y §5.

### Restricción bloqueante

**Solo HTML y Tailwind CSS v4** (CDN `@tailwindcss/browser@4`). Ni CSS propio, ni `style=""`, ni
JavaScript propio, ni frameworks, ni sintaxis de Tailwind v3. Única excepción: **Charts.css** por
CDN para los gráficos. Reglas [TW-01](../.agents/rules/tailwind.md), [TW-02](../.agents/rules/tailwind.md)
y [CH-01](../.agents/rules/charts.md).

### Mínimos del enunciado y lo previsto

| Mínimo | Previsto |
|---|---|
| Al menos 3 KPIs | 5: comisiones, ventas, conversión, engagement y ROI |
| Al menos 3 drivers | 5: embudo, plataforma, producto, actividad y engagement |
| Tablas o listados de detalle | 3 tablas (plataformas, productos, campañas), alertas y rankings con 4 filtros |

### Los 4 criterios de evaluación (`PLAN.md` §5)

| # | Criterio | Se construye en |
|---|---|---|
| 1 | HTML semántico: landmarks correctos, jerarquía clara | Fase 2 |
| 2 | Tailwind CSS: solo utilities, sin CSS propio, breakpoints y flex/grid | Fases 3 y 4 |
| 3 | Layout y componentes: 3 bloques separados, jerarquía visual, componentes reutilizables | Fases 2 y 3 |
| 4 | Diseño responsivo: móvil, tablet y escritorio, mobile-first, sin scroll horizontal | Fases 3 y 4 |

### Entregable

El repositorio, con `index.html` en la raíz, `verification.md` y un README de entrega (fase 5).
Tras fusionar la fase 5, Mateo entrega en 4Geeks la URL del repositorio.

El enunciado pide "solo Tailwind, sin CSS propio", pero en la entrega menciona "el CSS con los
estilos y las media queries". Se resuelve con Tailwind (sus breakpoints son las media queries) y
se explica en el README (`PLAN.md` §7).

## La clienta

**Lucía Vega (@luvega.daily)** es una creadora de lifestyle y bienestar **ficticia**, aprobada por
Mateo el 20-11-2026. Promociona 3 productos (50, 120 y 80 €) y cobra un 15 % de comisión por
venta. Todas las cifras son **datos de ejemplo** de octubre de 2026 y cuadran entre sí.

El panel responde 5 preguntas (`BRIEFING.md` § "Lo que pide"): cuánto gana en comisiones, qué
productos generan más, qué tal convierten sus anuncios, qué plataformas dan mejor retorno y qué
engagement tiene cada red y producto. Además avisa de lo raro y dice dónde mejorar. Lo mira
**sobre todo en el móvil**, y quiere ver primero el resultado, después el porqué y, al final, el
detalle.

## Qué decide cada documento

| Documento | Qué decide |
|---|---|
| [`CONTENT.md`](../CONTENT.md) | Todos los textos y todas las cifras, tal cual |
| [`DESIGN.md`](../DESIGN.md) | Todo lo visual: colores, tipografía, estructura, breakpoints, componentes, menú, gráficos |
| [`BRIEFING.md`](../BRIEFING.md) | Quién es la clienta y qué pide |
| [`design/`](../design/) | Maqueta aprobada (propuesta 2b · Studio claro morado): solo referencia |
| [`PLAN.md`](../PLAN.md) y [`plans/`](../plans/) | Fases, ramas, pasos y criterios de aceptación |

Si algo no está en estos documentos, **se pregunta a Mateo** (regla
[UR-02](../.agents/rules/using-rules.md)).
